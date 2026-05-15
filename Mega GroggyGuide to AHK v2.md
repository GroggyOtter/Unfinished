I told everyone I wrote this...I just never finished it b/c my depression finally caught up to my love of coding.
That and dealing with shitty people on the sub also contributed to me not wanting to finish it.
I love teaching...but I hate the way our society behaves anymore. It's offputting.
My hope is that others will find this and learn something from it...then do great things. Or teach others. That's what I've always wanted.
I worked on this for almost a year straight. :(
-----------------------------------------------------------------------------------------------------------------------------------------

# GroggyGuide: A Comprehensive Look at How AHK v2 Works
- [GroggyGuide: A Comprehensive Look at How AHK v2 Works](#groggyguide-a-comprehensive-look-at-how-ahk-v2-works)
- [Intro](#intro)
- [Get the best AHK v2 editor and make your life easier](#get-the-best-ahk-v2-editor-and-make-your-life-easier)
- [Expressions and Boolean](#expressions-and-boolean)
    - [What things are *not* expressions](#what-things-are-not-expressions)
    - [Operator arities: Unary, binary, and ternary](#operator-arities-unary-binary-and-ternary)
    - [Operator prescedence](#operator-prescedence)
        - [Order of operations, kind of like PEMDAS](#order-of-operations-kind-of-like-pemdas)
            - [Sub-expressions outrank operators](#sub-expressions-outrank-operators)
            - [Sub-expressins do NOT have levels of precedence](#sub-expressins-do-not-have-levels-of-precedence)
        - [A simple way to ensure order](#a-simple-way-to-ensure-order)
        - [Recap of operator precedence](#recap-of-operator-precedence)
    - [Boolean logic, true/false, and decision making](#boolean-logic-truefalse-and-decision-making)
        - [Evaluating boolean](#evaluating-boolean)
        - [Fun with true and false](#fun-with-true-and-false)
        - [Making a toggle using Boolean values](#making-a-toggle-using-boolean-values)
- [Functions](#functions)
    - [Scope and global space](#scope-and-global-space)
        - [The unwritten rule of global space](#the-unwritten-rule-of-global-space)
        - [Functions and scope](#functions-and-scope)
        - [Logical organization, abstraction, and meaningful names](#logical-organization-abstraction-and-meaningful-names)
        - [Global variables - don't use them](#global-variables---dont-use-them)
            - [Examples of global variable alternatives](#examples-of-global-variable-alternatives)
    - [The benefits and simplicity of functions](#the-benefits-and-simplicity-of-functions)
    - [Define a function](#define-a-function)
    - [Return values](#return-values)
        - [Function return values replaced v1's `ErrorLevel` variable](#function-return-values-replaced-v1s-errorlevel-variable)
    - [Parameters](#parameters)
        - [Learing about references, dereferencing, and double derefs](#learing-about-references-dereferencing-and-double-derefs)
        - [Passing parameters "by reference" vs "by value"](#passing-parameters-by-reference-vs-by-value)
        - [Required parameters](#required-parameters)
        - [Optional parameters](#optional-parameters)
        - [Understanding `unset`](#understanding-unset)
            - [Benefits of using unset](#benefits-of-using-unset)
            - [The "maybe" `?` operator](#the-maybe--operator)
            - [The "or maybe" `??` operator](#the-or-maybe--operator)
        - [Varaidic parameters and the variadic `*` operator](#varaidic-parameters-and-the-variadic--operator)
            - [Asterisk `*` can be used as a splat operator](#asterisk--can-be-used-as-a-splat-operator)
            - [Callbacks and using variadic parameters to discard input](#callbacks-and-using-variadic-parameters-to-discard-input)
        - [`FindWords()`, an example using all parameter types](#findwords-an-example-using-all-parameter-types)
        - [ByRef parameters and "by reference" variables](#byref-parameters-and-by-reference-variables)
        - [Parameter recap](#parameter-recap)
    - [Static variables are permanent variables](#static-variables-are-permanent-variables)
        - [Creating and using a static variable](#creating-and-using-a-static-variable)
    - [Reference counting and functions](#reference-counting-and-functions)
        - [Garbage collection and functions](#garbage-collection-and-functions)
        - [Static variables and reference counting](#static-variables-and-reference-counting)
        - [Circular references and memory leaks](#circular-references-and-memory-leaks)
        - [What does the word static mean?](#what-does-the-word-static-mean)
    - [Optional parentheses and function call statements](#optional-parentheses-and-function-call-statements)
    - [Nested functions](#nested-functions)
        - [Nested function scope](#nested-function-scope)
        - [Free variables, closures, and static functions](#free-variables-closures-and-static-functions)
    - [Naming variables and functions](#naming-variables-and-functions)
- [Syntax Sugar: Ternary, fat arrows, and code reduction](#syntax-sugar-ternary-fat-arrows-and-code-reduction)
    - [Ternary operator](#ternary-operator)
        - [Creating a ternary statement](#creating-a-ternary-statement)
        - [if/else vs ternary](#ifelse-vs-ternary)
        - [Pros and cons](#pros-and-cons)
        - [Formatting/aligning ternary statements](#formattingaligning-ternary-statements)
            - [Inline alignment](#inline-alignment)
            - [True/false aligned](#truefalse-aligned)
            - [Arrow aligned](#arrow-aligned)
    - [Or Maybe](#or-maybe)
    - [Fat arrow functions `() =>`](#fat-arrow-functions--)
        - [Anonymous functions](#anonymous-functions)
        - [The different types of fat arrow functions](#the-different-types-of-fat-arrow-functions)
        - [What fat arrows cannot do](#what-fat-arrows-cannot-do)
    - [Parentheses are powerful so use them](#parentheses-are-powerful-so-use-them)
    - [Ways to remove excess curly braces](#ways-to-remove-excess-curly-braces)
        - [Control flow can usually omit code blocks](#control-flow-can-usually-omit-code-blocks)
        - [If/else statements](#ifelse-statements)
        - [Functions, hotkeys, and hotstrings](#functions-hotkeys-and-hotstrings)
    - [Complex examples using sugar syntax](#complex-examples-using-sugar-syntax)
- [Objects](#objects)
    - [What is an "Object"?](#what-is-an-object)
    - [Understanding the point of an object](#understanding-the-point-of-an-object)
    - [When to use objects](#when-to-use-objects)
    - [Why the words "object", "property", and "method"?](#why-the-words-object-property-and-method)
        - [Object - A term for anything](#object---a-term-for-anything)
        - [Property - A term for describing attributes of something](#property---a-term-for-describing-attributes-of-something)
        - [Method - A term to describe a procedure](#method---a-term-to-describe-a-procedure)
        - [Fun fact: They're all autological words](#fun-fact-theyre-all-autological-words)
    - [Creating an object and object literals](#creating-an-object-and-object-literals)
    - [Properties](#properties)
        - [The dot `.` is the "member access operator"](#the-dot--is-the-member-access-operator)
        - [Add a property](#add-a-property)
        - [Add properties when creating an object](#add-properties-when-creating-an-object)
        - [Whitespace in AHK](#whitespace-in-ahk)
        - [Make object literals more readable](#make-object-literals-more-readable)
        - [Using a property](#using-a-property)
        - [Properties can contain objects](#properties-can-contain-objects)
        - [Built-in properties](#built-in-properties)
        - [Own properties](#own-properties)
    - [Descriptor objects define how a property behaves](#descriptor-objects-define-how-a-property-behaves)
        - [REMOVE? Using a descriptor to produce v1 behavior](#remove-using-a-descriptor-to-produce-v1-behavior)
        - [Understanding descriptors](#understanding-descriptors)
            - [DefineProp() and `value` descriptors](#defineprop-and-value-descriptors)
        - [`Call` descriptor](#call-descriptor)
        - [`Get` and `Set` descriptor](#get-and-set-descriptor)
        - [Shortening up descriptors](#shortening-up-descriptors)
    - [Methods](#methods)
        - [Calling methods and returning values](#calling-methods-and-returning-values)
        - [Built-in Methods](#built-in-methods)
            - [`Clone()`](#clone)
            - [`DefineProp()`](#defineprop)
            - [`DeleteProp()`](#deleteprop)
            - [`GetOwnPropDesc()`](#getownpropdesc)
            - [`HasOwnProp(Name)`](#hasownpropname)
            - [`OwnProps()`](#ownprops)
- [Arrays](#arrays)
    - [Traditional arrays vs AHK arrays](#traditional-arrays-vs-ahk-arrays)
    - [Making and using arrays](#making-and-using-arrays)
    - [Using arrays inside arrays](#using-arrays-inside-arrays)
    - [Array built-in properties](#array-built-in-properties)
        - [`Length`](#length)
        - [`Capacity`](#capacity)
        - [`Default`](#default)
        - [Special object property `__Item`](#special-object-property-__item)
    - [Array built-in methods](#array-built-in-methods)
        - [Adding and removing elements](#adding-and-removing-elements)
            - [`InsertAt()` and `RemoveAt()`](#insertat-and-removeat)
            - [`Push()` and `Pop()`](#push-and-pop)
            - [Origin of push, pop, and stack](#origin-of-push-pop-and-stack)
        - [Working with elemements](#working-with-elemements)
            - [`Has(index)`](#hasindex)
            - [`Get()`](#get)
            - [`Delete()`](#delete)
        - [Duplicating with `Clone()`](#duplicating-with-clone)
        - [Special object methods `__New()` and `__Enum()`](#special-object-methods-__new-and-__enum)
- [JSON](#json)
    - [A JSON object must be a "value"](#a-json-object-must-be-a-value)
    - [Data types](#data-types)
        - [Data rules](#data-rules)
    - [Whitespace](#whitespace)
    - [Data structures](#data-structures)
    - [Why use JSON?](#why-use-json)
    - [Some examples](#some-examples)
        - [Comparing JSON text to an AHK object](#comparing-json-text-to-an-ahk-object)
- [Object-oriented programming](#object-oriented-programming)
    - [The 4 pillars of OOP](#the-4-pillars-of-oop)
    - [Encapsulation](#encapsulation)
    - [Inheritance](#inheritance)
    - [Polymorphism](#polymorphism)
        - [Method overloading](#method-overloading)
        - [Method overriding](#method-overriding)
    - [Abstraction](#abstraction)
        - [Documentation is important](#documentation-is-important)
    - [Recap](#recap)
- [Classes](#classes)
    - [Classes have different uses](#classes-have-different-uses)
        - [Classes can be used to create objects](#classes-can-be-used-to-create-objects)
        - [Classes can be the object that is used](#classes-can-be-the-object-that-is-used)
        - [Classes can do both of these things](#classes-can-do-both-of-these-things)
    - [The Class class documentation page](#the-class-class-documentation-page)
        - [Classes are objects](#classes-are-objects)
        - [Classes have a static Call() method](#classes-have-a-static-call-method)
        - [Classes have a Prototype property](#classes-have-a-prototype-property)
            - [Please don't call them "blueprints"](#please-dont-call-them-blueprints)
    - [Making a class](#making-a-class)
    - [`Extends` keyword](#extends-keyword)
    - [The class members: Properties and methods](#the-class-members-properties-and-methods)
    - [Adding and using a property](#adding-and-using-a-property)
    - [Adding and using a method](#adding-and-using-a-method)
    - [Creating class members with `static`](#creating-class-members-with-static)
    - [Methods return values just like functions](#methods-return-values-just-like-functions)
    - [The hidden `this` parameter](#the-hidden-this-parameter)
    - [The `Base` property and hidden `super` parameter](#the-base-property-and-hidden-super-parameter)
    - [Creating an auto-clicker using a class](#creating-an-auto-clicker-using-a-class)
    - [Dynamic properties](#dynamic-properties)
        - [Unerstanding getters and setters](#unerstanding-getters-and-setters)
        - [Creating a dynamic property](#creating-a-dynamic-property)
        - [Class dynamic properties](#class-dynamic-properties)
        - [The `get` method](#the-get-method)
            - [Read-only properties with `get`](#read-only-properties-with-get)
        - [The `set` method](#the-set-method)
            - [The hidden `Value` parameter of `set`](#the-hidden-value-parameter-of-set)
        - [Backfields - Storing dynamic property values](#backfields---storing-dynamic-property-values)
        - [Dynamic property parameters](#dynamic-property-parameters)
        - [Dynamic properties vs making getters and setters](#dynamic-properties-vs-making-getters-and-setters)
        - [AHK does not have class access modifiers](#ahk-does-not-have-class-access-modifiers)
    - [Special class member names](#special-class-member-names)
        - [Make anything callable with `Call()`](#make-anything-callable-with-call)
        - [`__New()` and `__Delete()`, the constructor and the deconstructor](#__new-and-__delete-the-constructor-and-the-deconstructor)
        - [`__Enum()` the enumerator](#__enum-the-enumerator)
        - [`__Init()`](#__init)
    - [Meta-functions: Handling undefined things](#meta-functions-handling-undefined-things)
        - [`__Call()` - Handles undefined method calls](#__call---handles-undefined-method-calls)
        - [`__Get()` - Handles undefined property usage](#__get---handles-undefined-property-usage)
        - [`__Set()` - Handles the setting of properties](#__set---handles-the-setting-of-properties)
        - [Recap](#recap-1)
    - [The `__Item` property](#the-__item-property)
    - [The `__Class` property](#the-__class-property)
- [Fat Arrows](#fat-arrows)
    - [Fat Arrow Tips](#fat-arrow-tips)
- [Documentation for AHK's built in classes](#documentation-for-ahks-built-in-classes)
    - [Doc page structure and layout](#doc-page-structure-and-layout)
    - [Special class properties](#special-class-properties)
        - [`__Class`](#__class)
        - [`__Item`](#__item)
        - [`Base`](#base)
        - [`Prototype`](#prototype)
    - [Special class methods](#special-class-methods)
        - [`Call()`](#call)
        - [`__New()`](#__new)
        - [`__Delete()`](#__delete)
        - [`__Enum()`](#__enum)
        - [`__Init()`](#__init-1)
    - [Meta-functions](#meta-functions)
        - [`__Call()`](#__call)
        - [`__Get()`](#__get)
        - [`__Set()`](#__set)
        - [](#)
        - [](#-1)
    - [The Big Class Cheat Sheet](#the-big-class-cheat-sheet)
    - [Classes in other languages](#classes-in-other-languages)
    - [Class Cheat Sheet](#class-cheat-sheet)
- [Provide all the types of polymorphic examples in the class section?](#provide-all-the-types-of-polymorphic-examples-in-the-class-section)
    - [Bonus: You are learning more than AHK](#bonus-you-are-learning-more-than-ahk)
- [Examples](#examples)
    - [Class timer vs instance timers](#class-timer-vs-instance-timers)
    - [Rock, paper, scissors using a table.](#rock-paper-scissors-using-a-table)
- [Donations](#donations)
- [Cheat sheets](#cheat-sheets)
    - [Operator Precedence List](#operator-precedence-list)

# Intro

Writing a GroggyGuide takes a **lot** of time.  
I try to make them as thorough and educational as possible, including things I'd want to be taught.  
This whole thing started off as a project to do a dive into classes and it quickly spiraled out of control.  

This guide now covers a myriad of topics spanning the entirety of AHK.  
From discussing expressions to the fundamentals of functions to the entire concept of object-oriented programming.  

This document has become a massive compendium of different topics pertaining to AHK.  

I'm not sure how to classify this document.  
It's not hard, raw documentation.  
But it's not a beginners guide.  
It's a guide to teach you many core parts to AHK.  

The tone is supposed to be informal, as though I'm sitting at a table talking to you in person.  

Be comfortable and take it one topic at a time.  
If you don't get something, skip and come back.  
Or go to the subreddit and make a post asking for more information.  
Someone, possibly myself, will answer you.  

While I wouldn't advise jumping into this if you're brand new to the language, this document was written with the greener coder in mind.  
I try to make it a point to explain things how I would want them explained to me.  

Another thing that was taken into consideration is how much people like code examples.  
This document is littered with all kinds of code.  
Most of it is "example" code, designed specifically to showcase the subject at hand, but there are plenty of practical examples, too.  

Almost everything can be copy and pasted into a script and ran.  
And make sure to read the comments of the code as much is explained in them.  

I don't teach everything there is to know and this isn't meant to be a "tutorial".  
Instead, I cover a lot of core topics and different areas with the hopes you'll understand the language as a whole better.  
And I do deep-dive into each topic.  
Classes is a massive section by necessity. Because classes, while not super complicated, have a lot to offer.  
I tried to go over EVERYTHING.  
It's all about understanding how each part works, why we have them, what alternatives we have, how does AHK process something, what steps does it take, how and when are things deleted...all kinds of stuff.  

That brings me to another point I'd like to include.  
A lot of technical terms are used and I made sure to give the best descriptions I could.  
As you read through this, you'll keep learning more and more stuff and this stuff is not necessarily exclusive to AHK.  
In fact, a lot of these technical terms, topics, and concepts I include in here are applicable to MANY languages.  
By reading through this, I'm hoping to not only enrich your AHK knowledge, but your knowledge of programming as a whole.

To the people who say "I'm not a programmer...", I said the same thing.  
I teach it to people now!  

* If you start understanding AHK, you're already starting to understand JavaScript.  
* As you start understanding classes better, Java becomes more accessible.  
* As you start dealing with more low-level stuff (which I do not cover in this GroggyGuide but don't be surprised if one shows up later) in AHK, C/C++ starts becoming more accessible.  
* The entire OOP section of the guide is designed to help you understand OOP in general, not just in AHK.

The point of this is to ***just teach***.  

To clarify the time investment: There have been **entire sections** rewritten, some MANY times, because I didn't like the way they sounded or they were too long-winded or they didn't cover everything.  
I've consulted external sources (forums, people, and even AI) to get different ways of describing things until I felt each topic in this guide was properly covered.  

And pertaining to the examples, **I can NOT emphasize this enough**:  
Play with the code provided!  
Make it your own.  
Change things, add things, remove things.  
If at any point you wonder "What if...", you should quit wondering and do it.  
If there's an error there's an error. The script quits and exits out. No harm done and, most importantly, you learned something.  
This is when learning turns into understanding.  

There is a MASSIVE amount of information provided, so don't be expecting a quick read.  
You'll want to take it in sections.  

Don't get intimidated by any of the topics or big words you might see (looking at you, "polymorphism") because everything gets broken down, everything has code examples, and at the very worst you can always make a post on the forum or subreddit and ask for clarification or expounding of a topic.  

***RANDOMNESS***...you will see a LOT of random comments throughout here.  
There's a reason for it.  
Part of this writing style I do is talking to people. It's common to interject things in conversations.  
Unlike speech, I can always easily get back to the topic at hand...but I do like to share random things.  
Random facts.  
Random tips.  
Random history.  
Expect random things.  

Another oddity you might encounter is that I'm extremely consistant about some coding behaviors but I randomly do other things.  
I have a very set way I like to code and if I wrote everything the way I normally do, you'd see that.  
However, this is about learning. I write things ALL KINDS of ways in here.  
If you pay attention, you'll notice that when there are varying ways to write something, I try to do so. To expose you to other ways to write stuff.  
Example: We talk about making an array with the class `Array()` constructor or with array literal syntax `[]`.  
In AHK, these are BOTH acceptable (and I explain both formats in this guide).  
In AHK, all of these add one, so I'm inclined to rotate through them when writing example code:  

* `x := x + 1`
* `x += 1`
* `x++`

And that's why I write things differently between examples.  
It's not because I'm being inconsistant. It's because I'm showing you other ways of writing code.  
(FYI, I almost exclusively use `[]` and `{}` over `Array()` and `Object()`.)

One last thing to mention: At the end of this guide is a section about my future plans with AHK.  
I want to start doing this kind of stuff. More. A lot more.  
I have content ideas, and lots of them.  
And I want to start creating them regularly.  
Because of that, I finally set up a Ko-fi account and am accepting any support that wants to be provided.  
In short, I'm not going to charge for my content. I think everyone who wants to learn should have an opportunity.  
But if you do have money to spare and you want to help support the cause, this is how you can do it.  
I have no expectations, but the more support there is, the more content will come, and the faster it will be produced.  

In a truly amazing and ideal world, there'd be enough people wanting to learn about AHK that I could make it my job.  
I'm allowed to dream, right?  

That being said, go grab yourself a tea/coffee/beer/energy drink/whatever beverage you like.  
Maybe grab a snack, too?  
Use the bathroom, let the dog out, put the phone on silent, and play some quiet music you like.  

I sure hope everyone reading this gets a ton out of it.  

Let's start with something that'll make your coding experience and quality of life better.  

*Use the best text editor for the job!*

# Get the best AHK v2 editor and make your life easier

Before hopping into the guide, I want to make sure people understand that using a great editor can make coding in a language infinitely easier.  

For AutoHotkey v2, the current gold standard for code writing is VS Code with the AutoHotkey v2 Support Add-on installed.  
Bonus: I have a personally written an enhancement to that add-on that I'll be including with this.

Reasons why you want to use VS Code and this add-on:

* Calltips show up and give information about almost everything.
* Function/method parameters are always shown along with what type of data they expect.
* Return values are documented.
* All built-in vars are included with descriptions.
* Variable names are tracked. When typing, they show up in auto-complete.
* The autocomplete keeps scope in mind and won't suggest things you don't have access to.
* Errors are highlighted and a reason is displayed without the code ever needing to be ran. (Like spell checking for word docs.)
  * The amount of errors it will detect is incredible.
* Code is highlighted in different colors and styles depending on the context of the code.  
  * e.g. Variables are one color, operators are another, functions are another, built-in variables might be bolded or italicized
  * This all makes for MUCH easier code to read and eventually acts as a passive troubleshooter as you become accustomed to what colors and styles everything should have.
* This is a very small set of reasons and I could quite literally write an entire GroggyGuide on this topic.  

This add-on is so good that I actually rewrote the entire definition file for it (the thing that provides info to the calltips) over a period of almost a year and then provided it to the community free of charge so it can amplify their AHK coding experience.  

I could honestly do an entire GroggyGuide on VS Code and this addon.  
It's so feature rich and if you never want to mess with the features, you don't have to.  
Please, give it an honest shot.  
Write a few scripts with it.  
If you don't like it, you can uninstall it.  
You're out no money because everything is free.  
VS Code: Free  
THQBY AHK v2 Addon: Free  
My enhancement update: Free  

Here are links to for everything:

* Download VS Code (Free):  
  https://code.visualstudio.com/download  
  You want the `x64 system installer`.

* Download AHK v2 Support Add-on by THQBY (Free):  
  https://marketplace.visualstudio.com/items?itemName=thqby.vscode-autohotkey2-lsp  
  Or, use the [extensions pane of VS Code](https://i.imgur.com/tITgSnx.png).

* Download the Add-on Enhancement File by GroggyOtter (Free):  
  https://github.com/GroggyOtter/ahkv2_definition_rewrite  
  Yes, the enhancement file was completely written by me and adds in a TON of information to THQBY's add-on.  
  This includes most info found in the docs with better explanations added, all options included, hyperlinks to stuff, and example code in a lot of the examples.  
  This will make your coding life even easier and you'll find yourself alt+tabbing to the docs far less.  
  Lots of extra "auto-complete" features. For example, when using Send(), it will provide auto-completes for any key.

Get those installed and we can start talking about AHK.

# Expressions and Boolean

After a bunch of reordering and debate, I decided expressions were the place to start.  
It's difficult to talk about expressions without also involving Boolean logic, too.  
We'll cover both.

Expressions are a core part of programming and understanding them better means understanding AHK better.  
The term "expression" is a term you'll hear plenty in this guide, yet it seems many have a hard time defining exactly what an expression is.  
For the longest time, I thought of an expression as "something that can be defined on 1 line".  
To a certain extent, this was actually true. However, it was true because it's a byproduct of *being* an expression. It's not what *makes* it an expression.  

In my more educated years, I'd define an expression as:  
"Any code statement made of operators and operands that can be evaluated down to a single 'thing'."  

When working with expressions, we use expression syntax.  
If you're familiar with v1, you'll know it as the syntax used when `%` comes at the beginning of the line.  
When v2 got started, that v1 "dual syntax" crap was one of the first things removed.  
v2 deals exclusively in expressions so let's cover expression syntax:

* Strings must always be inside quotes.  
    Single or double quotes can be used as long as it's a matching set.  
  
      str1 := 'Hello'
      str2 := "World"
      MsgBox(str1 ' ' str2)
  
* Pure numbers are not quoted.  
    Numbers *can* be quoted, but that would be a string character, not a pure number.  
    On the flipside of that, AHK can do math with string numbers b/c it will attempt to convert it first.
  
      num := 17     ; Integer
      pi := 3.1415  ; Float
      str := '22'   ; String (not a number)
      MsgBox(num + pi + str)

* Variables, functions, classes, etc. are referred to by [name](https://www.autohotkey.com/docs/v2/Concepts.htm#names).  
    A name is an identifier in AHK that follow a set of rules.  
    Such as names must be unique or names cannot include quotation marks or many other symbols.  
    In fact, the only "symbol" from the ASCII standard that can be used in a name is the underscore `_`.  
    
    Do not quote a name. You're making a string.
    
      num1 := 7
      num2 := num1
      MsgBox()

You can use expressions to do math things with numbers or bits.  
You can use expressions to do text things with strings, such as appending, taking parts out, matching, substringing, replacing, and more.  

Expressions are based around "operands" and "operators" and they make up a large chunk of our code.  
Operands are the data.  
Operators are the symbols that make the operands do stuff.  

    ; The assignment operator is a binary operator, requiring two operands
    ; It assigns the operand on the right to the operand on the left
    ; 
    ; operand     operand
    ;    ↓           ↓
    my_variable := 100000
    ;           ↑
    ;        operator

To be clear, operator and operand are technical terms.  
You're not going to hear them in normal conversation.  
The above example is "a number being assigned to a variable".  
Not "The assignment opearator is assigning the number operand to the variable operand".  
No one talks like that.  
Use the technical terms when you need to reference the parts. Like when explaining a problem.  
Or when you're writing a GroggyGuide and want to teach people technical terms.  

When we talk about operators, we're talking about symbols like `+`, `-`, `:=`, `x.y`, `is`, `++`, `?:` and many others.  
Everyting in the following list is considered an expression.

    x := 2                              ; Assignments
    1 * 2 - x + 6 / 2                   ; Math operations
    x++                                 ; Incrementation
    (2 >> 1) ^ 1                        ; Bitwise operations
    y ? x := 5 : x := 10                ; Ternary choices
    x := x x . ' ' . x x                ; String concatenation
    (y := x + 1, x += y * 2)            ; Multi-statements
    (x is Integer)                      ; Type checking
    (num) => num * num                  ; Fat arrow functions
    x := 6 / 3 + (x is float ? 2 : 4)   ; Any combination of operators

All of those expressions evaluate down to a single "thing".  
Expressions can also be large and complex, like this one:

    ; This is a single expression
    x := Mod(12, 5) * 5 + ((y := 1 + 1) ** (z := 7 - 2)) + (z > y ? 0 : 100)
    
    ; View the results of that expression
    MsgBox(x '`n' y '`n' z)

Later in the sub-expression section, we will break down that entire expression, step-by-step.  
You'll be able to explain exactly how that expression evaluated down to the variable `x` and why it contains the number `42`.  

Remember that an expression has to evaluate down to a single thing.  
If you do the math, the expression evaluates to `42` at one point, but the final step is assigning that value to `x`.  
What is left is a reference to the variable `x` which happens to be storing the number `42.  

For those who disagree that `x` is what is left, here's some simple code that proves it.

    ; y is assigned 1 and what is left is a reference to y
    ; The ++ operator adds 1 to whatever is left from the sub-expression
    ; (We'll learn about sub-expressions in a bit)
    (y := 1)++
    
    ; If MsgBox shows 2, then the ++ was applied to y.
    ; If MsgBox shows 1, then I'm wrong (PS - I'm not wrong)
    ; MsgBox shows 2
    ; If (y:=1) didn't resolve to y, then ++ wouldn't have incremented it.
    MsgBox(y)

Expressions are about having a way to "express" the steps you want taken.  
Whether it be addition, multiplication, assignment, function calls, bit shifting, or any other opearting you want performed.  

    price := 12.99          ; Expression to assign a price to the price var
    tax := 1.05             ; Expression to assign a sales tax to the tax var
    total := price * tax    ; Expression to calculate and assign the total cost using tax and price

## What things are *not* expressions

It might seem like expressions make up the entire language, but there are plenty of things in AHK that aren't expressions.  
Or, rather, you're not able to use them with expressions.  
Things like:

* **Control flow statements**  
  `if`, `else`, `return`, `loop`, `for`, `switch`

* **Directives**  
  `#Hotif`, `#Warn`, `#Requires`, `;@Ahk2Exe-AddResource`, `;@Ahk2Exe-Base`

* **Function definitions**  
  
      my_func() {
          ; Code
      }

* **Hotkeys/hotstrings declarations (a special kind of function definition)**  

      *F1::MsgBox('hi')


None of the above can be used inside of an expression.  
You can't dereference `#HotIf`.  
You can't multiply a function definition.  
You can't assign an array to `loop`.  
And it's impossible to bit shift a function definition.  

Expressions are all about operators and operands; symbols and data.  

## Operator arities: Unary, binary, and ternary

Earlier in the expressions section, I mentioned assignment being a "binary opeartor".

> ; The assignment operator is a binary operator, requiring two operands  
> ; It assigns the operand on the right to the operand on the left  

Operators come in three different types, or "arities".  
An "arity" can be defined as the number of operands an opeartor requires to work.  
The term "arity" is actually seen in all these words, as the suffix "ary" is derived from "arity".  
The prefix to each term is a number and the suffix is "required parameters".  

* `Unary`  
  Un: Latin for "unus", meaning one.  
  "One required operand".
* `Binary`  
  Bi: Latin "bi", derived from "di", meaning two.  
  "Two required operands".
* `Ternary`  
  Tern: Latin "ternarius" or consisting of three, from "terni" or three each.  
  "Three required operands".

Examples:  

The assignment operator `:=` is "binary" because on the right, it requires a value to assign and on the left it required a value to assign to.

    assign_to := 'Some Value'
    MsgBox(assign_to)

The subtraction operator `-` is also binary because it requires one number to subtract from another number.

    num1 := 11
    num2 := 7
    MsgBox(num1 - num2)

The NOT `!` operator is unary. It requires a single operand.  
Whatever the opearand evaluates to (true/false), the opeartor returns the opposite of that.  
In this case, x is false, so `!x` would evaluate to true.  
"NOT false" or "opposite of false".

    x := 0
    MsgBox(!x)

Negation, also known as unary minus `-`, is another unary operator.  
When this is fixed to the front of a variable, it negates the value, turning a positive value negative and a negative value positive.  
This is the same symbol used for subtraction, however subtraction is binary.  

    x := 10         ; Set to 10
    MsgBox(-x)      ; Negated means it -10 is used
    
    y := 5 - -x     ; 5 - -10 (five minus negative 10)
    MsgBox(y)       ; Shows 15

Finally, there is the one and only ternary operator.  
It requires 3 operands.  
And while it is considered a single operator, it requires the use of two symbols:

    true_or_false := 0
    MsgBox(true_or_false ? 'True result' : 'False result')
    
    true_or_false := 1
    MsgBox(true_or_false ? 'True result' : 'False result')

We're not going into detail about ternary because there's an entire section dedicated to it later on.

## Operator prescedence

We can't discuss operators and not discuss the fact they have an order of execution, or "precedence" level. 

There are a lot of operators in AHK. There has to be in order to do all the different stuff AHK does.  
The docs supply a [full list of AHK operators](https://www.autohotkey.com/docs/v2/Variables.htm#Operators).  

I've also created a [table of operators and their precedence levels](#operator-precedence-list).  
This catalogs every operator, gives a brief description of what it does, and includes a numerical representation of each symbols precedence level (highest number has highest precedence).  zzzzzz


I encourage everyone to go read through all of those operators.  
You don't have to understand everything you read or how to use all of them, but you're exposing yourself to each operator.  
You're learning "this does this" and "that does that".  
Some may look familiar, like: `:=` and `+`  
Some might look weird, like: `()=>` and `?:`  
Those weird looking operators, the fat arrow `()=>` and ternary operato `?:`, each have their own sections later.  
Having a first-time expreience now means when you encounter these symbols later in the docs or in an example, you at least have an idea of what they do and it's easier to learn about them.

### Order of operations, kind of like PEMDAS
Operator precedence in programming is the same as PEMDAS in school (or BODMAS / BOMDAS / BEDMAS / BIDMAS depending on where you grew up).  
Regardless, it's the agreed upon order in which everyone does math.  
It's logical, it's practical, and it gives everyone the same standard to go off of.  

1. **Parentheses**  
   Always do things inside of parentheses first.  
   Parentheses are KING.
2. **Exponents**  
   When dealing with math operations, exponentiation (powers) are always done first.
3. **Multiplication/Division**  
   Multiplication and division are done next.  
   One is not higher than the other, so they're evaluated left to right.
4. **Addition/Subtraction**  
   The last math operation we do is addition/subtraction.  
   Again, neither is higher than the other. They're evaluated left to right.

Imagine someone gave you this equation: `2 + 2 * 5 + 5`  
But they didn't tell you what order of operations are expected.  
Which answer is the correct answer?

1. `25` - Evaluated left-to-right
2. `22` - Evaluated right to left
3. `40` - Evaluated addition first, then multiplication
4. `17` - Evaluated multiplicaiton first, then addition

Without a defined order or way of doing math, we would need to be told what the proper order of operations is.  
If they expect left to right, the answer is `25`.  
But if addition should be done first and then subtraction, the answer is `40`.  
Humans understood a **LONG** time ago that there needed to be a standard.  
And that's where PEMDAS came from.  
Now if you ask 100 different people from around the world to solve `2 + 2 * 5 + 5`, you'll consistently get `17` because we all follow the same order of operations when doing math.

AHK's operators follow the same ideology.  
Each one has it's own "level" and the expression will ALWAYS be evaluated in the same order.  
Double derefs are the highest priority: `%var%`  
When an expression is evaluated, that's the first thing it looks for and if it finds it, it evaluates it.  
If there are no double derefs, it checks the next symbol in the list, member access: `x.y`  
If it finds member access, it resolves.  
Then it goes to the next opeartor on the list.  
And it goes down the entire list, doing things in the same order EVERY SINGLE TIME.  

If an operator has the same precedence level, it does exactly like PEMDAS: Evaluate left to right.  

Following the same order each time, we get the reliable and consistent answers that never change.  
This is what "precedence" is. The order in which the operators are evaluated!  

Some code examples would be really helpful, so let's make some.

    x := 4 + 2 * 2 ** 4

This is an expression because it evaluates down to one value.  
Let's see how AHK evaluates it.  
If we check the list of operators, `**` is the first one we find.  
That means it must be evaluated first.  
This makes sense because in PEMDAS, exponents come before multiplication and addition, too.

    x := 4 + 2 * 2 ** 4
    ; Becomes
    x := 4 + 2 * 16

There are no more exponent symbols now.  
Going down the list (and past many opeators not in use in this expression) we come across `*`.  
This is higher than `+` and `:=`, so it must be done next:

    x := 4 + 2 * 16
    ; Becomes
    x := 4 + 32

Between addition `+` and assignment `:=`, addition is higher.  
So it must be done next.  

    x := 4 + 32
    ; Becomes
    x := 36

The final step of the expression is to assign the number `36` to the variable `x`.

    x := 36
    ; Becomes
    x

All we're left with is the variable `x`, which now contains the number `36`.  
This is why we have precedence levels. To ensure things are done in order.  

Think about that last operator choice. You didn't need to look up if `+` or `:=` is higher, because common sense will **tell you** which is higher.  
If you would've done assignment first, you would've assigned 32 to x.  
Then you would've added 32+4, which would turn into 36, and then it would be immediately deleted because the assignment part was already done.  
It's common sense that assignment must have a very LOW precedence level or you'd be assigning math statements before the math has finished.  

We can expand on that by thinking about math.  
You can't do math without the numbers you need, right?  
So when you see `x.y + 5`, it makes sense that `x.y` needs to resolve to something before 5 can be added to it.  
You can't add `5` to `x.y`. It's not a number. It's meaningless *until* it evaluates to a number.  
This is why `x.y` has such a HIGH precedence level.  
And what if we had `x.%y% + 5`?  
`%y%` has to resolve to *something* so that `x.something` can resolve to a number so 5 can be added to it.  
And that's why `%var%` has a higher level than `x.y`.  

Yes, I realize you might not understand what these mean.  
`x.y` is member access or getting the value stored in y from the object named x.  
`%var%` is a double deref and it resolves whatever is in var as the actual variable name.  
We'll learn more about both of these operators later in the guide.

The point is that every single operator's precedence level is at that level *for a good reason*.  
And precedence is not "level of importance".  
It's the logical order to make things work correctly.  
The assignment operator `:=` is EXTREMELY important but has one of the lowest precedence levels.  

#### Sub-expressions outrank operators

It's impossible to talk about operator pecedence without talking about sub-expressions.  
If you look at the page that lists all the operators and scroll down past them, there's a secondary section below it that reads:

> The following types of sub-expressions override precedence/order of evaluation:

What does the P in PEMDAS represent?  
It's parentheses, right?  
When reading through the operator list, did you ever see "parentheses" listed?  
They should've been the first thing on the list. Even before double deref, which has the highest precedence of any operator.  

The trick here is that parentheses are not operators and that's why they're not in the list.  
Instead, they're classified as a **sub-expression**.  
And like PEMDAS, sub-expressions in AHK are KING.  
No expression will ever be evaluated if a sub-expression exists.  
This is due to the hard rule that sub-expressions must ALWAYS be evaluated first. Just like in PEMDAS.  

So what are sub-expressions?  
It's in the name. It's an expression that resides inside of another expression.  

Just like in math class.  
Let's use our previous example from understanding PEMDAS.  
We understand and accept that multiplication comes before addition.  
But what if we NEED to do the addition first because it's part of how the equation works?  
It's **not wrong** to do addition before multiplication, but it **is wrong** to do addition before multiplication in a math problem. Get what i mean?  
So if we want to do addition first, we have to make that clear in our equation with the use of parentheses.  

    (2 + 2) * (5 + 5)

This gets us `40`, which is the correct answer we wanted.  
Parentheses **are** sub-expressions. Or in this case, sub-equations.  
They tell us "evaluate the stuff inside the parentheses first".  
You still follow order of operations inside those parentheses, but you do them first.  
And whatever resolves is what you use in the next step.

If you understandt his, you understand sub-expressions already.
Let's look at an example:

    ; This whole thing is an expression
    x := 2 ** (3 + (2 + 2))
    
    ; This part is a sub-expression of the main expression
    ;         |-----------|
    x := 2 ** (3 + (2 + 2))
    
    ; And this is a sub-expression within a sub-expression
    ;              |-----|
    x := 2 ** (3 + (2 + 2))

We follow the simple rule of "Evaluate all sub expressions first".  
    
    ; Can't evaluate expression as it has a sub-expression.  
    ; Evaluate sub-expression first.
    x := 2 ** (3 + (2 + 2))
    
    ; Can't evaluate sub-expression as it has a sub-expression.  
    ; Evaluate sub-expression first.
    (3 + (2 + 2))
    
    ; CAN evaluate sub-expression b/c there are NO MORE sub-expresions.  
    ; When evaluating, follow order of precedence.
    (2 + 2)
    ; Evaluates to
    4
    
    ; Insert 4 back into the previous sub-expression
    ; CAN evaluate sub-expression b/c there are NO MORE sub-expresions.  
    (3 + 4)
    ; Evaluates to
    7
    
    ; Insert 7 back into the previous expression
    ; CAN evaluate expression b/c there are NO MORE sub-expresions.  
    x := 2 ** 7
    ; Evaluates to
    x := 2 ** 7
    ; Evaluates to
    x := 128
    ; Evaluates to
    x

Every single expression follows this same order every single time.  

Parentheses are not the only sub-expression.  
There are four primary sub-expressions:  

* `()` = Parentheses
* `fn()` = Calling a function
* `x[y]` = Item access
* `{a:1, b:2}` = Object literal creation

Some of you might have immediately noticed that all 4 of these things are "enclosed" somehow.  
Meaning they all have "opening" and "closing" symbols.  
The stuff "between" the opening and closing is considered a sub-expression and must be evaluated.

* `(2 + 3 * 4)` = Evaluate inside parentheses
* `fn('hello' . 'world')` = Evaluate inside parentheses
* `x[some_item_name]` = Evaluate inside square barckets
* `{a:2 * 2, b:15 - 10}` = Evaluate inside curly braces

These are all sub-expressions and each must be fully evaluated before the rest of the expression can be evaluated.  

#### Sub-expressins do NOT have levels of precedence

When working with operators, there are precedence levels.  
And while sub-expressions are the highest ranked of all precedence levels, they do not have precedence levels amongst themeselves.  
This is simliar to how "multiplication/division" and "addition/subtraction" work.  
When something is equally ranked, we evaluate left-to-right.  
The same applies to sub-expressions. They're always evaluated left-to-right.



1. Go left to right and if a sub-expression is found, evaluate it to a single value.
2. If no sub-expressions are found, evaluate the expression following operator precedence.  

No matter how large or complex an expression, you can get through it by following these steps.  
Earlier, I said:

> Later in the sub-expression section, we will break down that entire expression step-by-step.  
> So you can see exactly how AHK process it.  

We're going to break down this expression now:

    x := Mod(12, 5) * 5 + ((y := 1 + 1) ** (z := 7 - 2)) + (z > y ? 0 : 100)

* Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.
    
       ;    |--------|
       x := Mod(12, 5) * 5 + ((y := 1 + 1) ** (z := 7 - 2)) + (z > y ? 0 : 100)

  * Evaluate the sub-expression.  
  * Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

        Mod(12, 5)

  * Step 2: If no sub-expressions are found, evaluate the expression following operator precedence.  
    
        Mod(12, 5)
        2

* Insert the sub-expression value back into the expression and continue with step 1.  
Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

      ;            |----------------------------|
      x := 2 * 5 + ((y := 1 + 1) ** (z := 7 - 2)) + (z > y ? 0 : 100)

  * Evaluate the sub-expression.  
    Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

        ;|----------|
        ((y := 1 + 1) ** (z := 7 - 2))

    * Evaluate the sub-expression.  
      Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

          (y := 1 + 1)

    * Step 2: If no sub-expressions are found, evaluate the expression following operator precedence.  

          y := 1 + 1
          y := 2
          y

  * Insert the value back into the sub-expression and continue with step 1.
    Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

        ;     |----------|
        (y ** (z := 7 - 2))

    * Evaluate the sub-expression.  
      Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

          (z := 7 - 2)

    * Step 2: If no sub-expressions are found, evaluate the expression following operator precedence.  

          z := 7 - 2
          z := 5
          z

  * Insert the value back into the sub-expression and continue with step 1.  
    Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

        (y ** z)

  * Step 2: If no sub-expressions are found, evaluate the expression following operator precedence.  

        y ** z   ; 2 ** 5
        32
    
* Insert the value back into the sub-expression and continue with step 1.  
  Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

      ;                 |---------------|
      x := 2 * 5 + 32 + (z > y ? 0 : 100)

  * Evaluate the sub-expression.  
    Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

        (z > y ? 0 : 100)

  * Step 2: If no sub-expressions are found, evaluate the expression following operator precedence.  

        z > y ? 0 : 100
        1 ? 0 : 100
        0

* Insert the value back into the sub-expression and continue with step 1.  
  Step 1: Go left to right and if a sub-expression is found, evaluate it to a single value.

      x := 2 * 5 + 32 + 0

* Step 2: If no sub-expressions are found, evaluate the expression following operator precedence.  

      x := 2 * 5 + 32 + 0
      x := 10 + 32 + 0
      x := 42
      x

After evaluating that entire expression, you're left with a reference to `x` which contains the number `42`.  
There are also the `y` and `z` variables that were assigned during the evaluation process.  

Or if you'd like a cascading view of each step, uninterrupted by my ramblings:

    x := Mod(12, 5) * 5 + ((y := 1 + 1) ** (z := 7 - 2)) + (z > y ? 0 : 100)
    ;    ↓‾‾‾‾‾‾‾‾‾
    x := 2 * 5 + ((y := 1 + 1) ** (z := 7 - 2)) + (z > y ? 0 : 100)
    ;                   ↓‾‾‾‾
    x := 2 * 5 + ((y := 2) ** (z := 7 - 2)) + (z > y ? 0 : 100)
    ;             ↓‾‾‾‾‾‾‾
    x := 2 * 5 + (y ** (z := 7 - 2)) + (z > y ? 0 : 100)
    ;                        ↓‾‾‾‾
    x := 2 * 5 + (y ** (z := 5)) + (z > y ? 0 : 100)
    ;                  ↓‾‾‾‾‾‾‾
    x := 2 * 5 + (y ** z) + (z > y ? 0 : 100)
    ;            ↓‾‾‾‾‾‾‾
    x := 2 * 5 + 32 + (z > y ? 0 : 100)
    ;                  ↓‾‾‾‾
    x := 2 * 5 + 32 + (1 ? 0 : 100)
    ;                 ↓‾‾‾‾‾‾‾‾‾‾‾‾
    x := 2 * 5 + 32 + 0
    ;    ↓‾‾‾‾
    x := 10 + 32 + 0
    ;    ↓‾‾‾‾‾‾
    x := 42 + 0
    ;    ↓‾‾‾‾‾
    x := 42
    ;‾‾‾‾‾‾
    x

AHK processes every single expression in the same way.  
Evaluate all sub-expressions left to right > evaluate the remaining expression > repeat  
Same rules.  
Same steps each time.  
Same expected behavior.  
Same consistent and reliable results.  

### A simple way to ensure order

Order of operations and sub-expressions do not need to be daunting topics or seem complicated.  
You undertand that there's an order things are done.  
And the complexity of expressions is only as deep as you want to write it.  
You don't have to deal with precedence at all if you don't want to.  
Use simple expressions in the order you want them to happen:  
You're not really expected to memorize the whole list.  

When we write this expression:

    x := 2 ** (3 + (2 + 2))

We're using parentheses to do 3 things in a specific order.  
If you're uncomfortable writing code like this, there is nothing wrong with you breaking it down to multiple lines:

    step1 := 2 + 2
    step2 := 3 + step1
    answer := 2 * step2

Do whichever makes sense for you.  

Plus, these are just examples from some random dude trying to teach some other people about AutoHotkey.  
We're using examples that aren't exactly meaningful.  
But when you're writing your own code, moving windows around, dealing with mouse positions, trying to calculate something with file sizes, or whatever scenario you're in, the expressions you use will make MUCH more sense than me saying `(3 + (2 + 2))` does.  

### Recap of operator precedence

The big thing to recap is make sure that you remember sub-expressions always happen first.  
Sweep left-to-right, eliminate each sub-expression as you encounter it by evaluating it down to a single value.  
This applies recursively to each 


Parentheses, function calls, item resolving and 


Let's do a quick recap of how an expression is evaluated using precedence and sub-expressions.

1. The expression is first checked left-to-right for any sub-expressions.  
   Remember that sub-expressions are all equals. None are done before any others.  
2. If a sub-expression is found, that sub-expression must be evaluated first.  
   That section needs to be evaluated, so 
3. If no sub-expression is found, the expression is evaluated using operator precedence.


## Boolean logic, true/false, and decision making

We've talked a lot about "evaluation", but it was almost exclusively math related. As in `2 + 2` is `4`.    
However, I specificially included the "greater than" `>` comparison operator in the last section:  

    ; Specificlaly this part
    (z > y ? 0 : 100)

    ; And I showed that it evaluated to
    (1 ? 0 : 100)

We don't care about the ternary part `?:` because it gets its own section later.  
`z` was set to 5 and `y` was set to 2.  
So why does `5 > 2` results in a 1.  

This is true/false at work. More specifically, it's Boolean logic at work.  

In computer programming, everything has a Boolean value.  
Everything in a language is defined as either being true or false, with very few things being false.  
The number zero `0` is almost universally acknowledged as false.  

In C, `0` is the *only* false value by default.  
More false values can be defined, but `0` is the only one you begin with.  
This is covered in every tutorial, book, or course you'll ever take on C.  

Meanwhile, JavaScript has six different false values (excluding number variations).  
[MDN documents these values here](https://developer.mozilla.org/en-US/docs/Glossary/Falsy).  

1. `false`
2. `0` / `-0` / `0n` (zero variations)
3. `""` / `''` (empty string)
4. `null`
5. `undefined`
6. `NaN`

As for AutoHotkey?  
It only has **two** false values:  
* `0`: The **number** zero
* `''` / `""`:  An empty, or blank, **string**

Everything else in AHK is considered true.  
Objects, arrays, any positive or negative number, any string that isn't empty...they're all true.  

However, we need to address a caveat to the rule.  
Lexikos made a decision that some people disagree with.  
False is specifically defined as "the **number** zero or an empty (blank) **string**".  
The catch comes from the fact that AHK will evaluate number strings as numbers.  

    num := '30'             ; Starts as a string containing 30
    num += 12               ; Adding 12 to it converts it to a number
    MsgBox(
        'Type: ' Type(num)  ; Type is now integer
        '`nnum: ' num       ; Value is now 42
    )

Part of the "user-friendliness" of AHK is that it converts between string and number when needed.  
What happens when you give it a string containing the ***character*** zero `"0"`?  

    str := '0'
    if str
        MsgBox('True!')
    else MsgBox('False!')

By definition, this *should* be true because it's a string that isn't empty, yet "false" is what pops up.  
This is because AHK evaluates the string, sees it as a zero, and converts it to a zero.  
Therein lies the problem.  
We have something that started true (a non-empty **string**) and ended up false (the **number** zero).  

This applies to hex numbers, too.  
A string containing `'0x0'` will also evaluate false because AHK sees a valid hex value and converts it.  

This has been brought up and Lexikos has addressed it stating that it'll remain this way for now.  
It's an edge case, but it's still one you should know about.  
And it does show up in the [v1.1 to v2.0 changelog](https://www.autohotkey.com/docs/v2/v2-changes.htm).

> Quoted literal strings and strings produced by concatenating with quoted literal strings are no longer unconditionally considered non-numeric. Instead, they are treated the same as strings stored in variables or returned from functions. This has the following implications:  
> * Quoted literal `"0"` is considered false.
> * `("0xA") + 1` and `("0x" Chr(65)) + 1` produce `11` instead of failing.
> * `x[y:="0"]` and `x["0"]` now behave the same.

If you wanted to implement a more accurate true/false evaluation, you could use a function like this:

    str := '0'
    if is_true(str)
        MsgBox('True!')
    else MsgBox('False!')
    
    is_true(value) {
        if (value is String && StrLen(value) = 0)
            return 0
        if (value is Number && value = 0)
            return 0
        return 1
    }

So let's define false as it should be in AHK:

* Numbers with a value of zero
    * `0`
    * `0.0`
    * `-0`
    * `0x0`
* Empty strings
    * `''`
    * `""`
* Strings containing a valid 0 number
    * `'0'`
    * `"0.0"`
    * `'-0'`
    * `"0x0"`

### Evaluating boolean

So how is Boolean used in a computer?  
Boolean logic isn't about the value of a number or the contents of a string.  
It's about expressions, comparisons, and things that sepcifically evaluate to a truth or a falsity.  
We use Boolean when comparing numbers `1 = 1`, comparing strings `'ahk' = 'ahk'`, checking for equalities or inequalities `x != y`, checking if numbers are greater than or less than each other `a <= b`, and ultimately we're producing a result of either `1` (true) or `0` (false) to show if the comparison was true or false.  

These comparisons are used with things like `if/else` statements or `while` loops.  
Take `if/else` as an example:

    if (1 = 1)      ; One IS equal to one. This is a truthy statement.
        do_this()   ;   This code runs because the expression was true.
    else            ; Else runs when a statement is falsy
        do_that()   ;   And this other code would then run

Boolean used to make a choice: "If true, do this, else do that"  
`While-loops` also rely on a true or false statement:

    x := 1              ; x is set to 1
    while (x < 10) {    ; While "x is less than 10" is true, keep looping
        do_stuff()      ;   Run some code
        x++             ;   Increment x by 1
    }
    ; x goes up by 1 each time.
    ; Eventually x will not be less than 10
    ; When x IS 10, it's no longer less.
    ; The statement is false and the while-loop breaks, ceasing the loop
    
The while-loop structure is saying "Keep looping while this thing is true."  

AHK has a [`true` and a `false`](https://www.autohotkey.com/docs/v2/Variables.htm#TrueFalse) built-in variable.  

    ; Run this and it'll show what's in 'true' and 'false'
    MsgBox(
        'true: Type = ' Type(true) ' , Value = ' true 
        '`nfalse: Type = ' Type(false) ' , Value = ' false 
    )

But unlike other languages, like JavaScript, true and false are not their own data type.  
In JavaScript, true and false belong to the `Boolean` primitive type.  
It's not a string. It's not a number. It's not an object. It is its own primitive type and it only contains two values: `true` and `false`

In AHK, true and false are indicated by the integers 1 and 0, respectively.

### Fun with true and false

A little fun with the `true` and `false` variables.  
I've got two tests for you.  

1. We know true is `1` and false is `0`.  
Can you come up with the answer to the universe using only truth?  
The solution is in the truth:

       <link to code>

       ; True is worth one, so add and multiply to your hearts content:
       two := true + true
       three := two + true
       seven := two * three + true
       MsgBox("Answer to the universe: " seven * two * three)
    
2. Knowing that false is `0`, can you come up with a way to crash a script using `false`?  

       true / false

    Why does it throw an error?  
    The error it throws tells you if you'd run the code!  
    Caught ya! You're not running my examples!

    The reason it crashes is because you cannot divide by zero.  
    False is the number 0.  
    The true part is irrelevant, it just looks neat written that way.  
    It could be any number and the error will still happen.

### Making a toggle using Boolean values

In programming, the concept of a toggle is like a toggle switch in real life.  
A light switch is a toggle switch. There's on and there's off.  
In programming, a variable is a toggle when it's used to control something by acting as the on (true) and off (false) switch.  

Let's make a toggle.  
Pressing F1 should cause the toggle to happen, switching between on and off.  

Try it out:

    *F1::{
        my_toggle()                                     ; Make a hotkey and assign a function to it
    }
    
    my_toggle() {
        static toggle := 'Hello'                        ; Create a permanent variable starting as hello
        
        MsgBox('Toggle is currently set to: ' toggle)   ; Announce state before toggling
        toggle := !toggle                               ; Toggle: Assign to toggle the opposite of toggle. true <-> false
        MsgBox('And after toggling: ' toggle)           ; Show after toggle status
        
        if (toggle)                                     ; Use toggle. If toggle is set to true
            do_true_stuff()                             ;   run this code
        else                                            ; Else it must be false
            do_false_stuff()                            ;   so run this other code
        return                                          ; end of function
        
        do_true_stuff() {                               ; Function with true code
            MsgBox('Running true code')
        }
        
        do_false_stuff() {                              ; Function with false code
            MsgBox('Running false code')
        }
    }

Notice that the toggle variable starts off as `hello`, which is considered true. It's a string that's not empty.  
Then we'll see the NOT operator in action `!`. This is called bit-wise not and bit-wise operators are used with Boolean statements.  
Bit-wise NOT inverts something between its true and false state.  
'Hello' is true. Flipping it to false means setting it to `0`, which is what AHK considers false.  
So yes, it went from a string to an integer and that's because AHK will always define false as the integer `0` and true as the integer `1`.  
The next time the toggle flips, it'll change from false `0` to true `1`. 

    The stored value inside toggle:   'Hello' > 0     > 1    > 0     > 1
    The boolean evaluation of toggle:  True   > False > True > False > True

And speaking of expressions, you'll eventually learn to make use of all the different operators to reduce code down to something like this:

    *F1::my_toggle()
    
    my_toggle{
        static toggle := 'Hello'
        (toggle := !toggle) ? do_true_stuff() : do_false_stuff()
        do_true_stuff() => MsgBox('Running true code')
        do_false_stuff() => MsgBox('Running false code')
    }

# Functions  

Functions are a fundamental part of any modern programming language, AHK included.  
They allow us to create "chunks of code" that serve some purpose or *function*. Hence the name.  

Whenever you're writing any code that's supposed to execute, it should be inside a function or inside a class.  
There's no reason to write code in global space.  

## Scope and global space

One of the big benefits to functions is that they provide `scope`.  
To understand scope, we have to understand what global space is.  
What does "global" mean?  

Global means something is declared in the "main" area of the script.  
If something is "global" it means **everything** in the script can see it and access it.  
All of the built-in vars and functions AHK provides are global. They need to be.  

If you create a new script and start writing code, you're coding in global space.  
It's the main area of the script.  

    x := 1                  ; Global code
    y := x + x              ; This does not belong to anything
    while (y < 10) {        ; It is in global space
        x *= 2              ; Don't do this
        MsgBox(x)           ; We don't code in global space
        y++                 ; It's not necessary
    }                       ; And we don't make global variables

We don't code in global space. It's a bad coding practice.  
You *can* do it but you *shouldn't* do it.  
Instead, we'd define a function or class and then write our code in that.  

    my_func()               ; Calling the function so it will execute its code

    my_func() {             ; my_func() is global and can be called from anywhere. this is a good thing.
        x := 1              ; Everything inside the function is private. This is also good.
        y := x + x          ; <- These are the functions own private x and y variables.  
        while (y < 10) {    ; They are not the same as the x and y variables in global space.
            x *= 2          ; Every function can have an x and y variable and they will never mess with each other.
            MsgBox(x)       ; Everything in this function is "out of scope" to everything else.  
            y++             ; Everything in global space is "in scope" for a funciton (and everything else).  
        }                   ; Everything in another function is "out of scope" for this function.  
    }                       ; End of function. Global code being after this curly brace.

So what kind of things ***should*** got in global space?

* Directives  
  Things that direct the AHK on how to behave.  
  These start with a `#`, like `#HotIf` and `#Requires`.  
* Function definitions  
  The very purpose of a function is to store code.  
  We can then bind the function to a hotkey, GUI control, or other something else to "activate" the code.  
* Hotkey/hotstring definitions  
  These are a special type of function definition that creates a key listener.  
  You're technically making a function and then binding it to the listener.  
  When the key listener detects that you pressed that key or key combo, it activates the associated function code.
* Class definitions  
  Class are special objects used to organize variables and functions into a single usable entity called a class.  
  There's an entire sections on classes later.

### The unwritten rule of global space

There's a common piece of advice you'll see in almost every programming guide/class/tutorial you'll encounter.  

**Put as few things in global space as possible.**

No programming language really has a hard rule on how many things you can have in global space, but it's generally accepted the fewer, the better.  
This also ties in with "don't use global variables", as you're adding more and more things to "the global namespace", or in other words "the list of all names available in global space".

Functions help us reduce the amount of things declared in global space by grouping up like-variables and code.  
They can even contain nested functions, or functions defined in functions, reducing code more.  
Classes are even better at reducing items in global space as they bundle many variables and funcions together into a single named entity.  
Eventually, you'll realize that you can do almost everything you want with classes and when used correctly, global variables and global code are never needed.

### Functions and scope

Now that we understand global space, we can talk about scope.  
When we talk about the fact that things inside of functions are private from things in global space, that's scope.  

Why do we call it scope?  
Because we talk about variables as though we can "see" them, similar to how you'd see something in a telescope or a rifle scope.  
A global variable can be seen by everything in the script. It is "in scope" of everything.  
Variables inside of a function are only "in scope" of the things inside the function.  
Nothing on the outside can "see inside" the function, so that code and those variables are "out of scope".  

The function's name is defined in global space, so it's in scope of everything, meaning the function can be called, or used, by anything.  
That's not the same as its internal code being accessible, because it's not. It's out of scope.  

A huge benefit to this that common variable names, like `str`, `txt`, `num`, `arr`, `var`, `obj`, `name`, `count`, `i` and more can all be used freely within every single function and they will never interfer with each other.  
Each function is its own little environment and gets to have its own set of variable names and code.  

That's programming! You make functions that do the things you want them to do, and you break it down into as many functions as you need to do the job.  

We can go deeper with scope when it coems to neseted functions, however there's an entire section of that later on.  
It's also hard to define scope when there are two kind of neseted functions and how they're defined makes a difference specifically in their scope.  
We'll discuss that when we get to it.

### Logical organization, abstraction, and meaningful names

Putting stuff in a function is just plain logical.  
Every time you write code, you're writing it to do *something*, or else you wouldn't be writing code.  
Take that code, put it in a function, and name your function something that accurately describes what it does.  
It doesn't have to be a massive, highly descriptive name, but it should easily convey the purpose of the function.  
Giving your functions meaningful names will help your code describe itself, making it easier to understand what the code is doing without resorting to using comments.  

> "Code is like a joke. If you have to sit down and explain it to someone, it's not good."

If you have a function that gets all the names from a file, `get_names()` or `get_names_from_file()` would both be good names.  
They describe exactly what they do.  
Do you have a script that can toggle a window's ability to be "always on top"? How about `aot_toggle()` or `always_on_top_toggle()`?

This is also how abstraction works.  
You have multiple lines of code that run and they do just what we described: `get_names()` or `aot_toggle()`  
Any time you want to do one of those actions, you call that function.  
You don't think "I need to get the file into a variable and then loop through it and then..."  
No, you just think to call `get_names()` and the function returns the names, just like you want.  
You're abstracting away all the steps that go into getting those names into a single thing called `get_names`.  

We'll talk more about abstraction later.  

### Global variables - don't use them

So we talked about trying to minmize things in global space.  
But let's talk about global variables.

Any variable declared in global space is called a "global variable".  
It's a variable that's in scope for EVERYTHING.  
Meaning any piece of code anywhere in the script can read and alter that variable.  

> "Global variables sound great! That way everything can get us it."

No!  
That is exactly why they're **not great**.  
I advise people to never use them because they're never needed.  
Global variables are what I call a "bad coding habit".  
A bad coding habit is something you **can** do but you **shouldn't** do because it can cause problems or difficulties in some way.  
Anything you can do with a global variable, you can (and should) do with a function or a class.  
Functions can store data in static variables.  
Classes can store data in properties.  
We'll be discussing both in this guide.  

> "Can you explain why globals variables are so bad?"

I would be happy to.

For one reason, it creates code that does not play well with other code.  
If you write some code containing a global called `id` and then Bob imports your code into his script and HE has a global called `id`, AHK isn't going to tell you about it.  
Now your code had a big problem and you don't have eyes on it.  
Maybe it breaks the code. Maybe it causes odd behavior.  
The point is, it was caused by the use of global variable.

> "I don't get how that's different from using a function or a class"  

Run this code that has the same global variables defined twice:

    my_global := ['a', 'b', 'c']    ; a global var from a script
    
    my_global := 'A string'         ; a global var from your code
    
    MsgBox(my_global[1])            ; Error. This was supposed to be an array.

In the example above, what if they were both supposed to be strings?  
Now you're not even getting a error due to misusing it.  
If your var gets set to 0 but the other one is expecting a 1, you got problems now and AHK won't tell you about it.  

Now run this code with two functions.
    
    ; Spoiler: This will throw an error every time
    my_func() {
        return []
    }
    
    my_func() {
        return 'A string'
    }

You can't accidentally declare two functions with the same names. AHK doesn't allow it.  
You also can't have two classes with the same name.  
That's why I always tell people "if you have a value that needs to be stored, put it in a function or a class."  

These scenarios are hypothetical, but they demonstrate the potential.  
And it's not that "this is HIGHLY imporbable and most likely will NEVER happen".  
I've fallen victim to it which is why I'm so adamant about it.  
And it's **completely preventable** if you just don't use global variables.  
Which is why so many guides/tutorials/courses/other coders will tell you the same thing.  
Avoid global variables. In ANY language, not just AHK.

> "What if I'm not sharing my code?"  

STILL don't use them.  
(Why do I keep acting like people are fighting me on this? Because they do! People don't appreciate the advice until they hit a problem involving it and then they're like "OMG I should've listened to Groggy!")  

Global vars can screw over your own code just as easily.  
What happens if you accidentally double dip on a global variable in your own code?  
You make a new piece of code that has a few functions.  
They all need access to the same variable so you make it global so they can all access it.  
However, you forget about the other part of the code that has an identical global variable name.  
You now have two separate groups of code using the same variable for different things. That's a big problem.  

But the bigger problem is AHK won't tell you about this unless the data type is different and causes an error.  
If they're the same data type, your code won't necessarily failr or show an error. Instead, it'll just start behaving oddly.  
Then it's up to YOU to spend the time troubleshooting it.  
And the error is really hard to detect, because when you go look at the code, it's all written correctly.  
Everything is logical. Everything is written correctly, even the use of the variable (that happens to be global).  
The code *should* work perfectly...but it doesn't.  
And until you realize you messed up and made a second global variable of the same name, you'll never find the bug.  

And that example is not an example.  
That's what we call an anecdote.  
It's this guy right here telling you:  
**"Don't use global variables because they're a pain in the ass, they aren't needed, and I don't want you guys wasting DAYS if not WEEKS trying to find a single, stupid bug like I did that could've been completely avoided had I respected the rule of not using global variables!"**

Since learning my lesson the hard way about global variables, I have never once used them again.  
None of the examples I've written use them.  
None of the code I publish uses them.  
I just **DON'T** use them and have never had a scenario where it was needed b/c there are other better options.  

In v1, globals were REALLY bad b/c of some bad design choices in that version.  
In v2, they did put some protections so it's harder to accidentally write to a global, but doubling up on them is still a possibility. Which is why you should just avoid them altogether.  

#### Examples of global variable alternatives

So where do we store "global" things?  

Are you needing a global for a value that shouldn't be changed?  
Make a function!  

    pi() {
        return 3.14159
    }
    
    radius := 3
    area := pi() * radius * radius
    MsgBox(area)
    
    ; And you can't write to a function
    ; This will throw an error
    pi := 10

What if need to be able to change the variable?  
That can be done, too.  
Set up the function to use its parameter.  

    MsgBox('tax is: ' tax())    ; Get the tax
    tax(1.09)                   ; Set a new tax rate
    MsgBox('tax is: ' tax())    ; New tax is saved
    
    tax(new_tax:='') {          ; Default is an empty string, a non-number
        static tax := 1.07      ; Permanent variable for tax
        if IsNumber(new_tax)    ; If new_tax is a number, we're setting a new tax
            tax := new_tax      ;   Update new tax with the number
        return tax              ; Always return the current tax
    }

Functions are the basic solution.  
Classes are the bigger solution.  
In the sections class later, you'll realize see how classes bundle variables and functions:

    MsgBox('tax is: ' restaurant.tax)   ; Get the tax
    restaurant.tax := 1.09              ; Set a new tax rate
    MsgBox('tax is: ' restaurant.tax)   ; Show new tax
    
    meal := 12.99
    drink := 2.99
    total := (meal + drink) * restaurant.tax
    MsgBox('Your total is: ' total)
    
    class restaurant {
        static tax := 1.07              ; One of the many properties or methods the class might have
    }

## The benefits and simplicity of functions

We understand scope, which is one of the benefits of functions.  
But what else makes functions so great?  
There are a **multitude** of things.  
But, before listing those reasons, I want to explain the simplicity of a function and what it does:

1. Functions "bundle" like-code and like-variables into a single, callable (usable) package.  
   It's a function because the block of code serves *some kind of function*.
2. Everything inside the function is in its own little private environment.  
   Code outside the function cannot do anything to the code inside the function.  
3. Functions can optionally accept zero or more pieces of data, called parameters.  
4. Functions can optionally return data with the `return` statement.  

That describes everything a function does.  
They're pretty simplisitic for what they are.  
However, they provide so many benefits.  
What are the benefits of this "simplistic" coding device?  

1. **Reusabitility and reliability**  
   There is no limit to how many times you can call (use) a function.  
   You only need to write the code correctly once and it will work right every time you call it.  
   This prevents the need to rewrite or copy and paste your code repeatedly.

2. **Abstraction**
   You take an entire sequence of code and abstract it away behind a single name that describes the code's actions.  
   Whenever you want to perform that sequence of code, you reference that function.  
   A single word with some parentheses replaces lines and lines of code.  
   This is abstrction and we will bring it up MANY times in this guide, including a section dedicated to it in the OOP section.

3. **Shorter code**
   Piggybacking on the abstraction paragraph, we replace entire blocks of code with a single function call.  
   If your function is 50 lines long, every function call after the first is 49 lines from being added to the script.  
   If you have 10 function calls, thats over 400 extra lines of code you don't have to write or copy/paste.  
   That's over 400 lines of code you don't have to scroll past while working on writing your code.  
   And that's over 400 lines of code not adding to the total byte size of the script.  
   The lines of code saved only goes up the more of them you use and the more times you reference them.  

4. **Simplified maintenence and error protection**  
   You need to use a specific chunk of code 10 times in your script.  
   
   Option 1: You write/copy&paste the code in 10 different places throughout your script.  
   When you need to change or update that code block, you now have to do it in 10 different places.  
   You also now have 9 more chances to make a mistake in your code.  
   Or, worse, you have the chance to accidentally miss a code block. So everything appears to work correctly until that one skipped block needs to be used.
   
   Option 2: You create a function and write your code in there.  
   You can now put 10 function calls in your script.  
   When it comes time to update or change your code, you only change it in ONE spot! The function body.  
   That change updates all function calls, so there's no going to 10 individual blocks of code.  
   That's also 9 less opportunities to introduce an error.  
   And there's no "skipping" a block because there's only one block to deal with.  
   
   Functions simplify maintenance and the help prevent errors.

5. **Divide and conquer complex tasks**  
   Functions can call functions which can call other functions and those functions can call other functions.  
   The idea is that larger tasks should logically be broken down into smaller ones.  
   Use your functions when you want to logically group toether some code or when a task is getting to complex or lengthy.  
   If there's a lot going on, then there's probably a lot of different "functions", so give each one their own "function" to do their work.  
   
   Example: Let's say you want to process a bunch of user profiles and you want to make sure their phone number is formatted a certain way and that email addresses are in a `mailto:` format.  
   Your main function should set up getting the profiles names and looping through them.  
   But the process of getting the phone number from the profile and then parsing through it and formatting it a certain way could go to another function called `format_phone_number()`.  
   And then another function can handle formatting the email: `format_email_mailto()`.  
   Each function has a purpose and they all work together to accomplish the goal.

6. **Reduce global space names**  
   A function can bundle up mulitple varaibles and code into a single function.  
   This means only the function name is added to global space.  
   All the variables, objects, and even other functions are private to the function and are being kept out of global space, thus helping respect that unwritten rule of "Minimize the amount of things in global space".  

7. **Cleanup**
   Last but most definitely not least is the fact that functions help keep the script clean.  
   When a function completes, it clears out all the temporary variables it used.  
   This keeps temporary variables from buidling up, reducing the footprint of the program and helping to prevent memory leaks.  
   We'll discuss this more when we talk about static variables.

## Define a function

Now that we understand the purpose and benefits of functions as well as how scope and global space work, let's dive into making them and learning how all the parts work.

To create a function, we provide a name, parentheses, and curly braces:

    ; This is what the minimal shell of a function looks like
    my_func() {
        
    }

To call a function, use the function's name with parentheses.  
Anytime you put parentheses at the end of something, you're "calling" it.  
This is explained later when we learn about `Call()` methods.  
Functions are meant to be called and you'll hear the term used a lot.  

    ; Call, or use, the MsgBox function
    MsgBox()

Because functions are private and nothing can see the code inside (not in scope!), we need a way to get data into a function.  
That's where parameters come in.  
Functions can have zero or more parameters.  
Parameters are how we pass data into the function to use.  
These become variables containing whatever the user passes in.  
There are multiple types of parameters that can be used, as discussed later.  
And a rule when using multiple parameters is there must be a comma separating each parameter

    ; Showing the function being called and providing the 1 required parameter
    my_func('Hello, world!')
    
    ; Make a function that requires 1 parameter: A message
    ; THen call the message box, include the message, and add a custom title
    my_func(msg) {
        MsgBox(msg, 'Custom title added by func')
    }

Parameters help us get data into the function, but we can also get data back from a function.  
This is where the [`return` statement](https://www.autohotkey.com/docs/v2/lib/Return.htm) comes into play.  
`return` will stop the flow of code at that point and, optionally, can return a value.  
Using the pi example from earlier:

    MsgBox('Pi is: ' pi())

    ; Function that always returns pi
    pi() {
        return 3.14159
    }

Let's put all of these things together and make a function that adds two nummbers and returns it.  
We would normally use the add operator, but this is a classic example that property demonstrates parameters and return values.  

    ans := add(2, 5)            ; Call add function with the numbers 2 and 5
    MsgBox('2 + 5 = ' ans)      ; Show the result of 2 and 5 being added

    add(num1, num2) {           ; Define an add() function with 2 parameters
        sum := num1 + num2      ; Add two numbers together
        return sum              ; Return sum to the caller
    }

Now that we have the basics down, we can get to the particulars.

## Return values

The [`return` statement](https://www.autohotkey.com/docs/v2/lib/Return.htm) is an important statement in almost any language.  
It serves two purposes when working with functions: 

1. It stops the thread (the flow of code).  
   This prevents the code from going any further.  
2. When a return is used, a value is returned to the caller.  
   If no return value is declared, an empty string is returned by default.  
   And when a function is used in an expression, the return value is what the function is "evaluating" to.

Stopping the flow of code:

    exit_script()
    
    exit_script() {
        ans := MsgBox('Shutdown script?',, 'YesNo')     ; Ask if script should shutdown
        if (ans = 'No')                                 ; If the no button was clicked
            return                                      ;   Return to caller/stop thread here
        ExitApp()                                       ; The thread doesn't reach here if ans is no
    }

Returning a value. We can use our good old adder example:

    MsgBox('7+8=' add(7, 8))    ; MsgBox is the caller
                                ; It calls add() first, which evaluates to 15
    
    add(n1, n2) {
        sum := n1 + n2          ; The numbers are added together
        return sum              ; The sum is returned to the caller
                                ; This is the value the function call will resolve to
    }

It's a simplistic idea but it gives functions a lot more control and *functionality*.  

I do want to give some insight into how the flow of code works, both in general and in reference to functions.  
Let's take some random code and break it down.  
This function requires one parameter.  
If the number is less than 10 it sends back a string error message.  
If it's 10 or higher, it pops up a message box.  

    x := test(7)                            ; Run test with the number 7 and no thank you popup
    MsgBox(x)                               ; Shows an error and reason
    
    test(param) {
        if (param < 10)                     ; If the param was less than 10
            return 'Error, less than 10'    ;   Return. Code stops running here. The string error is returned.  
        MsgBox('Thank you!')                ; Otherwise, show an thank you popup
    }

Let's explain how the thread flows through this code.  
Line numbers are included to describe where the thread currently is.

    1. x := test(7)                            ; Run test with the number 7 and no thank you popup
    3. MsgBox(x)                               ; Shows an error and reason
    4. 
    5. test(param) {
    6.     if (param < 10)                     ; If the param was less than 10
    7.         return 'Error, less than 10'    ;   Return. Code stops running here. The string error is returned.  
    8.     MsgBox('Thank you!')                ; Otherwise, show an thank you popup
    9. }

When we start the script, the thread starts at the first line of the script and goes down.  
If a line contains anything, it's read from left to right.  


1. The thread starts at line one
2. Line one is evaluated.  
   `test(7)` is called first because we always evaluate sub-expressions first.  
3. AHK uses a "stack" to track function jumping.  
   A stack is pretty much an array.  
   This is used to track where each "jump" came from.  
4. AHK is jumping from line 1, so it stores 1 in the stack.  
5. The thread jumps down to the function definition on line 5 along with its parameter, 7.  
6. 7 is plugged into the parameter
8. The thread continues to line 6.
9. An if-check happens. param (7) is less than 10.
10. The if-statement evaluates true and goes to line 7.
11. A return is encountered so the thread stops here and never goes to line 8.
12. The return value is set to: 'Error, less than 10'
13. AHK remove the last jump point from the stack. It's 1.
14. AHK "returns" to line one with the string.
15. `test(7)` call finished and resolves to 'Error, less than 10', which is assigned to `x`.  
16. The thread goes to line 2.  
17. MsgBox displays the contents of `x`.
18. The thread continues past the function definiton, reaches the end of the script, and the script calls [`Exit()`](https://www.autohotkey.com/docs/v2/lib/Exit.htm).  

This shows you how the thread works, going down one line at a time and evaluating each line as it goes.  
It also explains how AHK tracks function "jumping" using a stack (an array).  

For those with curious minds wondering "how many jumps are allowed?"  
The real question is how many jumps deep can you go or how many slots does the stack have.  
The answer is well over 1000.  
Meaning to reach recursion limit, you would have to call a function that calls another function that calls another function that calls another function.  
It has to do that over 1000 times without hitting the expected returns it needs to jump back.  
It is NOT normal to get anywhere even remotely close to 1000 jumps deep.  
Hitting a recursion limit is almsot exclusively called by some kind of infinite calling loop.

To clarify some points about the `return` statements :

* AHK **always** puts an empty return at the end of every function, even if you don't declare one.  
  This is a default behavior because a function needs to encounter a return to know when to go back.  
  You can include a return but you don't have to, as one is provided automatically.

* All return statements will return SOME value.  
  If no value is defined, an empty string is used by default.  
  Without this default behavior, `unset` would be returned instead and that would cause a lot of problems and require everyone know about the maybe operator.  

Code to prove these statements:

    returned := test()                      ; Call the empty test function
    if (returned == '')                     ; Is the returned value equal to an empty string?
        MsgBox("Empty string detected!")    ;   It sure is!
    
    test() {                                ; Test function with no params
    }                                       ; No code or return statement or return value

> "But what if I don't want the returned empty string?"

You don't have to save it. Or use it.  
It's perfectly normal to call a function just for its functionality and not do anything with a return value.  
If you don't assign the return value to something, the return value resolves and when the line finishes executing, the value "fizzles".  
Meaning the value is discarded and nothing happens.  
It's normal to do this.  

Think about the `MsgBox()` function and how many times we've used it.  
That function always returns the word of the button you clicked.  
And we almost exclusively use it without saving the return value.  

We don't need it so we don't save it and it's discarded.

One last thing to mention about return values.  
What if you make a hotkey and it reaches a return?  
What happens to the value that is returned to the caller (the hotkey)?  

Or what if a gui control event activates a function?  
What happens when it returns?  

If you were wondering this, I like where your brain is. Staying curious is a good thing!  
And the answer to the question, like almost all AHK-related questions, is answered in the AHK documentation.  
This information about return is logically located in the [`return` docs](https://www.autohotkey.com/docs/v2/lib/Return.htm).

> "If there is no caller to which to return, Return will do an Exit instead."

Meaning when a timer or a gui or a hotkey starts starts running code, eventually the doce will "return" to it, in which case return acts like `Exit()`.  
And `Exit()` is how we stop a thread immediately.  

Side note: As a good coding habit, you should almost exclusively use `return` for thread control and only use `Exit()` in very specific situations where it's *needed*.  
It's uncommon to see Exit() used in code.  
This is because the flow of code should (generally) be allowed to go the whole course.  
This ensures that other stuff which might be expected to get done **does** get done.  

Again, this is not a hard requiement, but it can save a lot of problems and troubleshooting in certain situations.  

### Function return values replaced v1's `ErrorLevel` variable

A constant question heard when talking about AHK is "why is v2 better that v1?"  
I'll give you a great reason right now.  

v2 doesn't use commands anymore. It's all functions.  
This is wonderful.  

Functions have return values and ByRef parameters.  
Because of that, there's no need for v1's `ErrorLevel` global variable.  
In v1, there were a ton of commands and to get the results of those commands, a single variable was used.  
Each time one of these commands ran, they would set the global variable `ErrorLevel` to *something* unique to that command.  
There's an [entire doc page filled with what these values meant for each command](https://www.autohotkey.com/docs/v1/misc/ErrorLevel.htm).  
It might be a `1` or a `0` or an empty string or a word or positive number or a negative number or something else.  
You would be expected to run a command and then immediately use or save the ErrorLevel value before another command updated it to its new value.
In other words, `ErrorLevel` was responsible for tracking the "end result" of EIGHTY FOUR DIFFERENT COMMANDS.  

In v2, we have no concept of the `ErrorLevel` global var because we don't *need* it anymore.  
Instead, all functions provide return values and if a function needs to communicate something to you, it almost always does it by using a return value.  
And there's no massive sheet of return value meanings.  
You read the documentation for the function you're using and it tells you specifically what the return value is.  
Also, if you followed my advice and installed my "Add-on Enhancement Update", then every function and method in the entire AHK language has its return value logged in the add-on.  
Just type it and the call tip will tell you everything you need to know about it, including return value type and meaning.  

As an example, consider how ImageSearch operates between both versions:

    ; v1
    ImageSearch, ...        ; do an image search
    if ErrorLevel {         ; Then immediately check ErrorLevel to see if it's true
        ; code to run       ;   If true, run this code
    }

    ; v2
    if ImageSearch(...)     ; Run image search and if true, image was found!
        ; code to run       ;   Run this code.


## Parameters

Due to functions being private, we need a way to get data into them and that's why we have parameters.  
Functions have four different types of parameters, and we're going to discuss them all:  

| Type              | Example
| :---              | :--- 
| - Required        | `fn(req1, req2)`
| - Optional        | `fn(opt:='Default')`
| - Variadic        | `fn(var*)`
| - By Reference    | `fn(&req, &opt:=0)`

The "By Reference" parameter isn't actually a type, but instead it's more like an option that a parameter can use.  
We'll discuss the term "by reference" in the next section and it'll help clarify the "ByRef" parameters when we get to them.  

The maximum amount of parameters that can be defined in a function is 255.  
This is a max number and you should never be anywhere near 255 parameters in a function.  
Consider the fact that your average function is going to have 0-3 parameters and that it's extremely rare to see a function 10+ parmeters.  

We're going to talk about each parameter type, how they're used, and the order they have to be declared.  

However, before that I want to talk about an important distinction to make about functions: Passing parameters "by value" vs passing parameters "by reference"

### Learing about references, dereferencing, and double derefs

Before we start discussing the different types of parameters, we need to understand how data is passed ***into*** parameters.  
To do that, we need to understand what the word "reference" means.  

When we create a variable `x := 42`, AHK does a lot of things in the background for us.  
1. It asks the operating system for some space in RAM.  
2. The OS finds a block of free space and marks it as in-use.  
   We'll say the address is `0x1234`. That address is where our number `42` is now stored in RAM.  
3. The OS gives that memory address back to AHK.  
4. AHK now associates the memory address `0x1234` with the name given to the variable, or `x`.  
5. `x` is now a ***reference** to the memory address `0x1234` where the number `42` is currently stored.  
6. AHK also keeps track of how many things in the script are actively making use of the reference.  
7. When AHK has no more references to the variable (say it was deleted or maybe the script is shutting down), AHK tells the OS that it no longer needs that memory anymore.
8. The OS marks that area as "available" and it can be written to by others tuff.

So AHK does ALL of that for you in the background so you don't have to.  
But the bigger point is that when `x` is assigned `42`, the variable `x` is acting as a *reference* to a memory address where the number is being stored in RAM.  
This is why we call it a reference.  

When we use the memory address in `x` to get its value, we're "derferencing" the variable into its memory address.  
Then we're getting the value from that memory address.  
Why do we call it "dereferencing"?  
The "de-" prefix is latin and means "from", with "de reference" meaning "to get from a reference".  

Going a step further, this also answers a very common question about why this operator `%var%` is called a "double deref" or "double dereference" operator.  
It's because two separate dereferences are happening.  
Take this code for example:

    num := 42
    test := 'num'
    
    ; %test% is a double dereference and produces: 42
    ; 
    ; A double deref first evaluates, or dereferences, the exprssion between the percent signs.  
    ; In this case, the test variable contains the string 'num'
    ; %test% becomes: num
    ; num was gotten "from the reference" to test  
    ; First dereference.
    ; 
    ; Next, num is evaluated, or dereferenced, from its memory reference
    ; The number 42 is gotten "from a reference" to that memory
    ; Second dereference.
    ;
    ; %% is the "Double dereference operator"
    ; MsgBox shows us the 42 as expected
    MsgBox(%test%)  ; Shows 42

So now we understand that everything in AHK is just a memory *reference*.  
It's helpful to understand this.  
But it's not necessarily helpful to constantly think of everything like this.  
Variables, objects, functions, and the such are all individual things.  
Think of them as such instead of thinking of them all as "address in memory".  
This is abstraction at work again and you'll hear me keep bringing it up.  

> "How does this all tie into functions and parameters?"

We have to understand references to understand how parameters are sometimes handled "by value" and sometimes "by reference".

### Passing parameters "by reference" vs "by value"

Functions are designed to handle primitive parameters and non-primitive parameters differently.  
Primitive values are duplicated and sent "by value".  
Non-primitive values, such as objects, are sent "by reference".  
Time to explain.

When a primitive value (a string or a number) is passed into a parameter, the original variable is not used.  
Instead, the value is **duplicated** and the memory reference of the copy is passed into the function.  
This is called passing in a parameter "by value".  
This is because the original variable's reference isn't used.  
The reference is for the duplicate **value**.  
And this is why we say it's passee "by value".  

Let's start off with some code to prove this.

    x := 10                 ; Assign 10 to x
    test(x)                 ; Run test function using x
    MsgBox(x)               ; x shows 10 because the duplicate primitive was changed, not the original
    
    test(var) {             ; A copy of x is passed in "by value"
        MsgBox(var)         ; Show it contains 10
        var := 'Hello'      ; Update to a new value
        MsgBox(var)         ; Show the new value has been assigned
    }

The whole reason a duplicate is made is to protect the original variable from being accidentally changed.  
The function can do whatever it wants to that copy and the original goes unchanged.  
That means you can take the copy and add to it, take from it, reassign it, or whatever you want.   

But what about objects and other non-primitives?

When a function works with something like an object, it does not duplicate it.  
Instead, it passes in the original reference to the object  
This is why we say the parameter is passed "by reference".  
It's a reference to the original and changing it in the function means changing it outside the function.  

Let's do another code example proving what was just said.

    x := {a:'Gatorade'}     ; A new object with 'gatorade' for the a property
    test(x)                 ; Pass the object into the function
    MsgBox(x.a)             ; The property is now "H20" because the function altered it
    
    test(obj) {             ; The original object reference is passed in "by reference"
        MsgBox(obj.a)       ; Show the property value
        obj.a := 'H20!'     ; Update to a new property value
        MsgBox(obj.a)       ; Show the new property has been assigned
    }

What was stated is what happned. Changing the object inside the function changed it on the outside, too.  
The topic of references will also come up again later in the guide.  
Like when we discuss the `Clone()` method and what "shallow copies" are.  

> "Why are primitives protected but objects aren't?"  

Great question!  
Because primitives are tiny compared to objects.  
A primitive can only contain a single value, so even a very large string can be small compared to an object.  
The time and cost to duplicate a primitive is so low that it's worth it to protect the original value.  

Objects, on the other hand, are larger.  
They can contain many different properties and method references.  
And if those objects contain objects, all those objects would need to be duplicated, too.  
This continues to branch our where other properties containing objects would need to be duplicated.  
Do the see the problem?  
And this would happen every single time any object was passed to any function.  
This could cause devestating cascades of copying that effectively strangle the application to death.  

And that is why objects aren't duplicated and why we pass them "by reference" to functions and methods.  
Yes, they can be changed and that's just something we learn and respect.  
Coders understand that primitives can be freely altered and messed with but objects must be respected as the originals they are.  

Now you know it too and you undersatnd the difference between "by reference" and "by value".  
Now we can learn about the different types of parameters a function has access to.

### Required parameters

The parameter we've been using so far is the required parameter.  
Required parameters indicate that the data in that parameter is required for the function to work correctly and the user **must** provide it.  
If you have two required parameters, you cannot call that parameter without providing two values.  
Take our adder function for example:

    ; This throws an error because add requires exatly two parameters.
    ; No more. No less. But we've only provided 1. 
    add(7)
    
    add(num1, num2) {
        sum := num1 + num2
        return sum
    }

The positioning rule for required parameters is that they all be declared first (left of) all optional parameters.  
That includes optional/maybe parameters as well as variadic parameters.  

### Optional parameters

Optional parameters are pretty simple to understand.  
They're required parmeters with pre-assigned values.  
If the user doesn't include that parmeter, it's not an error because it already has a value assigned to it.  
If the user does include a value, that value gets assigned over the pre-assigned value.

It gives the parameter a default value if one isn't provided.

    greeting('GroggyOtter')                     ; Call with a parameter
    greeting()                                  ; Call without a parameter

    greeting(name:='User') {                    ; Optional parameter b/c default value assigned
        MsgBox(
            'Hello, ' name '.'
            '`nThanks for learning AHK v2!'
        )
    }

A rule with optional parameters is they must come *after* required parameters.  
You cannot mix them.  
Required parameters are always listed first (left) and optional parameters are listed last (right).  
The only parameter that can come after optional parameters is the variadic parameter.  

This code example throws an error because AHK sees an optional parameter before a required one:

    test(, 'AHK')
    test(opt:='v2', req) {                  ; <--Error!
        MsgBox('req: ' req '`nopt: ' opt)
    }

However, if we put the parameters in the correct order, the function works perfectly:

    test('AHK', )
    test(req, opt:='v2') {                  ; This is valid!
        MsgBox('req: ' req '`nopt: ' opt)
    }

The order is a hard rule when using functions:  
`Required Params > Optional Params > Variadic Param`

Optional parameters can also be defined by using the "maybe" `?` operator.  
But to understand "maybe", we need to understand the `unset` keyword and what it means for something to have an "unset value".  

### Understanding `unset`

AHK has a keyword called [`unset`](https://www.autohotkey.com/docs/v2/Language.htm#unset) and it does what its name describes: it unsets the value and type of something.  
The thing *becomes* unset.  

Think of unset as a way to define (initailize) something without having to commit a value or type to it.  
It exists, but it is unusable.  
It is not a string or a number.  
It is not an object or an array.  
It is not a VarRef or a COMObject.  
An unset value is just a shell with no defined type and no associated value.  
It's waiting to be something; to be set (assigned) a value of *some* type so it can become usable.

Using JavaScript as a comiparison, `unset` is the closest thing we have to an `undefined` type in AHK.  
This makes sense considering the value and type of the thing is now unset, which is like being undefined.  
But maybe a better comparison is to `null` because, like unset, you don't really *work with* null.  
You check to see if something is null or is not null.  

But neither are a good comparison for unset.  
`null` and `undefined` are data types, `unset` is not a data type.  
`null` and `undefined` can be used in code while using `unset` will always result in an error.  
`null` and `undefined` both evaluate to a Boolean value (false). `unset` does not evaluate b/c it cannot be used and has no value TO evaluate.  

If unset is used, AHK will throw a special error called [`UnsetError()`](https://www.autohotkey.com/docs/v2/lib/Error.htm#UnsetError) that's designed specifically for unset value errors.  

While using an unset value does throw an error, there are ways to work with and manage unset values and it's the reason the "maybe" `?` and "or maybe" `??` operators have their own sections.  
They are both used to work with unset values.  
There's also a special function called `IsSet()` that can tell us if something is set or unset.  

Let's show `unset` in use:

    x := 5      ; "Set" x to 5
    MsgBox(x)   ; Show variable is set
    
    x := unset  ; Unset x, removing its value and type
    MsgBox(x)   ; Use it: Unset error!

The last line throws an error because you **cannot** use an unset variable.  
There is *no value* to use!  

If we need to check if a value is set or unset, the [`IsSet()` function](https://www.autohotkey.com/docs/v2/lib/IsSet.htm) can be used.  
Pass any value in and it will return a `1` if the item has a set value or a `0` if the value is `unset`.  
Let's try it.

    ; Unset value
    x := unset
    
    if IsSet(x)
        MsgBox('x is set!')
    else MsgBox('x is unset!')
    
    ; VS
    
    ; Set value
    x := 10
    
    if IsSet(x)
        MsgBox('x is set!')
    else MsgBox('x is unset!')

> "Wait, Groggy. Why can we pass an unset value to the `IsSet()` function without it throwing an error? It's `unset`." 

Great question!  
Normally, it *would* throw an error. Except I keep mentioning that there are ways to work with unset.  
The `IsSet()` function parameter makes use of the "maybe" `?` operator, which we'll be talking about in an upcoming section.  
And that's why it doesn't throw an error.

Now let's use unset as a default parameter for a function.  
There are many reasons you might want to have a parameter be unset, as discussed in the [upcoming section](#benefits-of-using-unset).  
The point is that an optional parameter can be defaulted to unset, allowing it the parameter to be defined but without committing a value or type to it.

    greeting('Groggy')                          ; This works
    greeting()                                  ; This fails
    
    greeting(name := unset) {                   ; Name defaults to an unset value
        MsgBox(
            'Hello, ' name '.'                  ; <-- This line will error if name is unset
            '`nThanks for learning AHK v2!'
        )
    }

In the code above, if not parameter is passed in, an error will be thrown when MsgBox tries to use `name`.  
This error might even be desireable for detecting errors, as we'll discuss in the next section.  
But in this case, it would probably be best to do an unset check using `IsSet()`.  
If it's not set, we can choose what to do:  

* Maybe throw an UnsetError.  
* Maybe prompt the user to enter in a name.  
* Maybe check another part of the code for a name.
* Maybe give it a default value.  

We'll give it a default value.

    greeting('Groggy')                          ; This works
    greeting()                                  ; And now this works

    greeting(name := unset) {                   ; Name defaults to unset
        if !IsSet(name)                         ; If name is NOT set
            name := 'User'                      ;   set it to User
        MsgBox(                                 ; This function call will no longer throw an error
            'Hello, ' name '.'
            '`nThanks for learning AHK v2!'
        ) 
    }

So now we understand `unset` and how to use `IsSet()` with unset things.  

We should talk about the benefits of using `unset` values.

#### Benefits of using unset

A benefit to using unset parameters is that it can give your parameters a common baseline to go off of.  
Making things `unset` until they're assigned a value can be a good troubleshooter.  
If something starts unset and isn't assigned correctly or is skipped or some other logic error happens, the act of using it will throw an error.  
This points you to the problem area and gives you an immediate idea of what's wrong.  
From there, you backtrack to figure out where the problem is happening.

Another way `unset` can be used is by providing a way to evalute something as false that might not otherwise have a false value to evaluate.  
Using unset as the "false" version of something means anything set can be true and unset is false, with `IsSet()` being the way you evaluate it.  

Later, when talking about objects, we'll learn that unset can be used to delete a property from an object.  
The property is no longer set, so it does not exist to the object.

There are plenty of other situations where using unset might be useful.

At the end of the day, unset is another tool in your coding toolbox.  
Use it when you think there's a good reason to use it.  
And if you decide to never use unset, there's **nothing** wrong with that.  
You code how you want to code.  

Finally, we can learn about those question mark operators: "maybe" `?` and "or maybe" `??`

#### The "maybe" `?` operator

The "maybe" `?` operator is a special operator that can be included at the end of a variable or parameter.  
This operator tells AHK that it's OK for that thing to be `unset`.  
Think of it as "it may be set or it may be unset".  

To use the maybe operator, include it after a variable or parameter name:

    my_func(maybe_param?) {
        
    }

I refer to these as "maybe parameters", though they're technically still just optional parameters.  

We've already worked with a function that specifically makes use of maybe parameters: `IsSet()`  
This is why it's allowed to accept an unset value.  
Because its parameter uses the maybe operator, it is **allowed** to accept unset values and not throw an error.  
Here is a general code outline of how `IsSet()` works.  

    IsSet(value?) {
        if special_func_to_determine_if_unset(value)
            return 1
        else
            return 0
    }

Another behavior of functions that should be discussed is what happens when you call a function requiring a parameter without providing a parameter.  
If no parameter is provided, `unset` is used.  
Even if AHK didn't check parameter count vs required parameters, an error would still be thrown by virtue of assigning `unset` to a parameter.  
Now what happens if that parameter is ALLOWED to be unset?  
It's no longer a required parameter because if you omit it, it accepts the unset value.  
This is how the maybe operator differs from using unset as the default value, though both ways get ya to the exact same spot.

    ; Optional parameter using unset assignment
    ; > Function is called
    ; > No parameter provided
    ; > unset is sent
    ; > function receives unset but is not allowed to use it
    ; > function keeps its default value, which happens to be unset
    ; > parameter value is now unset via being assigned unset to begin with
    unset_default()
    
    unset_default(param:=unset) {
        if !IsSet(param)
            MsgBox(A_ThisFunc ' is unset!')
    }
    
    ; VS 
    
    ; Optional parameter using maybe operator
    ; > Function is called
    ; > No parameter provided
    ; > unset is sent
    ; > function receives unset
    ; > parmater is a maybe parameter and is allowed to be unset
    ; > parameter value is now unset via accepting the unset from the omitted parameter
    unset_maybe()
    
    unset_maybe(param?) {
        if !IsSet(param)
            MsgBox(A_ThisFunc ' is unset!')
    }

It should be mentioend that the maybe operator works similiarly to how "nullable types" work in other languages.  
Instead of allowing a variable to be of "of null type", it allows the AHK variable to be "of unset type" (even though it's not a type).  
Bonus to this: The `?` is the same character used for nullable typing in C#.  
Yet another instance of how AHK is pretty much a mix of JavaScript and C# syntax.

While the maybe operator primarily deals with variables and parameters, it can also be used with arrays and object properties to indicate unset values.  

Array: 

    ; var does so the 'a' property is unset instead of throwing an error
    ; Meaning it doesn't exist as far as the object is concerned.  
    obj := {a:var?, b:'test'}
    ; Looping through all own props shows only 'b'
    for key, value in obj.OwnProps()
        MsgBox(key ': ' value)

Object literal:

    ; var is unset, so the second element is unset instead of throwing an error
    arr := ['a', var?, 'c']
    ; Looping through all elemens show element 2 is unset
    for index, value in arr
        if IsSet(value)
            MsgBox('Item ' index ' is set to: ' value)
        else MsgBox('Item ' index ' is UNSET!')

Let's go take a step back to our greeting() function from the prior section.  
We're going to update this thing with our new maybe operator.  
And we'll continue updating it in the next section.  

Let's replace `name := unset` with `name?`, as they end with the same result.

    greeting('Groggy')
    greeting()

    greeting(name?) {
        if !IsSet(name)
            name := 'User'
        MsgBox(
            'Hello, ' name '.'
            '`nThanks for learning AHK v2!'
        )
    }

Now we understand we can mark parameters as being `unset` using a single character, the "maybe" `?` operator.  
It also gives us a much shorter and quicker way of writing `param := unset`: `param?`  
Both convenient and appropriate-looking.  
Like "Is there going to be a value set? Maybe!" `¯\_(ツ)_/¯`

Let's learn about the "or maybe", or "coalescing" operator.  

Coalescing operator sounds so much cooler.

#### The "or maybe" `??` operator

This "or maybe" operator, also known as a "coalescing operator", is used as a shorthand way of determing if a value is unset.  
It acts similar to how `IsSet()` works and ensures that a value always "coalesces" to a set value.  

To use this operator, you need something that may or may not be unset: `value`  
And then you need to choose a value or expression to evaluate if `value` is unset:  

    value ?? expression

If value is set, the entire expression evaluates to whatever `value` is.  
If value is unset, the expression evaluates to whatever `expression` is.  

    var := unset
    MsgBox(var ?? 'UNSET!')     ; Right side is used b/c var is unset
    
    ; VS
    
    var := 'Hello!'
    MsgBox(var ?? 'UNSET!')     ; Left side is used b/c var is set

Remember that an expression isn't just about primitives and values.  
You can run code with expressions.  
In this example, `??` is used to detect something unset, post a message, and exit the script

    var := unset
    ; Var is unset, so evaluate expression on right
    ; That expression happens to be function calls
    ; It doesn't matter what the expression evaluates to, only that the functions run  
    var ?? MsgBox('You messed up. Var is unset. Exiting script!') ExitApp()

For the sake of those with curiousity, that would have *coalesced* to `'OK'` from the MsgBox's return string.  
And ExitApp() doesn't return anything because it shut the script down.  
But if it did, it would most likely be returning an empty string.  
So theres your answer. That experssion *would* evaluate down to the string `'OK'` if the script didn't shutdown.

But the most frequent use you'll see for the "or maybe" operator is assigning default values created by maybe parameters.  
Instead of a bunch of calls to `IsSet()` which will create multiple lines, you'll see single lines setting default values:

    ; 3 maybe parameters made with '?'
    fn(name, age?, email?) {
        if !name
            throw Error("Name required!", A_ThisFunc)
        
        ; Default age to 0, indicating never set.
        age := age ?? 0
        
        ; If no email is provided, use an empty string.
        email := email ?? ''
    }

Time to jump back to our greeting function we keep working with.  
Using the coalescing operator, we can replace this `IsSet()` check in the code:

    if !IsSet(name)
        name := 'User'

And here's the updated function.

    greeting('Groggy')
    greeting()

    greeting(name?) {
        name ?? name := 'User'
        MsgBox(
            'Hello, ' name '.'
            '`nThanks for learning AHK v2!'
        )
    }

We *could* reduce the code some more by getting rid of the name variable and using the operator directly in the MsgBox() call.  
Rememember the parenteses, otherwise the operator won't work right and it'll try to included everything after `??`.  

    greeting('Groggy')
    greeting()

    greeting(name?) {
        MsgBox(
            'Hello, ' (name ?? 'User') '.'
            '`nThanks for learning AHK v2!'
        )
    }

And then reduce it a little more by putting the whole thing on a single line instead of spreading it out.

    greeting('Groggy')
    greeting()

    greeting(name?) {
        MsgBox('Hello, ' (name ?? 'User') '.`nThanks for learning AHK v2!')
    }

We can reduce the code one more time **and** it's an excuse to show off the fat arrow `=>` operator, reducing the entire function down to a single line.  
Don't worry, this operator gets its own dedicated section later.  

    greeting('Groggy')
    greeting()

    greeting(name?) => MsgBox('Hello, ' (name ? 'User') '.`nThanks for learning AHK v2!')

OK, that was fun.  
And now you're educated on those crazy looking question mark operators that make working with `unset` easier.

* `?` = "Maybe" operator, acts like "nullabe typing" operator.
* `??` = "Or maybe" operator, also known as the "coalescing operator".  

Remember, you don't have to use any of these things.  
Both of these operators, unset values, and even optional parameters are not required to write code.  
You don't NEED them as there's always a way to write something without the need of this stuff.  
But they're here if you want to use them to make writing your code easier, faster, and clearer.  

### Varaidic parameters and the variadic `*` operator

A variadic parameter is a special type of optional parameter.  
When a parameter is marked variadic, it's turned into an array object.  
This allows any (reasonable) amount of extra parameters to be passed into the function, as they're all inserted into the array.  
This also circumvents the 255 parameter limit of functions. Again, I don't know why you would **ever** pass that many values by parameter.  
Just make an array of values and pass THAT in.  

The variadic `*` operator is how we indicate a parameter is variadic.  

    my_func(variadic_arr*) {
        
    }

Let's make an example of a funciton that can take in a "varying" amount of parameters.  

    test('alpha', 'bravo', 'charlie')       ; Send multiple parameters in
    
    test(items*) {                          ; One variadic parameter (array object)
        list := ''                          ; String for list of each item
        for item in items                   ; For-loop through the array of items
            list .= item '`n'               ;   Add the item and a new line to the list
        MsgBox(list)                        ; Show the full list
    }

The big rule about variadic parameters: The last parameter is the only parameter that can be variadic.  
Some languages allow for a varidaic parameter to be used inside the definition, but AHK does not support this.  
Only the last parameter of a function can be variadic.  
This rule also infers the answer to "can a function have more than one variadic parameter?"  
No, because only the last parameter can be variadic. That's a hard rule.  
If you want a parameter to be an array of values, design a parameter to accept an array.  

    ; Make a note in your function comment that param2 should be an array.
    ; The param name also infers this.  
    ; Now you can pass in an array of your values and still have parameters come after it.  
    ; The only difference is AHK isn't making the array for you via a variadic parameter. 
    my_func(param1, param2_arr, param3) {
        
    }

Here is a quick, easy test.  
There are 6 different function definitions.  
Read each one and write/type down if you think "yes" it's valid or "no" it's not valid.  
Do not make this difficult. Remember the only rule for variadic parameters:  
Only the last parameter can be variadic!

    func1(req, var*)
    func2(var*, req)
    func2(var*)
    func4(opt:=1, var*)
    func5(var*, var2*)
    func6(req, var*, opt:=1)

Did you get through all of them?  
If so, here are your answers:
yes, no, yes, yes, no, no  
Doesn't matter what ya got, give yourself an `A`.  
There are no scores here, no one is keeping count, and you're here to learn.  
You deserve an `A` IMO.  
   
Let's do another example where we call a function, pass in a category name, and then pass in a list of things pertaining to that category.  
Same idea as the last example, except we're introducing a required parameter and a lot more values.  
    
    test('animals', 'ant', 'bird', 'cat', 'dog', 'elk', 'fox', 'goat')
    
    ; This is what's happening
    ; test(list_type := 'animals', var_arr := ['ant', 'bird', 'cat', 'dog', 'elk', 'fox', 'goat'])
    
    test(list_type, var_arr*) {             ; 1 required param, 1 variadic param
        str := 'List of ' list_type ':'     ; Make header of text using list_type
        for animal in var_arr               ; Loop through list of items
            str .= '`n' animal              ;   Add new line and item to list
        MsgBox(str)                         ; Show full list of items
    }

Variadic params are simple to understand.  
It turns the last parameter into an array and allows zero or more things to be passed in.  

#### Asterisk `*` can be used as a splat operator

In the previous section, we used the asterisk `*` as a variadic operator to defining a variadic parameters in functions.  
The asterisk `*` has another use when calling a functions.  
If you pass in an array to a function call, it acts as a splat operator, also known as a spread operator.  
This operator will use each element of the arry as a parameter in the function call.  

To clarify:

* When *defining* a funciton, the asterisk `*` acts as a variadic operator.  
  It is condensing all the extra parameter values into a single array object.  

      ; Pass 5 values into the variadic parameter (array)
      my_variadic('a', 'b', 'c', 'd', 'e')
        
      my_variadic(variadic*) {
          for item in variadic
              Msgbox(item)
      }

* When *calling* a funciton, the asterisk `*` acts as a splat operator.  
  It is spreading all the array elements to each parameter.
  
      params := ['a', 'b', 'c', 'd', 'e']
      
      ; Spread 5 array values to each of the parameters.
      my_splat(params*)
      
      ; The above code is doing this:
      my_splat(params[1], params[2], params[3], params[4], params[5])
      
      ; Or this:
      my_splat('a', 'b', 'c', 'd', 'e')
      
      my_splat(p1, p2, p3, p4, p5) {
          MsgBox(p1 '`n' p2 '`n' p3 '`n' p4 '`n' p5)
      }

Let's do another example with the splat operator using a more familiar function: `MsgBox()`  
This function has three optional parameters:

    MsgBox([Message, Title, Options])

Knowing that, we can make an array of parameters and then spread it to the MsgBox's parameters:

    ; Make an array.  
    ; message in first element.
    ; Title in second element.
    ; Options in third element.
    params := ['Are you learning a lot?', 'Custom title!', 'YesNo']
    
    ; Use spread operator to spread values to each parameter
    MsgBox(params*)
    
    ; Same as if we had used this:
    MsgBox('Are you learning a lot?', 'Custom title!', 'YesNo')

Onto another use for `*` in our code: discarding parameters

#### Callbacks and using variadic parameters to discard input

There is one more thing that the variadic operator can be used for.  
It can be used to discard parameters passed into a function.  
Using `*` with a parameter still makes the parameter variadic.  
However, if you omit a name and use only `*`, the array can't be made.  
This causes all extra values to be discarded as there's nothing to save them to.  

Discarding parameters is OK to do **as long as you understand that's what is happening** and you understand **what** you're discarding.  

You might be thinking "When would you ever want to do that"?  
When the parameters are passed in and you don't need them.  
This can happen easily when working with "callback functions".  
So before go any further, we whould probably discuss what those are.  

This can be a useful thing, but I want to add why it also falls under "good coding habit/bad coding habit".

People will blindly use this operator thinking that it "fixes" their code when it doesn't work.  
And a big cause of this is when callbacks are used.  

In fact, let's go through the process I watched someone go through when they discovered that `*` "fixes their code".  
This isn't verbatim, but it definitely encompasses what happened:

They created a GUI, added a control to it, and wanted it to do something when they clicked it.  
Something like this:

    goo := Gui()                                ; Make a gui
    con := goo.AddButton('w100', 'Click me')    ; Add a button control
    con.OnEvent('Click', click_callback)        ; When clicked, run this function
    goo.Show('w300 h200')                       ; Show the gui
    
    click_callback() {                          ; Run when button is clicked
        MsgBox('Succesfully clicked!')
    }

And if you look at the docs and at this, it looks like it *should* work.  
Everything appears to be written correctly.  
Run it and get this:

> Error: Invalid callback function.

Looking at the code for `OnEvent()`. Yup, click is in the first parameter slot and a function is in the callback parameter.  
It should work.  
Run it again...

> Error: Invalid callback function.

And this is the point where the problem happened.  

Option A: They should've tried to understand WHY it's an invalid callback.  
Hit up the docs and look.  
Google for it.  
Or come to the sub or forums and flat out ask "why is this invalid"?  

Instead, they went with Option B:  
Start Googling for a solution to "invalid callback function".  
Find a random post with almost no comments on it that *discovered*, "If you put `*` in your function OnEvent works!!"  
They try it and HOLY CRAP IT WORKS!  

    goo := Gui()                                ; Make a gui
    con := goo.AddButton('w100', 'Click me')    ; Add a button control
    con.OnEvent('Click', click_callback)        ; When clicked, run this function
    goo.Show('w300 h200')                       ; Show the gui
    
    click_callback(*) {                         ; Run when button is clicked
        MsgBox('Succesfully clicked!')
    }

And there's the problem. Neither of them know what they're actually doing.  
These are also the same type of new coders who then use global variables to solve their next problem, which is they can't get the info from the controls.  
The reason they can't get the info from the controls is b/c they don't understand how guis and gui controls are structured and they don't undestand that they are discarding the very thing they're needing.  

The previous error wasn't caused b/c it lacked that symbol.  
It occurred because they don't understand that callbacks will sometimes require parameters so they can pass data back.  
And the documentation covers this!  
If we go to the `OnEven()` docs, specficially the part [dealing with Click events](https://www.autohotkey.com/docs/v2/lib/GuiOnEvent.htm#Click), the very first thing after the description is an example of what the callback needs to look like.  

    Ctrl_Click(GuiCtrlObj, Info)

It's not exaclty hidden.  
In fact, all of these sections dealing with each event are almost exclusively there to give you information about the callback and what parameters it gives you.  
If we apply this knowledge to writing our callback function, you'll find it works perfectly.

    goo := Gui()                                ; Make a gui
    con := goo.AddButton('w100', 'Click me')    ; Add a button control
    con.OnEvent('Click', click_callback)        ; When clicked, run this function
    goo.Show('w300 h200')                       ; Show the gui
    
    click_callback(control, info) {             ; <-- Added required parameters
        MsgBox('Succesfully clicked!')
    }

So what's so great about those parameters?  
The `info` parameter isn't used with click events from a button.  
It still has to be included because there are non-button click events that require it.  
However, the first parameter is VERY important.  
While the point of this guide is not to teach you about guis, I am going to teach you this to make a point about callbacks.  

OnEvent() will always pass a reference to the control object that was clicked.  
A control object gives you access to a control's position, any text associated with it, its internal "name", and an especially useful property called `gui`.  
This property contains a reference to the gui that owns this control.  
With this property, you have access to the gui and all of its properties and methods.  
And because you have access to the main gui, you also have access to ALL the controls of the gui.

Are you starting to get an idea of why this one little callback parameter is SO useful???

Here's a fun gui I put together that shows all of this being done with a single callback function.  

    goo := Gui()                                    ; Make a gui
    goo.AddEdit('w200 vedt_title', 'Title here')    ; Edit box to enter a new title
    con := goo.AddButton('w100', 'Update Title')    ; Button to update gui title
    con.OnEvent('Click', title_update)              ; On click, run title update function
    goo.Show('w300 h200')                           ; Show the gui
    
    title_update(btn, info) {                       ; Two parameters as required!
        goo := btn.gui                              ; btn.Gui IS the gui
        new_title := goo['edt_title'].Text          ; Use the gui to get the text from the edit box
        goo.Title := new_title                      ; Apply new title to the gui
    }

What happens if someone write the callback like this: `title_update(*)`  
Your function "works" because you're discarding some really useful parameters.  

This isn't to say "never discard input".  
Again, it **is** OK to discard parameters when you ***understand*** you're discarding parameters and you know ***what*** you're discarding.  
Sometimes the point of a function is just to run some code and you really **don't** care about the input.  
As an example, take a function designed to shutdown the script.  
You're closing the script. It's highly unlikely you care about any parameters being sent in.  
In this case, there's nothing inappropriate about discarding them.  

    goo := Gui()                                ; Make a gui
    con := goo.AddButton(, 'Exit script')       ; Create button to exit script
    con.OnEvent('Click', exit_script)           ; When clicked, run this function
    goo.Show('w300 h200')                       ; Show the gui
    
    exit_script(*) {                            ; Who cares about parameters?
        ExitApp()                               ; We're just closing the script!
    }

### `FindWords()`, an example using all parameter types

This is a practical example of a funciton that utilizes all three parameter types.

    FindWords(text_to_search, [case_sensitive, arr_of_words])
  
This function lets you send in a text to search and a list of words.  
It counts how many times each word in the list occurs.  
The second parameter is to force case-sensitive word matches.  
The function returns a map containing all passed in words and the number of times each word is encountered.  
If none of the words are found, a `0` is returned to indicate no matches at all.  

    ; Chorus from a great a song
    lyrics := "You say goodbye and I say hello. Hello hello. I don't know why you say goodbye, I say hello. Hello hello. I don't know why you say goodbye, I say hello."
    
    result := FindWords(lyrics, , 'hello', 'goodbye', 'say')        ; Get total count of words hello, goodbye, and say
    MsgBox(                                                         ; Show number of times hello and goodbye were used
        'hello: #' result['hello']
        '`ngoodbye: #' result['goodbye']
    )
    
    ; This function will search through text for a list of words
    ; The function returns a map containing all provided words and their number of occurrences
    ; A 0 is returned if none of the words were found.
    ; 
    ; text - The text to look through
    ; case_sense - Require the word to be a case sensitive match.
    ;              1 for yes, 0 for no.
    ; words - Any amount of words to check for.  
    FindWords(text, case_sense?, words*) {
        result := Map()                                             ; Results of the check
        found := 0                                                  ; Track if anything was found
        sense := case_sense ?? 0
        
        if !words.Length                                            ; If no words were provided
            return 0                                                ;   Return 0, nothing can be found
        
        for word in words {                                         ; Loop through each word
            StrReplace(text, word, word, sense, &count)             ;   StrReplace() can be used to count words!
            if count                                                ;   If the word occurred
                found++                                             ;     Increment found count
            result[word] := count                                   ;   Assign count to word
        }
        
        if !found                                                   ; If no words had any matches
            return 0                                                ;   Return a 0 indicating no matches
        return result                                               ; Otherwise, return the map to caller
    }

### ByRef parameters and "by reference" variables

Earlier, we made it a point to understand how values are sent to parameters.  
We talked about how primitive values are sent "by value" because a copy is made and passed in.  
This is done to protect the original value.  
Objects are sent "by reference" because making copies of objects is too costly and isn't feesible. So we pass the original reference of the object to the function.  

The question is what if you **want** to send a primtive "by reference" instead of "by value"?  
What if you **want** the function to be able to change the original variable?  

Wanting to do this is completely normal and expected of most languages that use functions.  
In AHK, we call these kind of parameters ["ByRef" parameters](https://www.autohotkey.com/docs/v2/Functions.htm#ByRef).  
To mark a parameter as being ByRef, we use the "reference" `&` operator.  
It must be at the beginning of the parameter's name.  

    my_func(&by_ref_req, &by_ref_opt:=1) {
        
    }

When calling a ByRef parameter, the reference operator must also be included.  
This is done on both ends as a way of confirming that using the original variable is OK.  
    
    var1 := 1
    my_func(&var1, &var2)
    
    my_func(&by_ref_req, &by_ref_opt:=1) {
        
    }

ByRef variables can be used for numerous things, but one of the big benefits is being able to get data out of a function without having to use the return statement.  
Not only can multiple values be gotten out this way, but it leaves the return statement free to be used with something like a success/error return value.  

Look at the [built-in function `MouseGetPos()`](https://www.autohotkey.com/docs/v2/lib/MouseGetPos.htm).  
It has 5 optional parameters, with the first four being ByRef parameters and the 5th being irrelevant to the point:

    MouseGetPos(&x, &y, &hwnd, &control, flag)

We have a function and it's used to get four different pieces of data:  

* x = The x coordinate of the mouse
* y = The y coordinate of the mouse
* hwnd = The handle to the window under the mouse
* control = The control name or hwnd (depending on flag) under the mouse

Let's talk about the different ways we could get four pieces of data back from a function?  
There are multiple options.

1. **Use ByRef variables** 
   This is the current setup that MouseGetPos() uses.  
   ByRef parameters are used, allowing any changes the function makes to affect the original variables.  
   This also allows the function to only get the information requested.  
   If you only need the x and y values and don't include `&hwnd` and `&control`, the funciton doesn't bother with getting those.  
   This makes it faster than getting all 4 things every time the function is called.  

2. **Use an object**  
   Objects can hold multiple pieces of data, so create an object and add a property for each item.  
   Return the object.
   The built-in function `InputBox()` uses this method.  
   It returns an object containing a `result` and a `value` property.  
   `value` is the string typed into InputBox and `result` is how InputBox was closed.  
   Why do it this way?  
   Because normally you want both of those pieces of data.  
   `value` is the string you asked for.  
   But `result` has to be checked to make sure the user didn't click cancel or "X" out of the window.  
   Otherwise, your code would run like they chose to enter an empty line.  
   Because both pieces of data are normally desired, the function is designed to return both.  
   If MouseGetPos() used this setup, it would return an object that looks like this: `{x:50, y:100, hwnd:1078765, con:'Button'}`  

3. **Separate functions**  
   This is what happened to the v1 `WinGet` command and the many different sub-commands it had.  
   Each sub-command was changed into it's own funciton.  
   Instead of `WinGet, List,` we now have a function called `WinGetList()`  
   As well as `WinGetClass()`, `WinGetPos()`, `WinGetControls()`, etc...  
   If we took this route with MouseGetPos(), we'd get rid of MouseGetPos() and replace it with these four functions:  
   * `MouseGetX()`
   * `MouseGetY()`
   * `MouseGetHwnd()`
   * `MouseGetCon()`
   
   Seems cumbersome and I'm glad this wasn't the path taken.  
   But it was a very good path for WinGet.

4. **Use a class** 
   Classes are designed for grouping variables and functions together.  
   We could create a "mouse" class and make methods and properties specifically to work with the mounse.  
   The `x` and `y` values would be properties that could be both gotten (currnet pos) and set (move to no pos)  
   And the `hwnd` and `control` would be handled with methods.  
   
        m := Mouse()
        MsgBox(
            'x: ' m.x
            '`ny: ' m.y
            '`nhwnd: ' m.GetHwnd()
            '`ncontrol: ' m.GetControl()
        )

5. **Global variables**  
   Make a bunch of global variables and use those to get data in and out of the function.  
   No example for this because *don't do this*.  
   Do literally *any other* option.  
   I'm only including it because it's technically a viable, albeit horrible, way of doing it.  
   Bad coding habit.

### Parameter recap

That covers parameters.  
To do a quick recap of what we just went over:

* Required parameters
* Optional parameters
* Variadic parameters
* ByRef parameters
* ByValue parameters
* Variadic operator and spread operator
* unset, "maybe" `?`, and "or maybe" `??`
* Callback functions
* Required params for callbacks

## Static variables are permanent variables

A big problem people encounter with functions is that variables in functions always get reset.  
When they need a permanent variable, they end up using global variables.  
It's because they haven't learned about making a function variable permanent.  

This is where the keyword `static` comes in.  
You'll see this word used in a few contexts, but no matter what the context is, this definition will apply:

> "Something that is static should persist through the life of the script."  

Meaning "static things are never deleted/destroyed/released".  
There's a section later that 
If you can remember that, it'll help make sense of all static things in AHK, including upcoming parts.  

### Creating and using a static variable

To make a static variable, we create a variable as normal but we prefix it with the keyword `static`.  
This tells AHK the variable shouldn't be deleted, so when that "cleanup" part comes, it doesn't get erased.  
It's saying "this varaible should persist through the life of the script."  
We'll discuss **how** static variables are handled in the next section.  

Let's create some code to demonstrate a static variable in action against a normal one.  
We'll make two functions, both with a `count` variable.  
Calling a function should increment `count` by one and then display count.  
The only difference is the count2() function will be using a static variable.  

    ; Press each a few times
    F1::count1()                ; Doesn't keep track of count
    F2::count2()                ; Keeps track correctly
    
    count1() {                      
        count := 0              ; Temporary variable
        count++                 ; Increment by 1
        MsgBox(count)           ; Show count
    }
    
    count2() {
        static count := 0       ; Permanent variable
        count++                 ; Increment by one
        MsgBox(count)           ; Show count
    }

You'll notice every time you press F1, it shows `1`.  
But each time F2 is pressed, the number goes up by 1.  
`1`, then `2`, then `3`, etc... 
In staying true to the definition of static, the variable is presisting through the life of the script.

We've made use of static things multiple times already. I just never brought attention to them.  
If you check the [toggle example](#making-a-toggle-using-boolean-values) from the Boolean section, you'll notice a static function is what tracks the toggle state.

I specifically waited until I had explained static variables before explaining how a function actually works.  
We are ging to skip a little bit ahead to something we cover in the [Classes section](#classes). 

## Reference counting and functions

We've [discussed references](#learing-about-references-dereferencing-and-double-derefs) earlier in the guide.  
To quickly recap, when creating a new variable or object:  

1. AHK asks the OS for some space in RAM.  
2. The OS finds a spot and gives AHK back the memory address.  

That memory address is what [reference counting](https://www.autohotkey.com/docs/v2/Objects.htm#Reference_Counting) is concerned with.  

Another thing to recap is how function parameters are passed "by value" and "by reference".  

* When we pass in a primitive value, AHK makes a copy and the copy is what gets passed in.  
  This is because duplicating primitives is simple and protects the original. 
* When we pass in an object, the original reference to the object is passed in.  
  This is because duplicating objects is too expensive.  

This whole concept of "primitives are handled by value" applies to almost everything in AHK, not just function parameters.  
This includes things like assigning primtives to variables and returning primitive values.

Take the following code for example:  

    x := 1      ; One memory address is made
    y := x      ; Another memory address is made

In the above code, the `1` is loaded into memory.  
The memory address of `1` is then assigned to `x`.  
On the next line, `x` is assigned to `y`.  
Because `x` is a primitive value, the value is copied into a new memory address.  
`x` and `y` now point to separate memory addresses that happen to be storing the same number.  
Changing `x` does not affect `y` or vice versa.  

Now let's do the same with an object.

    obj1 := {}              ; Create new object
    obj1.a := 'Auto'        ; Assign 'a' property to obj1
    
    obj2 := obj1            ; Assign obj1 to obj2
    obj2.b := 'Hotkey'      ; Add a 'b' property to obj2
    
    MsgBox(obj2.a obj1.b)   ; Show that 'a' and 'b' exist in both objects

In this example, an object is created in memory and the address is assigned to `obj1`.  
We add an `a` property to `obj1`.  
Then we assign `obj1` to `obj2`.  
This does not duplicate the object. Instead, it assigns the memory address from `obj1` to `obj2`.  
Unlike the primitive values which created two separate memory addresses, `obj1` and `obj2` reference the same memory address.  

Also, `obj1` has the `a` property and `obj2` had the `b` property.  
But in the MsgBox, we used `obj1.b` and `obj2.a`, to reinforce that `obj1` and `obj2` are the same object.  

This whole example is designed to introduce refernce counting.  
What is the primary purpose of reference counting?  
Script maintenance and keeping RAM cleaned up.  
Reference counting exists is so we know when something can be permanently deleted from the script.  
This prevents unused variables from building up and eating up RAM space.  

The common term for this entire process is called "garbage collection" and it's how AHK keeps a script from building up variables no longer being used.  

Whenever AHK creates a new spot in memory, it tracks that address.  
And along with that address, it tracks how many things in the script are actively referencing it.  
I think it'd be beneficial to visualize this using an object, so let's make our own reference counter (tracker).  
We'll continuously refer to this reference counter visualization throughout the section.  

The address and referenc count are what's normally tracked, but I added a "data type" and "reference name" column to help identify what type of data each memory address is holding and what variables are currently referencing it.

    ; Keeps track of references
    ; reference_counter := {
    ;     ; Address   Count         Type      References
    ; }

We're going to start by making an object.

    obj := {}               ; reference_counter := {
                            ;   Address     Count       Type        References
                            ;   0x1234 :    1           Object      obj
                            ; }

AHK asks the OS for space and gets back a memory address of `0x1234`.  
That memory address is now added to the counter with 0 references.  
The expression continues and the new memory address needs to be assigned to `obj`.  
`obj` now references the memory address `0x1234`, so its reference count increments by one.  

Now create a new varaible and assign `obj` to it:

    obj := {}               ; reference_counter := {
    obj2 := obj             ;   Address     Count       Type        References
                            ;   0x1234 :    2           Object      obj, obj2
                            ; }
    
`obj` isn't a primitive, so it's not duplicated.  
Instead, the *memory reference* in `obj` is assigned to `obj2`.  
Both `obj` and `obj2` now reference the object stored at `0x1234`.  
The reference count for `0x1234` increases because another thing in the script references it.  

Next, we assign a string to `obj`:

    obj := {}               ; reference_counter := {
    obj2 := obj             ;   Address     Count       Type        References
    obj := 'AutoHotkey'     ;   0x1234 :    1           Object      obj2
                            ;   0x5678 :    1           String      obj
                            ; }
    
AHK creates a spot in RAM for the string `AutoHotkey` and inserts the data.  
We'll say the new address is `0x5678`.  
The string address is assigned to `obj`, however, `obj` already exists and has a reference to `0x1234`.  
That means AHK sees that it's removing a referenced and decrements the reference to `0x1234` by 1.  
It then increments the refrence count for `0x5678`.  
`obj2` points to the first object we made at `0x1234` and `obj` points to the new string that was just created.  
1 reference counted for each.

Let's make a new variable and assign `obj` to it.  

    obj := {}               ; reference_counter := {
    obj2 := obj             ;   Address     Count       Type        References
    obj := 'AutoHotkey'     ;   0x1234 :    1           Object      obj2
    my_str := obj           ;   0x5678 :    1           String      obj
                            ;   0x9ABC :    1           String      my_str
                            ; }

my_str will create a new memory address because `obj` is currently set to a string.  
Strings are passed by value, not by reference.  
When copying one string to another, we make a new string in memory.  
We'll identify this new address as `0x9ABC`.  
The address is assigned to `my_str` and the reference count goes up by 1.  

Notice there are 2 separate strings even though both contain the same text.  
The copy is its own string and changing one does nothing to the other.

    ; Proof
    str1 := 'Hi'                ; Make a string
    str2 := str1                ; assign string to another var
    MsgBox(str1 '`n' str2)      ; show both are the same (copies)
    
    str2 := 'Bye'               ; Change string 2
    MsgBox(str1 '`n' str2)      ; Show only string 2 changed

Going back to the prior code, calling a string `obj` is just plain bad coding.  
That's not a "meaningful name".  

OK, but I think calling a string `obj` is dumb. It's not meaningful name and we should do something about it.  
Let's assing the original object back to `obj`  

    obj := obj2

Something new happens here.  
For the first time, we're decrementing something with only 1 reference.  
When `obj` is assigned the original object address of `0x1234`, the previous reference, `0x5678`, had to be reduced by 1.  
When AHK sees something with only one reference left being reduced, it removes the memory address from the reference counter.  
Then it tells the OS the memory address is no longer needed so the OS can assign it to something else.

    reference_counter := {
        ; Address   Count         Type      References
        0x1234  :   2,          ; Object    obj, obj2  
        0x9ABC  :   1           ; String    my_str
    }

So this is how reference counting works in AHK.  

For each memory address, the reference count gets +1 each time a new reference is added.  
Each time a reference is removed, it gets -1.  
And when the last reference is removed, AHK removes the memory address and releases it back to the OS.  

### Garbage collection and functions

If you haven't figured it out yet, reference counting is how the "cleanup" for functions works.  
When we call a function, we're running an "instance" of it.  
Let's use the adder function from earlier in the guide:

    MsgBox(adder(3, 4))
    
    adder(num1, num2) {
        sum := num1 + num2
        return sum
    }

In the above code, when adder() is called, there are three items in the function that are part of reference counting: `num1`, `num2`, `sum`  
Each has a count of 1.  
When the function call finishes, everything in the function is deleted.  
This means all the references get a -1.  
That causes all variables defined in the function to also be deleted.  

> "But what happens with the reutrn value, Groggy?"

Great question!  
And I'll answer that question with a question.  
"What kind of value is being returned?"  
It's a primitive (or number or intger, all are correct) and how are primitives passed?  
By value.  
The memory address storing `sum` inside the function will be different than the memory address that resolves from `adder(3, 4)` and is used by `MsgBox()`, but they'll both be the same value of `12`.  

Back to the function call.  
Being the funciton finished, all variables, including sum, had their reference count reduced by 1.  
That means all three are at 0 which means they are deleted from the reference tracking table and AHK releases the memory back to the OS.  

The "cleanup" part of a function isn't *designed* into the function.  
Functions are self-cleaning because their private nature synergizes with reference counting.  

> "OK, so what if a funciton returns an object?"

Let's alter the adder code and find out:

    numbers := [3, 4, 5]
    MsgBox(adder(numbers).sum)
    
    adder(number_arr*) {
        total := 0
        for num in number_arr
            total += num
        result := {sum:total}
        return result
    }

I modified the adder a little so it works with arrays and objects.  
This provides a slightly more complex way of looking at reference counting, but shouldn't be any harder because the same rules are always followed.

Let's walk through the reference counting of this function.

1. When `adder()` is called, the `numbers` array (an object) is passed in and `number_arr` now references it.  
   There are now two references to that array: `numbers` outside the function and `number_arr` inside the function  
2. On the first line, `0` is created in memory and is assigned to the `total` var.  
   Reference count for this variable is at 1.
   The for-loop starts and `num` is created.  
   `num` will serve as the storage variable for every element's memory address.  
   If an array element is primitive, `num` is assigned a new memory address containing the primitive.  
   If an array element is an object, `num` becomes a new reference to that object and receives the memory address of the object.  
   In either cases, the reference to the item is increased by 1
3. Each loop iteration, `num` loses it's previous memory address (-1 to reference counter) and gains the memory address of the next element (+1 to reference counter).  
   It continues doing this until all elements have been gone through.  
   If every element in the array is primitive, each iteration involves deleteing the previous primitive from memory (it loses its only reference each time) and creating a new primitive to assing to `num` each time.  
   This isn't bad or inefficient. It's just how primitives are handled and it's normal behavior we don't see.  
4. When the loop ends, it deletes the variables it made.   
   Meaning if the code `for index, value in some_arr` finished running, the variables `index` and `value` are deleted and the whatever  they were referencing get a -1 to their reference counters.  
   This is also why those variable names are no longer usable after the loop finishes. They don't exist.  
5. After the loop has finished, we create an object called `result` and store the total in it.  
   The object is made in RAM and the sum:total key-value pair are added to it and the memory address is added to the reference counter.  
   We'll say the address is `0x1234`.  
   The memory address is assigned to `result` and its reference count goes up by 1.  
6. When the return is reached, the memory address is returned to the caller and everything in the function is deleted, getting a -1 to reference.  
   Reference counting is updated.  
   There are 0 references to the object so it SHOULD be deleted, but it's not.  
   Instead, the memory addressed is successfully returned and used.  
   The reason why the object doesn't get deleted is because there is a *specific rule* that prevents this very thing from happening:  
    > Objects created within an expression or returned from a function are now held until expression evaluation is complete, and then released.  
    > This improves performance slightly and allows temporary objects to be used for memory management within an expression, without fear of the objects being freed prematurely.
   
   AHK purposely "holds" that returned object memory address until the expression has fully completed.  
   Meaning that object won't have an opportunity to be deleted until `MsgBox(adder(numbers).sum)` is fully resolved/evaluated.  
7. The last step is to finish evaluating `MsgBox(adder(numbers).sum)`.  
   We took care of the sub-expression. `adder(numbers)` resolvee to the memory address of an object.  
   Next, `.sum` is evaluated, so it access the "sum" property of that memory address.  
   Think of it like this: `0x1234.sum`, where "0x1234" is the name of the object instead of the address, as they're essentialy the same thing.  
   `0x1234.sum` resolves to the number `12`, and we're left with : `MsgBox(12)`.  
   At this point, the sub-expression has fully evaluated, AHK no long has to hold the memory address, the memory address wasn't assigned to anything, so its count is still 0, and the object can finally be deleted.  
   This all happens after `12` is gotten but before the MsgBox function is called.

I want to take this opportunity to point out that AHK does **all of this** for you in the background without your knowledge or intervention.  
You don't need to be actively thinking about this stuff.  

This is to help understand the finer details of AHK and all of the rules and nuances it has.  
It's one thing to write code.  
It's another thing to understand the details behind how your code opearates.  

### Static variables and reference counting

When talking about garbage collection, we have to bring up static variables and how they work with reference counting.  
The thing about that...they work the same.  

> "But Groggy, why don't they get deleted then when the function ends? Don't they lose their last reference?"

Great question!  
The catch is they never lose their last reference. It's impossible due to how things are set up.  

It's important to understand a rule about AHK. You can't delete a function.

    test := 0       ; Error! You can't override test because it's a function

    test() {
        MsgBox('hi')
    }

The static variables we define inside functions ***belong*** to the functions.  
Meaning the function stores a reference to that memory address at all times.  
The function will always keep the reference count at 1.  
If it can't be reduced below 1, it's never deleted.  
If you're wondering "how can a function exist if the function isn't running?".  
*Technically* a function is a type of object. Yes, the functions we use are "function objects"...  
That's why we have a `Func` class. But that's not the point right now.  

The point is that every function "exists" in global space as a function object.  
In the `test` function object is where the reference to the static value is stored.  
And being `test` is a function that cannot be deleted or overwritten, the refrence cannot be deleted or overwritten.  
Each time the funciton is called and an *instance* of the function is ran, the function always gives the same memory address to the static variables in the funciton call, which is why they retain the same value each time.  
That reference in the actively running function is reference **two** for that memory address.  
And when the funciton finishes, that references is deleted, and the reference count for that static variable goes from 2 down to 1 while everything else went from 1 to 0 and being garbage collected. 

### Circular references and memory leaks

There is one big danger with reference counting that should be discussed.  
That danger is called a "circular reference".  

A circular reference is when an object references itself. 
Or, when two objects reference each other.  
The problem with them is that you can create a memory address but accidentally get rid of all your direct references to them.  
They exist in the memory, but you delete the reference to them so you can't reach them.  
This creates a "memory leak", which is a term for describing when data builds up in RAM due to an error in the code.  

If you have ever heard "rebooting fixes lots of stuff", memory leaks are one of them.  
When you reboot, you force everything to start fresh.  
But the leak shouldn't exist at all.

Being a reference counter is just a memory address tracker that counts references, we'll depict one with an object.  
This is our reference counter object, or our "tracker" that we'll be using in this section, with some example addresses added.  

    reference_counter := {
        0x1234: 0,
        0x5678: 0
    }

We're also adding in some comments and a couple extra columns for us to take notes about what each entree is and what it's being referenced by.

    reference_counter := {
        ;Address    Count     Type    Reference
        0x1234:     0,      ; Object  my_obj
        0x5678:     0       ; String  my_str
    }

Let's create a couple different circular references and see how they create memory leaks starting with a self-referencing circulare reference.  
This code demonstrates a circular reference being created:

    obj := {}
    obj.prop := obj
    obj := 0

At first glance, this code might look OK, but writing something like this introduces a memory leak into your code.  
Let's break it down using our tracker.  

1. **Line 1**: `obj := {}`  
   A new block of memory is needed to create a new object.  
   The OS gives us back a memory address for our new object: `0x1234`  
   That address is added to the reference counter.

       reference_counter := {
           ; Address   Count     Type      References
           0x1234:     0       ; Object    
       }

2. That memory address is assigned to `obj`.  
   The memory address now has 1 reference to it.

       reference_counter := {
           ; Address   Count     Type      References
           0x1234:     1       ; Object    obj
       }

3. **Line 2**: `obj.prop := obj`  
   We create an object property and assign a reference to `obj`.  
   This means it has another reference, so let's increase the counter.

       reference_counter := {
           ; Address   Count     Type      References
           0x1234:     2       ; Object    obj, obj.prop
       }

4. **Line 3**: `obj := 0`  
   A zero is created in memory at address: `0x5678`  
   The address is added to the reference tracker.  
   AHK goes to assign the new memory addres to `obj` but notices it has another memory address set to it.  
   It removes 1 from the count for that memory address.  
   Then it assigns the new memory address to `obj` and increase the count for the new address by 1.  
   (Are you seeing the problem yet...?)  

       reference_counter := {
           ; Address   Count     Type      References
           0x1234:     1,      ; Object    obj.prop
           0x5678:     1       ; Number    obj
       }

5. If you haven't figured out the problem, I have two questions for you:
   How many references are currently being tracked?  

       reference_counter := {
           ; Address   Count     Type      References
           0x1234:     1,      ; Object    obj.prop
           0x5678:     1       ; Number    obj
       }

   And how many "items" are in our code do we have control over?

       obj := {}
       obj.prop := obj
       obj := 0
   
The problem with the code is that there is one item we're working with, `obj`, but we have TWO active memory addresses, `0x1234` and `0x5678`.  
The problem all started when we created the property that ended up containing a self-reference: `obj.prop := obj`  
This caused the reference counter to go up by 1.  
But then we deleted our only reference to `obj`, which also deletes our only reference to `obj.prop`.  
And this is the memory leak.  
AHK doesn't realize that `obj` is unreachable now. It only knows there is still one more thing in the script referencing memory address `0x1234`.  
What we've done is essentially burned our bridge to our object.  
There's no way to it and for the rest of the time the script is running, AHK will never delete it and it will never return the memory back to the OS.  

> "It's just a few bytes. Who cares?"  

Is it, though?  
The above code shows a single object with a single property being locked into existence.  
What if the object had a **bunch** of other object references?  
Tens. Hundreds. Even thousands.  
Now ALL of those objects it has a reference to are locked into permanent existence.  
Because a single object that is isolated and can't be reached still has a reference to all these other ones.  
And what happens when another object is created the same way? Such as with a class?  
Each time it's called, another object is being locked into memory.  
And any other refrences THAT object has are locked into memory.

See why this is no joke?  
I would say "self-referencing has to be handled carefully", but I think it's better to say "self-referencing needs to be handeled logically".  
Handling things logically is handling things safely.  
Make sure to always think about the bigger picture.

Let's break down a different instance of ciruclar referencing.  
This is the same basic idea, but it's done when two objects reference each other.  
I'm going to include the tracker to the right of the code.  

1. Let's start by creating two new objects.  
   AHK has to create two new spots in memory and we get back two addresses:

       obj1 := {}              ; reference_counter := {
       obj2 := {}              ;   Address     Count       Type        References
                               ;   0x1234 :    1,          Object      obj1
                               ;   0x5678 :    1           Object      obj2
                               ; }

2. Now we're going to add a property to each object.  
   And the property is going to be a reference to the other object.  

       obj1 := {}              ; reference_counter := {
       obj2 := {}              ;   Address     Count       Type        References
                               ;   0x1234 :    2,          Object      obj1, obj2.prop
       obj1.prop := obj2       ;   0x5678 :    2           Object      obj2, obj1.prop
       obj2.prop := obj1       ; }

3. Next, let's assing something else to `obj1`, like a string.

       obj1 := {}              ; reference_counter := {
       obj2 := {}              ;   Address     Count       Type        References
                               ;   0x1234 :    1,          Object      obj2.prop
       obj1.prop := obj2       ;   0x5678 :    2,          Object      obj2, obj1.prop
       obj2.prop := obj1       ;   0x9ABC :    1           String      obj1
                               ; }
       obj1 := 'Hi'

4. Finally, we assign something else to `obj2`.

       obj1 := {}              ; reference_counter := {
       obj2 := {}              ;   Address     Count       Type        References
                               ;   0x1234 :    1,          Object      obj2.prop
       obj1.prop := obj2       ;   0x5678 :    1,          Object      obj1.prop
       obj2.prop := obj1       ;   0x9ABC :    1,          String      obj1
                               ;   0xDEF0 :    1           String      obj2
       obj1 := 'Hi'            ; }
       obj2 := 'Bye'

5. And we're back to the same problem as in the previous example.  
   We have no more references to the objects that `obj1` and `obj2` referenced.  
   However, still objects still have a reference to each other.  
   And we've lost all of our references to the object so we can never fix the problem.  
   Which brings us to the next topic...fixing the problem.

Circular referencing isn't *forbidden*, but it is something you have to actively be aware of and account for.  

When a circular reference is being used, the proper way to delete it is to remove the property refernces first.  
This can be done by targetting the property individually or by clearing all properties.  
Using the original example:  

    obj := {}
    obj.prop := obj
    obj.prop := 0       ; This step prevents the circular reference from happening
    obj := 0

By assigning a new value to `prop`, we remove the reference to `obj`.  
This lowers the reference counter for the object `obj` is referencing from 2 to 1.  
Then setting `obj` to 0 causes the count to go from 1 to 0, allowing the object to be deleted.  
That internal reference isn't locking the memory into a "reference limbo".  

Let's fix the other example next.
For this one, you don't need to remove both properties to break the circular reference.  
By removing either `obj1.prop` or `obj2.prop`, the cicrular reference will be broken.  
I've included the reference counter with all the address used and their end reference count.

    obj1 := {}              ; reference_counter := {
    obj2 := {}              ;   Address     Count       Type        References
                            ;   0x1234 :    0,          Object      <MEMORY FREED>
    obj1.prop := obj2       ;   0x5678 :    0,          Object      <MEMORY FREED>
    obj2.prop := obj1       ;   0x9ABC :    0,          Number      <MEMORY FREED>
                            ;   0xDEF0 :    1,          String      obj1
    obj1.prop := 0          ;   0x1111 :    1           String      obj2
    obj1 := 'Hi'            ; }
    obj2 := 'Bye'

The above code shows our previous "two object circular reference".  
By clearing the reference from `obj1.prop`, the circulare reference is broken.  
Even if `obj2` is deleted first, that reduces its reference count to 0.  
Meaning the object `obj2` references gets deleted which means `prop` gets deleted which means the last reference to the other object is removed and it, too, is released.  
Meaning the object gets deleted from memory.  
Which means its properties are also cleared and that removes the last reference to the other object.  
That reference removal causes the counter to hit 0 and the first object is released from memory.  
Both objects are garabage collected, as was the number 0 that `obj1.prop` was assigned to.  

In the code we only have two variables: `ob1`, `ob2`  
In the reference counter we only have two strings: `0xDEF0`, `0x1111`  

Brilliant!

### What does the word static mean?

Quick bonus fact:  
Static is from greek:  
"statikos" meaning "to stand".  
This evolved to become synonymous with something being "fixed", "unmoving", or "unchanging".  
And that's what a static variable is. An unchanging or fixed variabled.  

## Optional parentheses and function call statements

I'm writing a section on this topic for the sake of education.  
I want to preface this section by saying I think function call statements are a bad coding habit and I don't condone using them.  

That being said, let's discuss what these are, what rules they play by, when they can and can't be used, and my own personal reasons why I don't suggest using them.

Function call statements are when you omit the parentheses from a function call.  

    MsgBox('Hello, world!', 'Custom Title', 'YesNo')    ; Function call
    MsgBox 'Hello, world!', 'Custom Title', 'YesNo'     ; Function call statement

The only difference is the parentheses.  
However, removing those parentheses severely compromises the places you can use a function.  
In fact, there are times when you MUST use parentheses.  

This statement alone should be a flag.  
If you find yourself thinking, "Hey, maybe I should just stick with using parentheses", you're in the right mindset.

Function call statements are written one line at a time, like v1 code.  
They come with restrictions and limitations, like v1 code.  
And they *look* like v1 code.  

Rules/use restrictions:  
Function call statements cannot have any other expressions, including other function calls, after it.  
This also infers that it cannot have any other code past it.  
This should be an obvious problem as the entire point of function parentheses are to show ownership.  
Wihtout those parentheses, there's nothing to delimit between the end of the function and beginning of the next part of the code.  
Instead, AHK assumes it's all part of the function call statement and an error is usually thrown.

Let's look at multiple scenarios where function call statements are not supported.  
I'll also include the same code but in working condition just by adding in parentheses.  

Function call statements can't be used inside function calls...

    str := 'AutoHotkeyv2'
    MsgBox(SubStr(str, 1, -2))  ; Yes
    
    ; VS
    
    MsgBox SubStr str, 1, -2    ; No, msgbox doesn't know where substr starts
    
    str := SubStr str, 1, -2    ; No, this an error for multiple reasons
    MsgBox str
    
    ; VS
    
    str := SubStr(str, 1, -2)   ; SubStr() REQUIRES parentheses
    MsgBox str                  ; Why use parentheses on one line and not the next?

Function call statements cannot be used with if/else...

    if MsgBox'Continue?',,'YesNo' = 'yes'       ; No! Error!
        MsgBox'Yay!'                            ; No! Error!
    else MsgBox'Boo!'                           ; No! Error!
    
    ; VS
    
    if MsgBox('Continue?',,'YesNo') = 'yes'     ; Yes!
        MsgBox('Yay!')                          ; Yes!
    else MsgBox('Boo!')                         ; Yes!

They can't be used with return statements...  

    MsgBox test                 ; Nope x2

    test() {
        str := '===AHK==='
        return Trim str, '='    ; Nope
    }
    
    ; VS
    
    MsgBox(test())              ; Yes x2

    test() {
        str := '===AHK==='
        return Trim(str, '=')   ; Yes
    }

How about using one with a for-loop...

    for value in StrSplit 'test'    ; Nope!
        MsgBox(value)
    
    for value in StrSplit('test')   ; Yes!
        MsgBox(value)

To wrap this up, you can write function call statements if you want to, but I don't ever advise using them.  
Above are multiple examples of when you **must** use them, so if you have situations where you must use them, why not just use them all the time and make stuff look uniform?  
And *not* like v1 code.  

A phrase I constantly tell people is:

> "Always use parentheses and you're never wrong."

It's true because there is **no scenario** where a function call can't replace a function call statement.  
The inverse is not true. There are many places a function call statement can't be used but a function call can.

I'm also going to take this opportunity to say that function call statements are one of my **biggest** complaints about the v2 docs.  
This format is used *whenever possible* in the docs and whoever decided to use this format made a very stupid choice.  
I don't care if Lexikos himself made the decision because it was not a good one.  
This actively promotes, encourages, and even emphasizes that using function call statements is the "correct way".  
To back this up, I've seen MANY posts on the subreddit and forums where a user will specifically state "I was just writing it like it shows to write it in the docs."  
No good comes from this and if anyone with say-so in the docs reads this, please change it. Or let me change it. I volunteer to do it. I will go through the whole docs and add parentheses to ever function call.  
Except for the section that teaches you that it's an option. A demonstration of it is acceptable.

OK, I'm done with this topic.  
(Use those parentheses!)

## Nested functions

We've learned quite a bit about functions.  
Now we're going to learn that functions can be defined INSIDE of other functions.  
This makes a nested function.  

    my_func() {
        nested_fn('hello')          ; Call nested()
        return                      ; End of function code
        
        nested_fn(msg) {            ; Nested function declaration
            MsgBox(msg)             ; Nested function code
        }
    }

Nested functions are owned by the function they're defined in.  
This makes them private. They are not global.  
Only the function that owns the nested function can use it, or even see it.  
This is a major benefit because it helps us follow that unwritten rule about minimizing things in global space.  

Use nested functions whenever you can.  

When should they be used?  
Whenever you need to break down code inside of a function.  
Remember, one of the benefits to using functions is the ability to divide and conquer.  
If a funciton looks like it's getting a bit complicated or overly complex, or there are any parts that repeat themselves, it's a great time for nested function.  
That allows you to take a block of code and give it a name without introducing another functions into global space.  
This also groups the code together, making things cleaner and easier to navigate.  

When SHOULDN'T they be used?  
It would be a bad idea to make a nested function if the code is something that other functions need access to.  
This would involve every function having its own nested function that does the same thing.  
Instead, the function should be declared in global space so everything that needs access to it can get access to it. (Or a class would work, too!)  
The unwritten rule of global space is to **minimize** the things in global space, not completely avoid global space.  
Global space is there for a reason and should be used when warranted.  
A function that multiple other things need access to **belongs** in global space.  

### Nested function scope

It's important to remember that functions can "see out" but nothing else can "see in".  
This applies to nested functions, too.  

The nested function can "see out" into the function that owns them, including being able to see all the variables and other nested functions contained in the outer function.  
It can also "see out" into global space.  
All of those things are in scope for the nested function.  

But nothing from the containing function can "see into" the nested function because it's private and out of scope.  

However, the differences between each nested function type come from what things they can see and interact with.

### Free variables, closures, and static functions

A term we need to learn about is `free variables`.  
Normally, a variable is considered a free variable if it is accessible to a function but not defined inside that function.  
AHK's definition of "free variable" differs slightly.  
In AHK, a free variable is any variable defined inside of a function that a nested function can access.  
In other words:  

* A free variable is a variable that a function has access to that is not defined inside that specific function.
* Things from global space are not considered free variables.

We need to understand free variables because they're what separate a closure from a static function.  

* **Closure**  
  A nested function that accesses a free variable is a closure.  
  This is a basic exmaple of a closure.  
  The fact that `closure_fn()` access the `x` defined in the `outer()` function is what makes it a closure.  
  It's "bound to a set of a free variables" as the documents say.
  
      ; Example code for a closure
      outer()
      
      outer() {
          x := 'Default value.'                       ; Create a local variable
          MsgBox(x)                                   ; Show it
          closure_fn()                                ; Run closure
          MsgBox(
              'x value: ' x                           ; Show updated local variable value
              '`nInner() type: ' Type(closure_fn)     ; And show type is closure
          )
          return
          
          closure_fn() {                              ; A closure accesses something from a containing function
              x := 'Updated by inner!!'               ; This line is why it's a closure
          }
      }
    
  These nested functions get their name from the fact that they "close over" the entire function, capturing free variables for use.  
  If a reference to a closure is maintained, that instance of the function call isn't closed because the closure needs access to the  free variables.  
  This is what makes it a closure.  
  Keeping a reference to everything means nothing gets released prematurely before the closure is finished being used.  
  
* **Static function**  
  To create a static function, the `static` keyword can be used before the function name.  
  This forces the function to be a static one instead of a closure.  
  Static functions are allowed to access other static functions and static variables.  
  The other way a static function can be created is by defining a normal static function and not using any free variables.  
  This is the same way a closure is written, with the only difference being a closure accesses a free varaible.  
  
  When differentiating between the two types of static functions, I like to use the terms "explicit" and "impliclit".  
  
  * An explicit static function is a nested function defined with the `static` keyword.  
    An explicit static function cannot access any free variables because free variables do not exist to it.  
    
  * An implicit static function is a nested function that doesn't use the `static` keyword and doesn't access any free variables.  
    It *can* access a free variable, but if it does, it becomes a closure.  
    This is the core difference between explicit static functions and implicit ones, in that explicit ones will throw an error when trying to access a free variable because they are not in scope.
  
  Let's alter the prior example to an explicit static function.

      ; Example code for a forced static function
      outer()
      
      outer() {
          static y := 'static y'                      ; Create a static variable
          x := 'local x'                              ; Create a local variable
          MsgBox('static: ' y '`nlocal: ' x)          ; Show both
          static_fn()                                 ; Call the static function
          MsgBox(
              'x value: ' x                           ; Show local x is unchanged
              '`ny value: ' y                         ; Show static y is changed
              '`nInner() type: ' Type(static_fn)      ; static_fn type is func, not closure
          )
          return
          
          static static_fn() {                        ; Static function (explicit)
              y := 'Updated by inner()'
              x := 'Updated by inner()'               ; This creates a new local variable in the function
              MsgBox(
                  'x value: ' x                       ; Show local x is set
                  '`ny value: ' y                     ; Show static y has been updated
              )
          }
      }
  
  The static function is able to create an `x` variable because it creates it locally.  
  It is not accessing the `x` free varaible provided by `outer()` as that is out of scope.  
  Instead, it creates it's own local `x` variable.  
  Static `y` is accessed without issue because static things are allowed to access other static things.
  
  Next, we'll create an implicit static function using the same prior code.  
  You'll notice that a new keyword is being used: `local`  
  This keyword forces a new local variable to be created within the scope of that function.  
  This will prevent referencing any free variables of the same name.  
  I'll include an example of using this keyword to keep a static function from becoming a closure.
  
  To create an implicit static function, create a nested function without using the `static` keyword.  
  This is the same format as a closure with the only difference being a closure accessess a free variable.  
  
      ; Example code for a forced static function
      outer()
      
      outer() {
          x := 'Default value.'                       ; Create a local variable
          MsgBox(x)                                   ; Show it
          static_fn()                                 ; Call the static function
          MsgBox(
              'x: ' x                                 ; Show x wasn't changed by static_fn
              'Inner() type: ' Type(static_fn)        ; static_fn type is func, not closure
          )
          return
          
          static_fn() {                               ; Static function (implicit)
              local x := 'CHANGED!'                   ; Make an x variable local to this function
              y := 'Some code doing stuff'            ; y is local to here because no y exists in outer
          }
      }
  
  In the above code, we see static_fn is defined and has two variables.  
  It has a local `x` and a `y`.  
  `y` does not exist anywhere in the other containing function, so y is local. 
  `x` is defined as local, so working with it is not a free variable.  
  This is not the same `x` as the one in `outer()`.  
  static_fn() cannot see outer's x because because it is out of scope. It has no reference to it.  
  The MsgBox confirms that `static_fn` is a func, not a closure.
  
So let's talk "good coding habit/bad coding habit".  

If you want to access free variables, you have to use a closure.  
Otherwise, use an explicit static function.  
I don't recommend using implicit static functions as this is more of a fallback than it is something that should be adjusted for.  

When using an explicit static function, you're provided with error detection.  
If you try to use a closure when you don't mean to, then AHK will error out and let you know.  
This is a **good thing**.  

But if you try to use an implicit static function and you *accidentally* use a free variable name in your function, you've made a closure.  
Maybe you're overriding some data that you didn't mean to.  
AHK isn't going to tell you that you made that mistake because it has to assume you wrote things correctly.  
There is no way to catch a logical error like that due to how closures work compared to implicit static functions.  
However, by using a static function, we're making a statement to AHK that, "I do not want to use any free variables."  
If you DO use the same variable name as a free variable, it doesn't matter. AHK makes a local version because those free variables do not exist to a static function.  

Another bonus from using explicit static functions is that you will rarely, if ever, have to use the `local` keyword.  
The only time you would need it is if you wanted to ensure a local variable in a closure for some reason.  

With all that in mind, that's why I consider implicit static functions to be a bad coding habit.  
They have that *possibility* to allow a human error to go uncaught.  
Use closures when you know you need to access free variables.  
Otherwise, use explicit static functions.  

## Naming variables and functions

As a short addition, I'm a big stickler for how people name things and I strongly believe that stuff should have meaningful names.  
If you're smart about how you name your functions and variables, your code will practically describe itself purely by descriptions.  

Two quick things to mention:  

* Variables should be noun-based.  
  It should briefly describe what the contents are.  
  If you're working with prices and taxes, things like `price`, `tax`, and `total` are great variable names.  

* Functions should have a verb or predicate in their name.  
  They're actions and should describe what they do.  
  Such as `GetName()`, `CalculateTotal()`, or `StopTimer()`.  
  Functions that return Boolean (true/false) values tend to use words like "is", "has", or "contains".  
  Such as `IsOdd()`, `HasProp()`, or `ContainsVowel()`. 

# Syntax Sugar: Ternary, fat arrows, and code reduction

In AHK, some of the operators and functionality provided is strictly to reduce coding and provide an easier and more compact way of writing code.  

Two things that are well-known for this are the ternary opeartor and fat arrow functions.  
We're going to discuss both of these.

I will also be discussing the multiple ways code can be reduced, including all the times you can omit curly braces (you will be shocked to find out how many places you can omit curly braces from).  

## Ternary operator

The [ternary operator](https://www.autohotkey.com/docs/v2/Variables.htm#ternary) `?:`, or sometimes `a?b:c`, is a very unique operator in that it's the only ternary operator in the language (and in most other languages).  
That's why it is referred to as **THE** ternary operator.  
While "ternary" is the common term, it goes by other names:  

* Conditional operator/expression
* Ternary-if
* Inline-if (or iif)

This opeartor allows us to make a "decision" with our code, similar to an `if/else` statement.  
However, it is an operator and can be used in expressions.  
This gives it both advanatges and disadvantages over `if/else`.  

### Creating a ternary statement

Earlier we explained ternary means that this operator requires three operands and the symbols `?` and `:`.  
The `?` symbol is used to separate the evaluation from the true result.  
The `:` symbol is used to separate the true result from the false result.  
To write a ternary statement, we use this format:

    expression ? true_expression : false_expression

`expression` is something to evaluate as a Boolean statement, meaning it evaluates to either true `1` or false `0`.  
If it's true, the ternary statement resolves to whatever `true_expression` is.  
And if it's false, the ternary statement resolves to whatever `false_expression` is.  

### if/else vs ternary

A ternary statement performs similarly to an if/else statement in that it evaluates something then runs one branch of code for a true result and another branch of code for a false result.  
Using our previous ternary example `expression ? true_expression : false_expression`, we can rewrite it as an `if/else`.

    if (evaluate)
        true_expression
    else
        false_expression

Both the ternary statement and the if/else statement will produce the same result in this case.  
However, they are not the same when it comes to how and when you can use them.  
There are things you *can't* use inside of a ternary statement, like a for-loop.  
There are also things that `if/else` can't be applied to that ternary statements can, like making an if/else choice inside of an expression.  

Each one has its perks.  
We're going to go through some examples.

Let's create an `if/else` that checks variable `x`.  
If x is equal to one, set `match` to 'yes', else set `match` to 'no'.

    x := 0
    
    if (x = 1)
        match := 'Yes'
    else match := 'No'
    
    MsgBox('match: ' match)

This code works as intended.  
Now let's rewrite it to use a ternary statement instead.  

    x := 0
    
    (x = 1)
        ? match := 'Yes'
    : match := 'No'
    
    MsgBox('match: ' match)

By writing it like this, we can show how it's structured the same as an if/else.  
We removed the `if` and `else`, inserted `?` before the if-true statement, and inserted `:` before the if-false statement.  

We can also choose to write that ternary statement on one line, something an if/else statement can't do.  

    x := 0
    
    (x = 1) ? match := 'Yes' : match := 'No'
    
    MsgBox('match: ' match)

The `match := ` part of the code is being written twice in our ternary statement.  
This is redundant when working with the ternary operator as we can single out only the spot that's changing.  
The expression is `match := ???` where `???` is the only thing that changes.  
In this case, it's going to be the string `yes` or `no`.  
That's the only area we need to apply the ternary operator to.

    x := 0
    
    match := (x = 1) ? 'Yes' : 'No'
    
    MsgBox('match: ' match)

This reduces the code, makes it look cleaner, and it reads easier.  
As shown above, you're allowed to spread out a ternary opeartor.  
This is because all lines that start with an operator are automatically bound to the previous line. (Excped `++` and `--` because they special and have a very logical reason for not being included).  

The point is that when a line starts with `?` or `:`, AHK knows it belongs the ternary statement.    

    x := 0
    match := (x = 1)            ; Evaluate
        ? 'Yes'                 ; Do if true
        : 'No'                  ; Do if false
    MsgBox('match: ' match)
    
    ; Example of a more complext ternary setup
    ; Or what if you're doing a double evaluation?
    x := 10, y := 200
    quadrant := (x < 960)
        ? (y < 540)
            ? 'Upper Left'
            : '

Formatting ternary statements is covered more in the next section.  

`if/else` can be chained into `if/else if/else if/else` statements.  
This applies equally to the ternary opeartor.  
In fact, a ternary can be inside of a ternary which has anohter ternary.  
There is no reasonable limit to how far you choose to chain your statement (though I believe the max operators you can use is something like 57000...you should never have 57000 operators in a single line!)  

We'll use a grading function to demonstarte this.

    ; grade percent
    score := 75
    MsgBox(grade_score(score))

    grade_score(gp) {
        if (gp >= 90)
            return 'A'
        else If (gp >= 80)
            return 'B'
        else If (gp >= 70)
            return 'C'
        else If (gp >= 60)
            return 'D'
        else
            return 'F'
    }

    MsgBox(grade)

We can rewrite that entire code block as a chained ternary statement:

    ; grade percent
    score := 75
    MsgBox(grade_score(score))
    
    grade_score(gp) {
        return gp >= 90 ? 'A' : gp >= 80 ? 'B' : gp >= 70 ? 'C' : gp >= 60 ? 'D' : 'F'
    }
    
Or spread it out so it's more readable.  
Maybe even align values so it's even easier to read and understand.  
This is what separates normal code from sexy code.  

    ; grade percent
    score := 75
    MsgBox(grade_score(score))
    
    grade_score(gp) {
        return gp >= 90 ? 'A'       ; If 90 or above, A
            :  gp >= 80 ? 'B'       ; else if 80 or above, B
            :  gp >= 70 ? 'C'       ; else if 70 or above, C
            :  gp >= 60 ? 'D'       ; else if 60 or above, D
            :             'F'       ; else F
    }

And when we learn about fat arrow functions later, we'll be able to write that entire grading function as a single line.

    ; grade percent
    score := 75
    MsgBox(grade_score(score))
    
    grade_score(gp) => gp >= 90 ? 'A' : gp >= 80 ? 'B' : gp >= 70 ? 'C' : gp >= 60 ? 'D' : 'F'

Let's talk about when ternary can't be used.  
If we need to use any control flow statements, ternary is out of the quesiton.  
They're not usable in an expression and at that point an `if/else` statement is required.  

    arr := [1, 2, 3]
    if arr {
        str := ''
        for value in arr
            str .= value '`n'
        MsgBox(str)
    }

This example can't be done with an expression.  
OK, that's not exactly true. It can be done but it's really messy and there's no reason to do it and you might have to deal with recursion limits in some situations.  
The point is, using a for-loop inside of an expression isn't possible. That's an error.  

    (arr) ? (str := '', for value in arr...uh...)

It can't be done because there's no way to include the body.  

What if a function is called and the first check is a "still running?" check?  
The purpose of something like this is to halt a loop or repetitive operation by returning when a 

    ; Calling this function turns it on and let's the code run once and tells you.  
    ; When it runs again from the timer, it switches off and tells you.  
    ; The fact it uses return stops the thread from reaching the timer and setting itselfa gain.  
    ; It acts as a sentinel.
    fn()
    
    fn() {
        static running := 0
        running := !running
        if !running
            return MsgBox('stopped!')
        MsgBox('running!')
        SetTimer(fn, -1)
    }

This setup cannot be done with a ternary statement as `return` is a control flow statement and those cannot be part of an expression.

    fn()
    
    fn() {
        static running := 0
        running := !running
        
        ; ERROR!!
        ; Return is not OK to put in here
        ; AHK thinks you're using it as a varaible name
        (!running) ? return MsgBox('stopped!') : MsgBox('running!')  
        
        SetTimer(fn, -1)
    }

This fails because the ternary statement thinks `return` is a variable name and that's a protected name, meaning no variable, class, or function can ever be named that.  
That's why this throws an error.  

On the flip side, ternary allows you to reduce and shorten stuff in a way `if/else` statements cannot.  
We already covered this earlier when we were talking about not writing `match := ` twice in the ternary.  
Instead, wrote `match := ` and then put the ternary after it, only dealing with the two alternate values.  
This is just smart use of the ternary operator. It's doing its job by making our coding life easier! That's why it exists.  
We don't need it. IT'S SYNTACTICAL SUGAR!

Let's do another example.  
In the last example we had a "running" variable.  
What if we wanted to write a notification that tells us when something is "on" or "off"?  
Using `if/else`, it would look like this.

    toggle := 0
    
    if toggle
        MsgBox('Toggle is set to: On')
    else
        MsgBox('Toggle is set to: Off')

We could rewrite it using a ternary operator like this.

    toggle := 0
    
    (toggle)
        ? MsgBox('Toggle is set to: On')
        : MsgBox('Toggle is set to: Off')

But look at all that duplicated code we're writing.

    ; The only difference     ↓↓↓↓
    MsgBox('Toggle is set to: On' )     ; true branch
    MsgBox('Toggle is set to: Off')     ; false branch

Instead of using `toggle` determining which MsgBox code block to run, it should be used to determine if `On` or `Off` is shown.  

Let's rewrite this better:

    toggle := 0
    ;                            |--Evaluates to 'Off'-|
    MsgBox('Toggle is set to : ' (toggle ? 'On' : 'Off'))

In this code, only the `on` and `off` values are dealt with.  
This drastically reduces the code and it's clear what's going on.  

### Pros and cons

Pros of ternary:

* Can reducde overall script size as if/else statements can be written on one line.  
* Can be used to make decisions inside of an expression.  
  Meaning it can operate on *parts* of data instead of entire statements.
  This is a huge benefit, when applicable.
* Can be chained together to make if/else if/else if/else chains, indefinitely.  
* Can be used with other opeators and sub-expressions to write entire blocks of code on a single line.  
* All of those things inevitably result in shorter code.  
  Remember that shorter code means smaller file sizes and (usually) easier readability.  
  It does **not** have any correlation with the speed of the script.

Cons of ternary:

* Can be cryptic to those not familiar with it.  
* Can sometimes make an `if/else` statement harder to understand.  
* Chaining too many ternary statements or making statements too long reduces readability.  
  This can also be a cause of more difficult code maintenance.  
* Making elongated single statements with ternary statments requires nesting parentheses and can get messy.  
* Flow control statements cannot be used inside of a ternary statement as they are no types of expressions.  
* (Small con) Ternary doesn't have a concept of "if-only". There always has to be an else
  However, this can easily be a `0` or empty string if you don't want to anything done.  

Readability of the code should always be a consideration.  
Remember that we spend far more time reading code than writing it.  

### Formatting/aligning ternary statements

I've decided to include a bonus section about different ways to format and aligning ternary statements.  
I have three primary ways that I use to align my ternary statements.  

* Inline expression
* Align true and false branches
* Indent true branches

For each example, we'll show a single `if/else` as well as an `if/else if/else if/else` example, following this basic format:

    if (evaluate)
        if_true
    else else_false

    ; and
    
    if (evaluate1)
        if (evaluate2)
            both_true
        else 
            e1_true
    else
        if (evaluate2)
            e2_true
        else
            both_false

#### Inline alignment

Whitespace has no general meaning to an expression, other than when a string uses it.  
Any expression can be written out however you want it to look.  
If you prefer an expression be written on a single line, that's OK to do.  

The code runs correctly because most whitespace is disregarded.  
The syntax of the language relies on the operators and keywords to dictate how things are processed.  
To be clear about whitespace, it **does** have meaning.  
Spaces are required, such as betten a string and a funciton call: `MsgBox('Characters in string: ' StrLen(str))

Readability and maintainability of the code **is** important and should be considered when trying to cram everything onto one line.  
Meaning there are times when putting everything on a single line is a horrible choice that has no benefit other than the coder being able to say "hurr durr durr I was able to do it..."  
Just because you *can* doesn't mean you *should*.  

Example of of inline ternary examples:

    (evaluate) ? if_true : else_false
    
    (evaluate1) ? (evaluate2) ? both_true : e1_true : (evaluate2) ? e2_true : both_false

#### True/false aligned

Spacing out ternary statements to other lines makes it easier to read.  
There are a couple different ways to write these while maintaining readability.  

The first way is to always align your if/else branches, meaning the symbols become aligned.  
This creates a pattern where each evaluation is indented a level, easily identifying which if/else belongs to which check.  

    ; Align true/false branches
    ; Meaning the true and false branches
    ; will always align with each other
    (evaluate)
        ? if_true           ; Both of these branch from "evaluate"
        : else_false        ; Both of these branch from "evaluate"
    
    (evaluate1)
        ? (evaluate2)
            ? both_true     ; These results are if evaluate1 is true
            : e1_true       ; These results are if evaluate1 is true
        : (evaluate2)
            ? e2_true       ; These results are if evaluate1 is false
            : both_false    ; These results are if evaluate1 is false

It easily shows ownership of the statements.  
This format also gives the appearance of an if/else statement where each branch is on its own line.  
Notice that true and false branches are also aligned in this example, just like in the above ternary version.  

    if (expression)
        true_stuff
    else
        false_stuff

#### Arrow aligned

The other way to write ternary statements is to use an "arrow" alignment.  
Every true branch is indented.  
Every false branch is outdented.  
This results in something that resembles horizontal arrows/bumps.  
The deeper the true branches goes, the deeper the arrow becomes
    
    ; Indent true branches
    (evaluate)              ; Start with no indent
        ? true_thing        ;   The true branch is indented
    : false_thing           ; Ends with no indent

    (first)                 ; if first true
        ? (second)          ;   if second true
            ? both_true     ;     Both true branch
        : first_true        ;   Only first true branch
    : (second)              ; if second true
        ? second_true       ;   Only second true branch
    : both_false            ; Both false branch

Notice how it makes an arrow?  

    (first)                 ; Initial evaluation
    >>  ? (second)          ;   true indent
    >>>>    ? both_true     ;     true indent
    >>  : first_true        ;   false outdent
    : (second)              ; false outdent
    >>  ? second_true       ;   true indent
    : both_false            ; false outdent

This format also gives the appearance of an if/else statement where the else-statement is included on the same line as the else keyword.  
Writing code like this creates the same "arrow" appearance as above:

    if (first)
    >>  if (second)
    >>>>    both_true
    >>  else first_true
    else if (second)
    >>  second_true
    else both false

This arrow indentation is beneficial because it tracks if all if/else branches are accounted for.  
Everytime there's an "if", there's an indent.  
Everytime there's an "else", there's an outdent.  
This will always cause a symmetrical effect and should always result in the last statement being on the same level of indentation as the starting evaluation of the ternary.  
In the code above, notice that the first line, `(first)`, and the last line, `both_false`, are on the same level of indentation.  
If an arrow isn't formed, you know an "if" or an "else" branch was skipped or it's in the wrong place. It's visually noticeable.

But the bigger thing to remember here is that when getting to the point where you're losing track of indents, you might want to consider using if/else blocks or a switch statement.  
Readability is always something to keep in mind and cramming multiple things onto one line does not make your code faster. That's not how programming works.  
An entire block of code spanning 100 lines could be x1000 faster than a single line of code, all depending on how it's written and what it's doing.

## Or Maybe

This is going to be a short one, but I wanted to reference back to the "or maybe" operator.  
We already learned about it so no need to double tap.  

`??` is definitely syntax sugar as it's just a shorcut for writing this:

    IsSet(value) ? value : 'Value to use if unset'

These two statements are identical:

    var := value ?? x
    var := IsSet(value) ? value : x

Meaning `value ?? something` is syntax sugar used as a faster, more convenient, more readable way of writing: `IsSet(value) ? value : something`

The coalescing operator becomes a lot less confusing when you realize it's just a ternary operator with the evaluation and true branch filled in for you.

## Fat arrow functions `() =>`

Fat arrow functions are one of my favorite pieces of syntax added to v2.  
This allows us to define a simple funciton quickly and dynamically.  

Let's look at the basic syntax of it:

    (params*) => expression_to_return

If this was rewritten as a normal function and given a name, it would look like this:

    my_func(params*) {
        return expression_to_return
    }

The fat arrow operator resolves into a function that you can call.  
It's no different than calling `MsgBox()` or `adder()`.  
Speaking of adder, let's bring it back for an example.  
Here's the original code:

    MsgBox(adder(3, 4))

    adder(num1, num2) {
        return num1 + num2
    }

Let's convert it to a fat arrow function:

    MsgBox(adder(3, 4))
    
    adder(num1, num2) => num1 + num2

Easy, right?  
The key difference between a fat arrow function and a normal function is a fat arrow function doesn't have a "body" to run code.  
The value after the fat arrow is a single expression and whatever it resolves to is returned.  
This is why control flow statements like `loop`, `if`, `try`, and `return` can't be used in a fat arrow function. They're not expressions.

Using the adder function, I want to morph it into a fat arrow function.

    ; Normal function
    adder(num1, num2) {
        return num1 + num2
    }
    
    ; Fat arrow functions don't have curly braces
    adder(num1, num2) 
        return num1 + num2
    
    ; The fat arrow operator represents the "return" statement
    adder(num1, num2)
        => num1 + num2
    
    ; Or you could move it all onto one line
    adder(num1, num2) => num1 + num2

The reason both work is because a line starting with an operator is considered a continuation of the previous line.  
There are times when this migth be preferred, such as keeping a line from extending out too far or if the name and parameters are especially lengthy.  
Personally, I like to keep the length of my lines at less than 100 characters.  
There have been many times when moving the arrow down to the next line meant I didn't have to break up my lines.  
    
Fat arrows aren't used exclusively with function definitions.  
They can be used to dynamically create a function within the code.  

Similar to creating a variable, a function can be "assigned", too.  
Choose a unique name then assign the fat arrow function to it.  

This name now becomes a reference to that function.

In the following example, the function is designed to take in any amount of keys.  
It checks each key and if that key is being logically held, it's released, but if the key is already released it holds it.  

    toggle_keys(keys*) {
        ; Dynamically created functions
        ; Hold(key) will hold down a key
        ; Release(key) will release it
        hold := (key) => Send('{' key ' Down}')
        release := (key) => Send('{' key ' Up}')
        
        for key in keys {
            if GetKeyState(key)
                release(key)
            else hold(key)
        }
    }

What the function does isn't the point.  
It's how it does it.  
Two functions have been created on the fly, creating `hold()` and `release()` methods.  
These are used in the code and it makes the code extremely clear about what it's doing.  
"Loop through all keys. If a key state is down, release it, else hold it."  
We could've used `Send('{' key ' Down}')` for hold, but `hold(key)` sure looks a lot better.  

Creating functions whenever you need them is an *extremely* useful thing and it's why fat arrow functions are such a gerat v2 addition.

### Anonymous functions 

When using fat arrow functions, it's not required that you assign a name to them.  
A fat arrow can be defined without a name and is appropriately called an anonymous function.  

Everything used in the prior sections are types of "named function" because they are assigned some kind of name, allowing them to be referenced later.  
Sometimes a function doesn't need to be called by name.  
Instead, it might be referenced by something like a callback or a hotkey.  
In these cases, no name is needed. Meaning anonymous functions have their place.

An common use for this would be clearing tooltips.  
When `ToolTip()` is used, it shows a message in a small box.  
Normally you only want a tooltip to stay up for a second or two and then close.  
You can easily do that with an anonymous function.  

    ToolTip('Starting script up...')    ; Show a tooltip
    SetTimer(() => ToolTip(), -1500)    ; Set a timer to close it in 1.5 seconds

SetTimer needs a callback. As we discussed in a prior section, a callback is a function that runs at a later time.  
In the tooltip example, we've set a timer to run in 1.5 seconds and the thing it's running is an anonymous function.  
It has no name, but it **does** have a reference due to SetTimer.  
In 1.5 seconds, AHK will be checking its internal timer queue, see this timer is ready, and then run the provided code. Which is calling tooltip with no parameters, thus clearing it.  
Once that happens, the timer is deleted, the only reference to the fat arrow function is removed, and at this point garbage collection takes care of it.  

So when should you use an anonymous function?  
Whenever it's appropriate.  
There is no scenario where you **need** to use an anonymous function. They're available as an option.  
Anything you can with an anon function you can do with a normal function.  

Use fat arrows as the syntax sugar they are when you feel comfortable with them and you can readily identify a good time to use them.  
It's your code and your choice.

### The different types of fat arrow functions

Examples of the different kinds of functions made with fat arrows:

    ; Anonymous fat arrow function
    ; Returns a reference to a function for use.
    (key) => Send('{' key ' Down}')
    
    ; Dynamic fat arrow function
    ; Creates a function whenever needed using code.
    hold := (key) => Send('{' key ' Down}')
    
    ; Fat arrow function definitions
    ; Creates a function definition the same as a normal function.
    ; Much smaller, no curly braces, but at the cost of no function body and no control flow statements.
    hold(key) => Send('{' key ' Down}')
    
    ; Normal function definitions
    ; Anything the above fat arrow functions can do, normal functions can do, except normal functions can do more.
    ; That's why fat arrows are syntax sugar.
    hold(key) {
        return Send('{' key ' Down}')
    }
    
### What fat arrows cannot do

Let's do a quick reminder of what a fat arrow *can't* do.  
A fat arrow function has no body to it.  
Without a body, no control flow statements can be used.  
This includes things like loops, if-statements, returns, for-loops, try/catch, switches, etc.  

That's the major downside.  
No looping.  
No try/catch error handling.  
No access to switches.  

If you need those things, then make a normal function.  
There is nothing *wrong* with using normal functions.  
In fact, a better statement would be:  

> Anything an anonymous function can do, a normal function can also do.  
> However, the inverse is not true, as an anonymous function can not utlize control flow statements.  

Acknowledge that fat arrows are syntax sugar.  
They make writing code quicker and easier but they're not really needed because normal functions work just as well and can do more.  
Fat arrows are more conventient, make for writing tighter code, and allow you to implement anonymous functions for functions that don't **need** to be named.  

Use the right tool for the job! (It's becoming a theme.)

## Parentheses are powerful so use them

Remember to use parentheses (sub-expressions) to your advantage.  
There are many ways that parentheses can help your code.  

In short, parentheses give you total control of exactly how things are done.  
If you want something done first, put in parentheses.  
They can be nested to ensure inner workings are also done in order.  

Not only can they organize and control things, they can be used to fix problems and do stuff that would otherwise not be possible.

Let's start by reiterating that parentheses are considered "sub-expressions".  
Sub-expressions are defined as something that: "override precedence or order of evaluation"  
Multiplication will **always** happen before addition.  
If you need addition to happen first, use parentheses.

    x := (1 + 2) * 3

Simple enough.  

How about bringing our friend, the ternary statement, back into the picture.  
Let's write a function where we can pass in a value and the function makes a popup message saying:

    The value <value> is <true or false>.

The function should plug in `<value>` and show if that value is `true` or `false`. 
The catch is there's a problem with the code.  
Regardless of what's passed in, it says nothing but `true`.  
See if you can identify the problem.  
Bonus if you can also identify a fix by only adding parentheses.

    TrueFalse(1)
    TrueFalse(0)

    TrueFalse(value) {
        if (value is Primitive)
            MsgBox('The value ' value ' is ' value ? 'true' : 'false' '.')
        else MsgBox('The ' Type(value) ' is ' value ? 'true' : 'false' '.')
    }

The problem with this code is all based around the ternary operator.  
Specfically this part: `value ? 'true' : 'false'`  
This code is *supposed* to return "true" if value is true, otherwise it returns false.  
The problem is that this is the expected ternary statement:

    ;--1--|---2----|---3---|
    value ? 'true' : 'false'

The first section is supposed to be the evaluation, the second section is the true branch, and the last section is the false branch.

But because of how the ternary statement was written and how it was mixed in with the other text of the MsgBox call, AHK has no way to differentiate between what part belongs to the ternary statement and what part belongs to the function.  

Instead, AHK treats **everything** inside the MsgBox() parentheses as one giant ternary statement:

    ;---------------1---------------|---2----|-----3-----|
    'The value ' value ' is ' value ? 'true' : 'false' '.'

Because of this, the evaluation will **always** be true because there will always be characters in the string.  
This causes the ternary statement to always evaluated to `'true'`, which is what we when we ran the test, including when passing a false value in: `TrueFalse(0)`  
Not only did this compromise the evaluation, it also caused the first part of the message to get "eaten" by the evaluation.  
`'The value ' value ' is '` is supposed to be displayed, but that doesn't happen when it is considered part of the ternary evaluation.

To fix all this, the only thing needed is some parentheses.  
The ternary statement needs to be turned into its own sub-expression so that it can evaluate properly.  
In other words, isolate it so it can do its job.  

    (value ? 'true' : 'false')

The ternary evaluates to true or false and that gets plugged into the MsgBox text, giving the desired result.  
The first part of the message is shown correctly and value is properly evaluated:

    TrueFalse(1)
    TrueFalse(0)

    TrueFalse(value) {
        if (value is Primitive)
            MsgBox('The value ' value ' is ' (value ? 'true' : 'false') '.')
        else MsgBox('The ' Type(value) ' is ' (value ? 'true' : 'false') '.')
    }

All fixed by simply putting parentheses around the statement that needed to be evaluated first.  



















Another thing parentheses can be used for is turning multi-statements into a single expression.  
You can transform complex and lengthy blocks of code into a single statement by using ternary statements, parentheses, mutli-statements (comma operator), and fat arrow functions.  

Take this chunk of code I randomly cobbled together.  

    x := 10
    y := 19

    if (x > 7 && y < 20)
        if IsBetween(x, 0, 100)
            MsgBox('valid x!')
        else MsgBox('invalid x!')
    else MsgBox('x and y do not meet threshold')

    IsBetween(num, low, high) {
        if (num < low || num > high)
            return 0
        return 1
    }

It has variable declarations, if/if else/else blocks, and a function definition.  
The entire thign can be reduced down to a single line of code (if we care enough to do so).  
The starting values are already expressions and can be moved to the same line:

    x := 10, y := 19

The function can be rewritten as a fat arrow function inside the expression:

    IsBetween := (num, low, high) => (num < low || num > high) ? 0 : 1

(We'll talk about fat arrows more in the next section.)

All the if-else parts can be reduced using a ternary expression:  

    (x > 7 && y < 20)
        ? IsBetween(x, 0, 100)
            ? MsgBox('valid x!')
        : MsgBox('invalid x!')
    : MsgBox('x and y do not meet threshold')

And now all of those parts can be put into a single multi-statement, separated by commas (hence it being called the multi-statement operator):

    x := 10, y := 19, IsBetween := (num, low, high) => (num < low || num > high) ? 0 : 1, (x > 7 && y < 20) ? IsBetween(x, 0, 100) ? MsgBox('valid x!') : MsgBox('invalid x!') : MsgBox('x and y do not meet threshold')


That entire block of code is now represented as a single line of code.  

Personally, I'd never write code like this for the multitude of reasons already mentioned.  
Just because it *can* be done doesn't mean it *should* be done.  

The fact still remains that you can compress almost any code onto a single line if you want to.  
It's not until you need to use something like a loop or another specific control flow statement that you are required to break.  
Loops aren't even a deal breaker, as in a lot of cases you can create a fully functional loop via recursion.  
That's not to say you **should** do this, I'm merely pointing out that not even the need of a loop is a hard-stop for being able to put entire code blocks on one line.

It's ultimately your choice if you want to write a bunch of code on a single line, but I suggest that you be reasonable about it and be able to acknowledge when it's getting unruly.  
It might be technically correct, but that doesn't make it a best choice.  
Sacrificing readability and maintainability in trade for nothing other than bragging rights about being able to put all the code on one line isn't a good trade.  

Another example of when wrapping things in parentheses is when using expressions inside of expressions.  









One last bonus with parentheses is that if you wrap an entire statement in parentheses, you now have a single expression.  
That expression can be used in places that a multi-statement can't be used, such as fat arrows.  





## Ways to remove excess curly braces

You would be surprised how often you can omit curly braces from code.  
There are only a few times when they're *required*, and if you understand this you can really reduce your code and clean things up by omitting needless curly braces.  
I talked about ternary and fat arrows purposely before this topic because they help play a big role in this.

Curly braces have two main purposes in AHK.  

* To define code blocks, such as function code blocks, loop code blocks, and if/else code blocks.
  
      my_func() {
          loop {
              if (A_Index < 10) {
                  continue
              } else {
                  Break
              }
          }
      }
  
* Curly braces are also used to create object literals
  
      obj := {a:'Alpha'}

We don't want to get rid of object litearls. We love object litearls!  
They're the reason we don't have to use the `Object()` class and also how we're able to define properties at object creation.  
So we'll function on the others.  

### Control flow can usually omit code blocks

In many languages, AHK included, there's a rule about control flow statements like loops, if/else, try/catch, etc.  
These do not REQUIRE curly braces unless multiple statements are being used.  
Meaning both of these are a valid way of writing a loop

    loop 5 {
        MsgBox(A_Index)
    }
    
    loop 5
        MsgBox(A_Index)

Only the next statement is executed.  
So if you have two statements, it won't work.

    y := 0              ; A number to increment and view
    loop 5 {            ; Loop 5 times
        y++             ;   Increment y each time
        MsgBox(y)       ;   And show updated value
    }
    
    y := 0              ; A number to increment and view
    loop 5              ; Loop 5 times
        y++             ;   Increment y each time
        MsgBox(y)       ;   This only shows once

The "multi-statement" `,` operator is how we solve this.  
By using a comma, we can "chain" multiple statements into a single "multi-statement".  
This still counts as *one statement* so curly braces are not needed.  
It's kind of like when you're ordering something and you say "I want x and I want y and I want z..."  
You're doing the same thing with multi-statements.  

    y := 0              ; A number to increment and view
    loop 5              ; Loop 5 times
        y++             ;   Increment y each time
        ,MsgBox(y)      ;   (and then)

Or, sometimes it's cleaner to just put it all on one line:

    y := 0
    loop 5
        y++, MsgBox(y)

To add my personal preference, I like to write things in a list, each starting with a comma.  
It makes it clear that it all belongs to the statement.

    loop 5
        thing1()
        ,thing2()
        ,thing3()
        ,thing4()

Multi-statements apply to many situations.

### If/else statements  

In the previous example, we got rid of if/else curly braces by using a multi-statement.  
Curly braces can also be removed by removing the if/else statement and replacing it with a ternary operator.
As long as control flow is not needed.

    ; Code to choose if yes/no is displayed based on the value of x
    x := 1
    if (x = 1) {
        MsgBox('yes')
    } else {
        MsgBox('no')
    }
    
    ; Same code with if/else replaced by a ternary
    ; No need for curly braces here
    x := 1
    MsgBox((x = 1) ? 'yes' : 'no')

But if a control flow statement needs to be used, ternary is not an option:

    ; This can't be converted to a ternary statement due to the loop
    somevar := 2
    if (somevar = 1) {
        loop 5
            MsgBox(A_Index)
    } else MsgBox('not 1')

### Functions, hotkeys, and hotstrings

Function definitions are another time we use curly braces to define a code block.  
This defines the body where the code goes.

    my_func() {
        ; Code body
        return 'value'
    }

However, if no control flow statements are used, a fat arrow function can be made and the curly braces are not needed.  

    my_func() => 'value'

Fat arrows expect expressions and the ternary operator is an expression.  
That means you can turn a good majority of functions into fat arrow functions.  
Let's make a practical example for this.  
Checking if a value is "between" two numbers is commonly done.  
Make a "between" function that takes in 3 numbers: The number to check, the low end, and the high end.  
Have it return turn true if it falls between those numbers and false if it's out of range.  

    ; A function to check if a number 'is between' two other numbers (inclusive).
    is_between(num, low, high) {        ; Get number, low end, and high end
        if (num > high) {               ; If number is greater than high end
            return 0                    ;   Return false (not between)
        }
        if (number < low) {             ; If number is lower than low end
            return 0                    ;   Return false (not between)
        }
        return 1                        ; Otherwise, return tru (is between)
    }

This works as expected.  
But it's also 8 lines. 9 including the function end brace.  
Let's reduce the if/else first.  
We're returning a value

    is_between(num, low, high) {
        return (num > high) ? 0
            : (number < low) ? 0
            : 1
    }

And put the ternary statement on one line

    is_between(num, low, high) {
        return (num > high) ? 0 : (number < low) ? 0 : 1
    }

We're left with a function that has no body code and only a return statement.  
That's the requirements for a fat arrow function.

    is_between(num, low, high) => return (num > high) ? 0 : (number < low) ? 0 : 1

And we've turned a 9-line piece of code into a single line.  
To be clear, don't ever think "shorter code = faster code". That's not how it works.  
Code reduction like this is done to make things more streamline and cleaner.  

We've applied this "reduction" to functions.  
In AHK v2, hotkeys and hotstrings are functions.  
They're a special type of function, but they're still functions.  
For anyone wondering "why does v2 require curly braces around hotkeys now?"  
This is why. You're making the function body.  

    *F1:: {
        word1 := 'Hello'
        word2 := 'World'
        MsgBox(word1 ' ' word2)
    }

"Fat arrow syntax" is sort of *built into* the design of hotkeys and hotstrings.  
The docs for Hotkeys (General) explains that hotkey syntax does not require curly braces if only one statement is associated with it.  
You don't even have to include the fat arrow.  
Make use of the multi-statement operator

    *F1::word1 := 'Hello'
        ,word2 := 'World'
        ,MsgBox(word1 ' ' word2)

Or put it on one line.  
These are called "inline hotkeys" or "inline hotstrings".  

    *F1::word1 := 'Hello', word2 := 'World', MsgBox(word1 ' ' word2)
    :?*x:/msg::word1 := 'Hello', word2 := 'World', MsgBox(word1 ' ' word2)

One last thing to think about doing is how big is it getting?  
How hard is it to read?  
How difficult will it be for me to edit or update this code?  

You *can* take 60 lines of code (assuming no control flow) and put it on one line, but *should* you do that?  
You have to use good judgment.  
There are times I've reduced code, looked at it, and said "nope, this looks horrible" and undid everything.  
Don't sacrifice readability and maintainability to flex your awesome code compression skills.  

As a general rule I try to teach people about hotkeys and hotstrings:  
Always make inline hotkeys and inline hotstrings.  
Create your hotkey/hotstring and assign a function to it.  

    *F1::do_something()

This keeps the hotkey/hotstring section of you're script really clean and easy to read because there's no code taking up multiple lines between each one.  
If you need to change how a hotkey behaves, go down to its function. (Neat trick in VS Code: Ctrl+Click a function name and it'll take you to its definition).  
And another big reason for using a function call is that other parts of the script can run that code if need be.  
I've seen more than a couple new coders write code directly inside hotkeys and then try to "activate" that code by using the `Send()` command to trigger the hotkey.  
This is a bad idea for **multiple** reasons. Use a funciton.
Code smart, not hard.

## Complex examples using sugar syntax

Earlier in the guide we made toggle example: 

    *F1::{
        my_toggle()                                         ; Make a hotkey and assign a function to it
    }
    
    my_toggle() {
        static toggle := 'Hello'                            ; Create a permanent variable starting as hello
        
        MsgBox('Toggle is currently set to: ' toggle)       ; Announce state before toggling
        toggle := !toggle                                   ; Toggle: Assign to toggle the opposite of toggle. true <-> false
        MsgBox('And after toggling: ' toggle)               ; Show after toggle status
        
        if (toggle)                                         ; Use toggle. If toggle is set to true
            do_true_stuff()                                 ;   run this code
        else                                                ; Else it must be false
            do_false_stuff()                                ;   so run this other code
        return                                              ; end of function
        
        do_true_stuff() {                                   ; Function with true code
            MsgBox('Running true code')
        }
        
        do_false_stuff() {                                  ; Function with false code
            MsgBox('Running false code')
        }
    }

By using a lot of the tricks we just learned, we can reduce it by over half.  
It still does the same thing as before, it's just been rearranged, makes use of fat arrows, makes use of ternary, and has a lot of unnecessary curly braces removed.

    *F1::my_toggle()                                        ; Removed hotkey curly braces
    
    my_toggle() {
        static toggle := 'Hello'                            ; Create a permanent variable starting as hello
        do_true_stuff() => MsgBox('Running true code')      ; Fat arrow function definition
        do_false_stuff() => MsgBox('Running false code')    ; Another fat arrow function definition
        
        MsgBox('Toggle is currently set to: ' toggle)
        MsgBox('And after toggling: ' (toggle:=!toggle))    ; Moved toggle into MsgBox
        (toggle) ? do_true_stuff() : do_false_stuff()       ; Replaced with ternary
    }

# Objects

AHK v2 is an "object-oriented" language.  
Meaning it focuses on creating and using objects.  
It doesn't mean we stop using variables and functions. It just means we focus on using objects.  
So let's discuss what an object really is, why we have them, and how to make use of them.  

## What is an "Object"?

We know a variable holds a piece of data.  
Like a string or a number.

    language := 'AutoHotkey'    ; Assign a string
    ans_to_uni := 42            ; Assign an integer

But what if we want to store multiple pieces of data in one variable?  
Like a variable for storing other variables.  

Objects can do that!

In the most generalized definition, an object is a container.  
This container can hold any amount of values (called properties).  
Don't think of it as a container with a size. It can be as small or as big as needed.  
Just think of it as something that can hold everything that makes up the object.  
It's an empty thing we can add properties and methods to.  

Properties are pretty much variables for an object.  
They're meant for saving data.  

And methods are functions for an object.  
Or rather a function assigned to an object.  
When the function is bound to the object, then it becomes a "method".  
It also gets some bonus features we'll mention in the [classes section](#classes).

So we can say:  
Objects are containers that can contain two things: Properties and methods  
Properties are variables of an object that are used to store data.  
Methods are functions of an object that run the code, or rather perform the actions, of the object.  
And "members" is the term used to describe an objects properties and methods. Those are "members" of an object.  
We'll see that term pop up a few times and it's nice to know that member refers to both properties and methods.  

## Understanding the point of an object

Before we get into this, I want to make a point about objects real quick.  
No one ever really explained to me how they can be used to represent **anything**.  

An object is like a blank canvas or a lump of clay or bunch of building supplies.  
You can make whatever you want with them. They're the start point.  

On a very basic level, they can be used to group things together. Even if the things aren't releated, they can package them up.  
You could call each thing `item1`, `item2`, ..., `item47`, etc.  because it's a container that can hold stuff.  
But you can also use them make *anything* you want.  

I mentioned a lump of clay earlier for a reason.  
A scluptor can take that blob and turn it into an intricate work of art.  
A programmer can take an object and turn it into whatever they need!  

Objects are much more powerful than variables because they allow us to categories and organize things.  
If you add in arrays, you can start representing really complex data structures and even instruction sets.  
Othewrise, if you want to make a simple grouping of objects, objects can do that, too.  

They have many uses and as you read through this you'll start to understand that we take an object and turn it *into something*.  
We tend to not continue calling them objects because we instead think of them and use them as the objects they represent.  
e.g. All arrays are actually "array objects". We don't say "array objects", we just say "arrays".  
The object is the host for the data and how it's managed and used.  

Another big benefit of objects to convey is that they can continue to grow and evolve if you want them to.  
A very simple yet effective example would be if you made a GUI object in your code that acts as a popup.  
You give it some info and it displays it **perfectly** each time.  
Months later, you decide you really dislike the fact that the big edit box that stores the text is white. It's hard on the eyes.  
You *could* go into the code and hard code in a new color.  
But intead, you opt for the ability to set the edit box color to ANY color at ANY time by making it a property.  

You add a `.edit_color` property to it.  

This is responsible for the color of the edit box.  
It doesn't affect anything in the code b/c `edit_color` didn't exist until just now.  
Meaning there are no errors to be corrected.  
And now the only update you have to make is changing the line of code that adds the edit box to the gui.  
Whenver your popup is generated, the new popup will have an edit box of the set color.  

You had a working object.  
You wanted to expand on your object.  
All it took was adding a new property and updating a little code to use it.  
This can be HUGE for writing code and can be used for so many things.  
This helps exemplify why objects are so robust and useful.  

Here's a quick test.  
Before we go any further into objects and explain them, look at this object and see if you can figure out what this mystery object represents.  
I'm betting the vast majority of you will figure it out.

    mystery_obj := {
        title: "The Code Chronicles",
        author: "Alice Syntax",
        publisher: "Binary Press",
        yearPublished: 2023,
        genres: ["Programming", "Science Fiction", "Technical"],
        pageCount: 450,
        physicalAttributes: {
            coverType: "Hardcover",
            dimensions: {
                height: 9.5,
                width: 6,
                thickness: 1.5
            },
            weight: "1.2 kg",
            binding: "Thread-stitched",
            paperQuality: "Acid-free, 100gsm"
        }
    }

Even if you've never seen an object written in your life, the properties of the object make it pretty clear what the object is representing.  
While it started out as just an empty object: `{}`  
It started to turn ito something else.  
By through adding specific properties such as "publisher", "pageCount", and "genres", most of you will have instantly figured out it's a book.  
These are properties that would apply to ALL books.  
That's why it's a book object...or what we'd eventually just call a "book" when referring to it in our code (because it's redundant to call everything an object or we'd call a basic object and "object object".)  

An object isn't about "what it is" when you make.  
It's about "what kind of data it stores" that defines it.

And there is NO RIGHT WAY to create your objects.  
You decide when to use them.  
You design them.  
You choose the type of information they should store.  
You choose the property names.  
You pick the data types.  
It's YOUR object to design.  

PersonA does this:

    person := {
        name := {
            first: 'Groggy',
            last: 'Otter'
        }
    }

PersonB does this:

    person := {
        firstname: 'Groggy',
        lastname: 'Otter'
    }

Who's right? Both.  
Who's wrong? Neither.  

They both made an object that contains a first and a last name.  
PersonA chose to use one property that contains an object and the object contains a first and last name.  
PersonB chose to use two properties to represent the first and last name.  

One person built it one way and one person built it another way.  
Both still have access to the same data and both have logical structure to them.  
And I'd go as far as to say I'd do what PersonB did for smaller projects (because it's simpler) and I'd do what PersonA did for a larger projects (because they always end up expanding and incorporating more data and organization becomes more paramount).  

I **really** wish someone had explained objects to me like this when I was newer to programming.

## When to use objects

**Whenever you want to.**  
There is not a specific time you have to use an object over a variable.  
It's a matter of structure, ease of use, ease of access, and whatever your design plans are.  
We're learning about them so you can use them when you find a need for them.  

*You can design your code however you see fit.*

Do you have a bunch of variables all associated with the same thing?  
Put them in an object.  

Want to return multiple values from a function?  
Put them in an object and return the object.  

Got a single string or number you want to work with?  
That's what a varaible is designed for so use that.  
However, you ***could*** put a single value inside an object and use it that way.  
There's nothing saying you can't do that as it's still data being saved somewhere.  

> "Give us a realistic use of an object, Groggy!"  

OK, you're creating a card game and a player has 5 cards.  
Do you assign each card to individual variables?  

    card1 := 'd1'   ; Ace of diamonds
    card2 := 'h7'   ; Seven of hearts
    card3 := 's13'  ; King of spades
    card4 := 'c3'   ; Three of clubs
    card5 := 's12'  ; Queen of spades

Or do you make a "hand of cards" object containing each card?  

    hand := {
        1 : 'd1',   ; Ace of diamonds
        2 : 'h7',   ; Seven of hearts
        3 : 's13',  ; King of spades
        4 : 'c3'    ; Three of clubs
        5 : 's12'   ; Queen of spades
    }

Realistically, an array would be a better choice here.  
However, this example works great with an object, so we're going with it.  

Would you rather pass five individual variables around:

    score_hand(card1, card2, card3, card4, card5)
    
Or would you rather pass a single object containing all that information:

    score_hand(hand)

Bundle things together logically.  

## Why the words "object", "property", and "method"?

The first time I tried learning about coding went really bad.  
I remember a conversation I had in the ONLY programming class I ever took:  

    Me: "What's a method?"
    Teacher: "It's a function for objects."
    Me: "But why are they called methods if they're just functions? Why the name change?"
    Teacher: "Because they're called methods."
    Me: ಠ_ಠ

This teacher has a core tie-in with why I teach the way I teach.  
More info is always better than no info.  

Also, methods are *like* functions because they *are* functions.  
They become methods when we bind them to the object with a call descriptor.  
This provides methods with the wonderful `this` self-reference variable we keep talking about.  
And if you're going "Huh?" that's perfectly fine.  
This is all covered in upcoming parts of the guide.  

Let's cover some term origins.

### Object - A term for anything

The term object was chosen because it's an extremely vague term for pretty much ***anything***.  
In real life:

* A ball is an object
* A beverage is an object
* A car is an object
* A person is an object
* A planet is an object of our solar system
* A quark is a subatomic object
* A thought is an object of the mind

Anything can be thought of as an object in some way.  
This concept is very applicable to programming objects as they can become ***anything*** by adding properties and methods to them.  

In programming: 
* An autoclicker is an object
* A point (x/y coordinate) is an object
* A user account is an object
* The protagonist of your favorite video game is an object
* Arrays are objects
* Maps are objects
* GUIs are objects

We use the word "object" because it's a great word for describing anything.  
Objects can become whatever we need them to become.

### Property - A term for describing attributes of something

An object is defined by its properties because properties are the things an object is made up of.  
It's the attributes of the object.  
Things like height, weight, speed, color, location, name, age, velocity, x coord, y coord, key state, identifiers, cost, temperature, balance, quantity, origin, and date of creation are all examples of properties some object could have.  
An object can be *anything*.  
A property can *describe parts of anything*.  
Ultimately, properties can be considered the "data" of something.  

Examples of properties from objects (both real and digital):  
- A ball has a radius, a color, a weight, and a manufacturer.  
- A beverage has a flavor, volume, ingredients, temperature, and a color.  
- Earth has moutains, oceans, animals, an atmosphere, a spin direction, a rotational speed, and a movement speed.  
- A GUI object has a height, a width, an x and y position, and a title.  
- An autoclicker has a running status.  

These are considered properties of the objects.  
This is why the term "property" is used to describe the individual attributes of an object.  

Consider a bullet in real life and in a video game:  
Both have a weight, a direction, a velocity, a material, and a type.  
In real life, those properties determine the physics of the bullet.  
Things like the direction it's traveling, how fast it's going, how heavy it is, and how much wind is blowing determines its speed, how quickly it'll drop, how accurate it is, how much damage it'll do on impact, etc.  
In a game, a bullet object would have the same kind of properties.  
Those properties are then used by the physics engine to simulate what would happen in real life.  
With a direction, a velocity, a material, and weight, we can move the bullet realistically.  
The physics engine may cause it to drop by simulating gravity or it might cause it to deviate left or right due to wind being simulated.  

The resulting behavior of the bullet object is dependant on its properties.  

### Method - A term to describe a procedure

The term method means a "procedure, technique, or steps taken to accomplish something."  
In the simplest terms, method means "doing something step-by-step".  
Think "methodology".  
This is why it was chosen instead of something like "object action" or a "object function".  
Though it's extremely helpful to thing of methods as "the actions of the object"...because they are.  
Methods always do *something*.  

And methods exist to serve the object.  
They should always have something to do with the object.  
You wouldn't bind a method to an object that never used that object (edge cases excluded).  

Think about the actions of a real life object and how they would translate to a method:

- A ball can be thrown, so a ball object would have a throw() method. Because "it can be thrown".
- A beverage can be consumed, so a beverage object would have a consume(), or maybe a drink(), method.  
- An autoclicker can be turned on/off so it would have toggle() method to handle that.  
- A GUI can be moved and resized with the Move() method, shown with Show() method, and hidden with Hide() method.  

That is why they're called methods.  
Because you're telling it to "follow some steps" or "follow a procedure" when it's called.  
Hence why it's OK to think of them as "the actions of the object".  

### Fun fact: They're all autological words

Most programming terms, like *object*, *property*, *method*, *function* and *variable* are all used because they're autological words.  
Meaning they are words that describe themselves.  

Think about it. Objects are objects because an object can be used to describe anything.  
A property of an object describes a property of an object. A property *is* a property.  
Methods execute the next steps of code, which is a procedure and the word method *means* procedure.  

This applies to multiple parts of programming:

Loops loop.  
Functions provide some sort of functionality.  
Variables can be a variety of varying things.  
Loops loop.  
Operators operate on things.  
Classes classify things.  
And loops loop.  

## Creating an object and object literals

We're going to learn how to create and use objects.  
There are two ways to create a new object in AHK:

    ; Create a new object calling the Object() class
    obj := Object()
    
    ; Create a new object with object literal syntax
    obj := {}

Going through each one:  

1. [`Object` class](https://www.autohotkey.com/docs/v2/lib/Object.htm)  
    `obj := Object()`  
    Classes are a special type of object designed to *make other objects*.  
    They're core to OOP and have an entire section dedicated to them later.  
    The `Object` class is the class that's responsible for creating the "basic object" of AHK.  
    It is the source (either directly or indirectly) of every single object you'll use in this language.  
    It is what makes **the container** we were talking about.  
    It is the reason we're able to create properties and use methods.  
    Without the Object class, there *is no AHK v2*.  
   
    Calling the class is what generates the standard "object" used by almost everything.  
   
2. [Object Literal Syntax](https://www.autohotkey.com/docs/v2/Objects.htm#object-literal)  
    `obj := {}`  
    Objects are **so important** and used **so often** that they warrant having their own special syntax.  
    Object literals were created to allow easy and quick object creation inside of code.  
    They also work inside of expressions because they are one of the few types of [sub-expression](#sub-expressions-outrank-all-operators).  
    They are evaluated at the same time parentheses, function calls, and other sub-expressions are evaluated.  
    Object literals are not only usable in exprssions, they also provide the benefit of being able to add properties while declaring them, which we'll go over in the next section.  

Regardless of which method you use, the end product is the same.  
You'll quickly realize that object literals are almost universally preferred to calling the Object() class, just based on it taking fewer keystrokes and the bonus of adding in property declaration at creation (something the Object class cannot do).

## Properties

Properties are what we use to store data.  
It can be a string, a number, or even another object.  

The first object we'll be creating is a point object.  
What is a "point"?  
A point is a term for an x and y coordinate pair.  
We use x/y values **a lot** in programming.  
Everything on your screen has to do with coordinates.  
Your mouse position is a coordinate.  
The location of every window is a coordinate (it's actually the upper left pixel of the window).  
Control positioning is done with coordinates.  
Drawing is done with coordinates.  
So "points" are used a lot.  

In this section we're going to manually create point objects and use them for our examples.  
Then we'll eventually make a Point class in the classes section so we can create point objects on demand.  

### The dot `.` is the "member access operator"

When working with properties (and methods), we'll be using a dot between the object and the member name.  
This is called the [Member access `.` operator](https://www.autohotkey.com/docs/v2/Variables.htm#objdot).  
Why member access operator?  
* "Member" because it's the term used for referring to object properties + methods.  
    Objects are made of up members.  
    Members include properties and methods.  
* "Access" because we're making use of, or "accessing", a member.  
* "Operator" because...well, it's an operator.  
    It's actually a binary operator.  
    It requires an object name on the left and a member name on the right, no spaces.  
    That's why `obj. prop`, `obj . prop`, and  `obj.` all throw errors.  

And for a little coding history:  

> Calling properties and methods "members" originates from structs.  
> In low level languages like C, structs are used to store multiple values.  
> They work on the same basic idea of key:value pairs, just like objects do.  
> The concept of a struct is what ended up evolving into the objects we now use.  

### Add a property

To assign a value to a property, you do the same as with a variable.  
Use the assignment operator and pass in a value.  
The only difference is that with a property, you include the object name, too.  

    var := 42           ; Assign a value to a variable
    
    ; VS 
    
    obj.prop := 42      ; Assign a value to a property

Make sure to include the member access `.` operator.  

It's time to create a point object.  
When working with two point values, we'd normally use two variables to store the coordinates.  

    mouseX := 100       ; Assign x to one variable
    mouseY := 250       ; Assign y to another variable

Instead, we should consider using an object.  
This way both the x and y coordinates can be stored to respective `x` and `y` properties.  
This bundles them up into a single package.  

    point := {}                     ; Make a new empty object called point
    point.x := 100                  ; Create an x property and assign a coordinate
    point.y := 250                  ; Do the same for the y coordinate
    MsgBox(                         ; Use the point object as needed
        'x is set to: ' point.X
        '`ny is set to: ' point.Y
    )

In real life, a point is a point because it's an x and y coordinate pair representing a point somewhere.  
In our code, we took an empty, meaningless object, gave it an x and y property, and turned it into something that represents a point.  
It was turned from an object into a "point object".  

When this point is needed, only the object needs to be passed.  
The x and y properties are expected because that's something a point should have.  
For the x coordinate, use `point.x`.  
And for y coordinate, use `point.y`.  

Now that we have this new point object, we can use it in the code at a later time.  
Now we can click at that point when required.  

    if exit_option_showing()
        Click(point.X, point.Y)

* Quick tangent: Normally, I comment code, but notice that I didn't **need** to comment this code.  
    You can read this snippet of code with **no** coding background and you'd still have a pretty good idea of what the code is doing.  
    Just by virtue of being able to read.  
    
    This is why I tell people to choose meaningful and intelligent names for their variables, functions, properties, etc...  
    It creates self-documenting code or code that describes itself and what it's doing.  
    
    > "An exit option of some type is showing and the code is clicking at some x/y coordinate."  
    
    It's obvious b/c it's stating everything accurately (though vaguely) through naming conventions.  
    When you're smart about it and you use well-chosen, descriptive, and preferably *shorter~ish* names, the need for commenting drops drastically from the code documenting itself.

Have you noticed that everything is an object but we don't really say object that much?  
When a new array is created, it's a new *array **object***.  
But we don't normally call them "array objects". We say "arrays". Including "object" seems redundant.  
When we're talking about basic objects (which are technically Object objects!), then yeah, we call those objects.  
For everything else, we drop the extra "object" part and just refer to it as the thing it represents.  
We'd say "make an array" or "create a GUI" or "assign a new point".  

### Add properties when creating an object

A big benefit of object syntax is being able to define properties when creating an object.  
It's one of the many reasons we have this separate syntax and it's why people almost always prefer `{}` over `Object()`.


Object literal rules:  

1. Must start with an open curly brace `{` and end with a closing curly brace `}`.

2. Property names must be unquoted.  
    It is NOT a string. It's an [AHK name](https://www.autohotkey.com/docs/v2/Concepts.htm#names).  
    These are the same rules that variables, functions, and classes follow.  
    Actually, properties have fewer naming restrictions than classes, functions, and variables.  
    A property can start with a number and it can be the same name as another function, a flow control statement, or other forbidden words.  
    This is because properties are inside something and are not restricted to the names in global space.  
    But they do still have to adhere to things like max length and character restrictions.  
    
3. A colon is used to separate the property name from the value.  

4. Each set of properties must have a comma between them.  

This showcases how certain naming restrictions do not apply to properties and methods.  

    obj := {1:1, for:'b', if:'else', A_Index: 42, in: 'test'}

Let's go back and recreate our point object.  
This time we'll create and assign properties using object litearl syntax.

    point := {x:300, y:500, name:'Options'}

It's a simple format that you'll use frequently and get used to quickly.  

### Whitespace in AHK

Tabs and spaces have no meaning to AHK outside of strings.  
Putting one space between two items is the same as putting 20 spaces between it, or a tab, or 5 tabs.  
It's all whitespace to AHK and any excess whitespace is stripped out of the code when AHK runs the script.  

Parentheses `()`, curly braces `{}`, and square brackets `[]` are also used to "group" things.  
Notice these are the symbols used by all the sub-expressions.  
`{They} (enclose) [code].`  
Because they have opening and closing symbols, this marks their start and end.  
AHK acknolwedges this and allows you to use line feeds `` `n `` and carriage returns `` `r `` freely inside the code *without needing to start the line with an operator*!  
You'll see me use this frequently with MsgBox examples.

    MsgBox(
        'First line.'
        '`n<-- line feed character (Can`'t see in msgbox)`n`n'
        'Multiple`nline breaks`nin one line`nof code.'
        '`nOr one line of text '
        'spread over multiple '
        'lines of code.'
    )

AHK doesn't care about that whitespace and how we use it to make the code more human-readable.  
When AHK gets ready to process that code, it'll strip out all the unnecessary stuff and we're left with something that looks like this.

    MsgBox('First line.`n<-- line feed character (Can`'t see in msgbox)`n`nMultiple`nline breaks`nin one line`nof code.`nOr one line of text spread over multiple lines of code.')

Earlier I mentioned that inside of a sub-expression you didn't have to start the line with an operator.  
That's a rule I don't think I've mentioned.  
You can make any line continue onto the next line if it starts with an operator.  
So let's say you want to spread a string out over two lines.  

    str := 'hello'      ; Small problem
        ' world'        ; <-- This line is an error
    MsgBox(str)         ; A primitive can't be on a line by itself

Instead, you would start the line with an operator.  
In this case, you're working with two strings, so the concatenate `.` operator would be used.  
Yes, this operator DOES have an actual use other than being a 100% optional operator between two strings.  

    str := 'hello'
        . ' world'      ; This works fine
    MsgBox(str)

You can use it with other opeartors
    
    total := 8          ; This is OK, too
           + 7
           - 4
           + 9
    
    MsgBox(total)

### Make object literals more readable

Understanding whitespace better now, this can be applied to objects.  
Sometimes you'll add multiple items to an object when you create it.  
Instead of defining them all on one line, space them out.  
This makes it more readable and doesn't affect the code in any way.  

    ; It's OK to put properties on their own lines
    ; As long as we follow object literal rules
    point := {                  ; ✓ Curly braces
        x:100                   ; ✓ No quotes around property name
        ,y:250                  ; ✓ Colon between name and value
        ,name:'Options'         ; ✓ Comma between each set of properties
    }

We can make the object even more readable by adding more whitespace and aligning each column.  
This results in the properties, colons, and values all becoming aligned.  
This produces cleaner looking code.  
Also, notice that I moved the commas. Why? To show you that it can be done.  
It does not matter where the comma is or what whitespace is used between each item.  

    ; You can even align text
    point := {
        x    : 100,
        y    : 250,
        name : 'Options'
    }

Not only does this make it look nicer, but it can be useful to do this.  
A feature of VS Code is the ability to work with multiple lines (cursors) at once.  
This makes it easy to copy/delete/move entire blocks of data when they're aligned like this.  
In VS Code, try middle clicking and dragging the mouse.  
You'll see a "box" of text selection.  
There's also the incredible alt+ctrl+up/down hotkey.  
This is something people love learning about as it allows you to extend your cursor up and down rows, creating multiple cursors.  
This can be used for a **multitude** of reasons and once people know how to do this, they find many uses for it.  
Bonus tips:  
Remember that when working with multiple lines, shift still highlights and control still moves by word.  
The multi-cursors also respect the "home" and "end" keys, which can be great for "aligning" your cursors back together.  

Back to spacing out objects.  
If we take spacing a step further, you can put each value on the next line down.  
It's all preference.  
If you like how this looks, write your objects this way!

    point := {
        x:
            100,
        y:
            250,
        name:
            'Options'
    }

All of the above objects are valid and all are identical to each other.  
They produce the same object with the same properties and same values.  
The only difference is how the user chose to add whitespace and how they wanted to format the code.  

Speaking of whitespace, when does it get removed?  
When AHK is given a script to run, it does a lot of "pre-run" stuff.  
One of the steps it takes is stripping all unnecessary/meaningless whitespace out of the script.  
All the examples shown above will end up looking identical when scrubbed:

    ; How all the above objects will end up
    ; Only mandatory white space is preserved
    ; In this example, no mandatory whitespace is needed
    point:={x:100,y:250,name:'Options'}

### Using a property

An object property can be used anywhere a variable can be used.  
There's nothing special to using it and we've kind of been doing it already.  
But to be clear:

    obj := {}               ; Make an object
    obj.test := 'Hello'     ; Assign a property
    MsgBox(obj.test)        ; Use the property

or

    numbers := {}
    numbers.1 := 30
    numbers.2 := 12
    sum := numbers.1 + numbers.2
    MsgBox(sum)

### Properties can contain objects

So far we've only shown primitive properties (numbers and strings).  
A property can also be another object.  

Going back to our point object, let's say we have multiple points to work with.  
Instead of having multiple individual point objects, we can use a single object to bundle all the points together.  
Make a new object.  
Each property name should be the "spot" the point represents.  
And the value is a point object.  

    ; Create an object of objects:
    points := {
        exit_button : {x:550, y:20},
        menu        : {x:10, y:10},
        menu_new    : {x:10, y:35},
        save        : {x:200, y:50}
    }
    
    ; Use objects when needed:
    Click(points.exit_button.x, points.exit_button.y)

You've used one object to give organization and order to a bunch of other objects.  

Or maybe you want to create an object with more in-depth information.  
Here's an object with the properties of a banana.  
Banana object!

    banana := {
        group   : 'Fruit',
        species : 'Cavendish',
        color   : 0xFFE135,
        length  : 7.5,              ; In inches
        nutritional_content: {      ; In mg
            vitamins: {
                C : 10.3,
                B6: 0.4
            },
            minerals: {
                potassium: 422,
                magnesium: 37
            }
        }
    }

An object can have as much information as you want.  
There's no (realistic) limit to how many properties you can add.  
But make sure the information has a purpose.  
Do you need to know the nutritional content of the banana for your code to work?  
If not, don't include stuff like that.  
That's needlessly taking up space and it adds confusion as it serves no purpose.  
People looking at the code will be wondering "Is that nutritional content info ever used...?"  

But if you **can** use it, then include it!  
You can include a LOT of information.  
Eventually, you might end up with an object that [looks like this car object](https://pastebin.com/HJP2FWC8).  
It's OK to use complex objects like that as long as you understand the object's layout and your code is designed to use it correctly.  

### Built-in properties

There is only one built-in property that objects have and it happens to be one of the most important properties in the entire language.  

Object is what provides the `Base` property to everything.  
That's because everything in AHK derives from some class and every class is a type of object.  
Meaing **everything** in AHK has a `Base`.  

This property is unique and special in MANY ways, including:  
* It is protected and can only be updated if it meets certain requirements.  
* It can't be deleted, as it would break the object.  
* It's not considered an "own prop" even though it's in the object.  
* It's one of the only names that can't be used as a property name as it's the only property name guaranteed to be in any given object as it can't be deleted.  

`Base` is going to be covered in the classes section.  
How it works, why it can't be deleted, how it is directly responsible for inheritance, and how the prototype chain works will all be covered.  

### Own properties

A new concept in v2 that people sometimes struggle with is the concept of an "own property" or an "own prop".  

The easy way to think of "own props" are properties added after the object is created.  
They are properties uniquley "owned" by that object.  

For example, if you create an array object, it has a `Length` and a `Capacity` property.  
These are not "own props" because they are not "owned" by the newly created array object.  
Instead, `Lenght` and `Capacity` are inherited, meaning that array object has *access* to them.  

How this works is revolves around something we haven't discussed yet called the "prototype chain".  
Right now is not the place to expound on this topic. It'll be discussed more in the classes section.  
But I chose to mention it because it *does* explain why own props are own props.

When you make a new object, you're getting a relatively empty object.  
The only things inside of a new object are its `Base` property and its `__Class` property.  
Other than that, there's nothing else.  

Let's create a new array.  

    arr := []

This is how I used to think a new array object looked on the inside.  
I thought it had all the methods and properties it inherited. Kind of like this:

    arr := {
        Clone()
        Delete()
        Get()
        Has()
        InsertAt()
        Pop()
        Push()
        RemoveAt()
        __New()
        __Enum()
        
        DefineProp()
        DeleteProp()
        GetOwnPropDesc()
        HasOwnProp()
        OwnProps()
        
        GetMethod()
        HasBase()
        HasMethod()
        HasProp()
        
        Base
        Length
        Capacity
        Default
        __Item
    }

Come to find out that I was very wrong.  
Instead, this is what you actually get:

    arr := {
        Base: Array.Prototype,
        __Class: 'Array'
    }

As far as AHK is concerned, `Base` and `__Class` are system-used properties.  
These are "own properties" of the object, however, they are used by the system so it ignores them.  
Meaning when you create a new array, if you disregard those two system properties, the object is empty.  
It has no owned properties.  

Let's prove this using an array object.  
We're going to check four different properties: `Base`, `__Class`, `Length`, and `my_prop`  

* All objects have a `Base` and a `__Class` property.  
* Array objects have access to the `Length` property.  
* And we will add a user-defined property, too.  

There are three different methods to use here.

* `HasProp(name)` will return true if the object has access to the specified property. This includes access through the protoype chain (inheritance).  
* `HasOwnProp(name)` will return ture only if an object **owns** the specified property. This means the prototype chain is excluded.  
* `OwnProps()` can be used with the for-loop to loop through all "own props".  
AHK does not include `Base` or `__Class` when enumerating OwnProps, even though they **are** considered own props of the object.  
Again, AHK knows these are properties used by the language, so it ignores them.  

Run this code and let's see what happens:

    arr := []                                       ; Crate a new empty array
    arr.my_prop := 'Hello'                          ; Add a user-defined property
    
    ownprops := 'OwnProps():'                       ; Create a string to store all own props
    for key, value in arr.OwnProps()                ; Loop through the own props provided by OwnProps()
        ownprops .= '`n' key ': ' value             ;   Add each key and value on a new line
    
    MsgBox(
        ownprops                                    ; OwnProps() only lists my_prop
        
        '`n`nHasProp():'                            ; Properties arr has access to
        "`nLength: " arr.HasProp('Length')          ; True
        "`nmy_prop: " arr.HasProp('my_prop')        ; True
        "`nBase: " arr.HasProp('Base')              ; True
        "`n__Class: " arr.HasProp('__Class')        ; True
        
        '`n`nHasOwnProp():'                         ; Properties arr owns
        "`nLength: " arr.HasOwnProp('Length')       ; False
        "`nmy_prop: " arr.HasOwnProp('my_prop')     ; True
        "`nBase: " arr.HasProp('Base')              ; True
        "`n__Class: " arr.HasProp('__Class')        ; True
    )

In the results, all four are considered "properties" because `arr` has access to them.  
`Length` is the only one not considered to be an "own property".  
That's because arr doesn't own `Length`. That property is owned by `Array.Prototype`.  
This means `arr` doesn't own `Length` but it does have *access* to it.  
This is done via the `Base` property and this is your introduction to the prototype chain.  
We'll discuss the prototype object and prototype chain more in the classes section. 

But let's look at the `OwnProps()` result.  
The only property it lists is `my_prop`.  
This is why I said AHK doesn't consider `Base` and `__Class` to be "own props" even though they technically are.  

The big thing to take away is that "own properties" are properties that are defined in an object and owned by it.  
Properties that are inhertied from classes are not own props.  

## Descriptor objects define how a property behaves

To understand classes, we need to understand objects.  
To understand objects, we need to understand properties.  
And to understand properties, we need to understand descriptors.  
Descriptors are the hidden secret to how object properties work in AHK v2 work.  
They define how properties behave and they're what differentiates a property from a method.  

v1 lacks descriptors and that's part of the reason why the user doesn't have the same level of control over v1 as they do v2.  


### REMOVE? Using a descriptor to produce v1 behavior

People coming to v2 from v1 will often complain "I can't pass objects to for-loops anymore!"  

Let's talk about this and explain why v2 behaves like that.  
Then we can come up with multiple solutions to this.  
The last part of this section will show how we can alter v2 to behave like v1 by allowing basic objects to be passed to a for-loop.  

We've brought up the `__Enum()` method earlier in the guide.  
Here it is again.

When an object is passed to a For-loop, the very first thing it checks for is an `__Enum()` method.  
If it doesn't find the __Enum method, it checks to see if the object is setup to behave like an enumerator object.  
This is the reason why objects can't be passed to for-loops. They lack an __Enum method and they're not designed to act as an enumerator object.  
But in v2, there are three different ways this "problem" (it's really not a problem) can be addressed.

1. Don't use objects as associative arrays.  
    v2 provides us with maps and they act as true associative arrays.  
    In AHK v1, the standard object was this "super object" that acted as an object, an array, and an associative array all at once while having this really weird set of rules it played by.  
    This was a HUGE problem with v1. Top 3 IMO.  
    Even I struggled when coming to v2 b/c I didn't understand that v2 had made this distinction.  
    V1 taught us that objects, arrays, and associative arrays are the same thing and can be used interchangably.  
    This is a problem and now you have to explain to people that all three of those are different data structures with different behaviors.  
    They should've never been used "interchangably".  
    v2 acknowledges this and provides three individual structures, each with it's own purpose and features.  
    
    In fact, let's distinguish the three right now.
    
    * Objects `{}`  
        * The building blocks for the language.  
        * Key:value pairs but with restrictions on key names.  
        * These are designed for creating code structures.  
        * They are not designed to be data storage structures.  
            That doesn't mean they can't store it, they're not designed or optimized for it.  
        * They're not sterile, meaning no object starts off empty.  
            There will always be properties and methods inherited.
        * They're not enumerable by design because it's not common to "loop through" an object.  
            As opposed to looping through arrays and maps, which is expected behavior.
        * The OwnProps() method still provides a way to loop through "own props" of an object.
    
    * Arrays `[]`  
        * These are designed for storing data sequentially.  
        * They keep things in a numerical order, starting at index 1.  
        * They start sterile, meaning NOTHING is inside them when created.  
        * They're enumerable by for-loops.  
        * They don't allow for gaps in the array structure.  
            Meaning if when gaps are made, such as by removal of elements, all remaining elements are shfited left to fill the gaps in.  
            This is important to realize as it's part of the functionality of an array.  
            AHK v1, arrays didn't do this as they are associative arrays at heart.  
        * Working outside the range of elements in the array is an error.  
            You can't have an array with 10 items in it and assign something to array element 15.  
            It doesn't exist.  
            This is another thing v1 got wrong with arrays. Any "index" could be used because the index was just a key in a key:value pair.  
            That's why a v1 array can have strings as their "index"
    
    * Maps `Map()`  
        * These are designed for storing data by an associated value of some type.  
            Meaning it maps one value to another value.  
        * Unlike objects, maps allow the key to be ***ANYTHING***.  
            This is a big difference between maps and objects.  
            Object properties are restricted by AHK's [name rules](https://www.autohotkey.com/docs/v2/Concepts.htm#names).  
            Map keys can be *anything*. It's a **value** mapped to another **value**.  
            You could map a string to a string. A number to a number. A string to an object. An object to a string.  
            Meaning key names key be *objects*. You can't do that with property names.
        * Map keys have the option of being case-sensitive. Yet another thing impossible in v1.
        * All keys are sorted in ascending alphabetical order.
        * They start sterile, meaning NOTHING is inside them when created.  
            This is another core difference between using a map as an associative array vs an object.  
            Objects will inevitably start out with inherited members.  
            An array object will always the properties "Base", "Length", and "Capacity".  
            Worse, if you were to add a "Default" property to it to store a value, you might be sabotaging your own code.  
            You'll find out more about arrays `Default` property later.  
        * They're enumerable by for-loops.
    
    When you need an associative array, use a map, not an object.  
    That's what they're for.  
    
        mp := Map(
            'first', 'Groggy',
            'last' , 'Otter'
        )
        
        ; Enumerate keys and values
        for key, value in mp
            MsgBox('Key: ' key '`nvalue: ' value)

    
2. Objects **can** be enumerated with the `OwnProps()` method.  
    Objects, at their core, are still a valid way to store data in key:value pair format.  
    Even though v2 provides maps, it doesn't mean you can't use objects.  
    You just have to be OK with them being "associative arrays with a bunch of key naming restrictions".  
    If you understand that properties have these [name restrictions](https://www.autohotkey.com/docs/v2/Concepts.htm#names) and you don't need case sensitivity and you don't need spaces, etc..., then use an object.  
    This is why objects have a concept of "own properties" and why the "OwnProps()" method exists.  
    Own properties help identify "user-defined properties" and `OwnProps()` produces the enumerator to enumerator through an object's own properties.
    
        ; Create an object
        obj := {
            first : 'Groggy',
            last  : 'Otter'
        }
        
        ; Call the OwnProps() method to loop through everything
        for key, value in obj.OwnProps()
            MsgBox('Key: ' key '`nvalue: ' value)
    
    There might not be an __Enum method, but the Object does still provide that all important enumerator object.  

3. You can alter AHK's core structure so that all objects ARE enumerable without having to call OwnProps().  
    Descriptors are how we can do this and it's the reason this sub-section was created.  
    If the goal is to emulate v1's behavior of "pass any object to a for-loop and it loops through all of the added properties", we can add this behavior with one line of code.  
    
        Object.Prototype.DefineProp('__Enum', {call:(this, *) => this.OwnProps()})
    
        ; Create an object
        obj := {
            first : 'Groggy',
            last  : 'Otter'
        }
        
        ; Pass it to the for-loop without using OwnProps()
        for key, value in obj
            MsgBox('Key: ' key '`nvalue: ' value)
    
    From now on, all objects in that script can be used directly with a for-loop.  
    This line of code tells AHK:
    
    > "All objects you create will now have an __Enum method. When that method is called, get the enumerator from `OwnProps()` and return it.
    
    Here's what that line looks like when it's broken down into a more educational-friendly manner:

        descriptor := {call:object_enuemration}             ; This is what we're learning about in this section
        
        Object.Prototype.DefineProp('__Enum', descriptor)   ; DefineProp() are explained later in this section
                                                            ; Prototypes are explained in the classes section
        
        object_enumeration(this, *) {                       ; "this" is from the call descriptor object
                                                            ; * discards all other parameters
            return this.OwnProps()                          ; Return the object's enumerator from OwnProps
        }

And that use of a descriptor is what this entire section is about.  
Descriptor objects.  

Descriptors help us **understand properties** which helps us **understand objects** which helps us **understand AHK v2**.

### Understanding descriptors

A descriptor is used to describe what a property does.  
Every property in AHK is made from one of these descriptors.  
Don't be mistaken about descriptors just because we don't directly use them as we indirectly use them all the time.  
They are part of everything done in AHK.  
 
To make a descriptor object, you create a new object, give it a descriptor keyword, and associate something with it.  

    descriptor := {keyword: item}

There are four different descriptor keywords that can be used:

* `Value` - A property that stores data
* `Call`  - A callable property (method)
* `Get`   - A property that responsds to being accessed or used
* `Set`   - A property that responsds to being assigned something

When making a descriptor object, it should only contain one keyword.  
Meaning one key:value pair per descriptor object.  
There is one exception to this rule, though.  
A descriptor is allowed to contain both the `Get` and `Set` descriptor keywords as they can (and should) work together in many instances and they do not conflict with each other.  
It's the only time two keywords can be included inside a single descriptor object.  

That means we can break down every single property in AHK to one of these five descriptor types:

    {value: any}                ; A value property
    {call: func}                ; A callable property (a method)
    {get: func}                 ; A getter (one-way, access)
    {set: func}                 ; A setter (one-way, assign)
    {get: func, set: func}      ; A getter and setter (two-way, access & assign)

The `Value` descriptor is unique in that it's the only one that can be paired with any type of value.  
That's because it **is** the storage keyword.  
All of the other descriptor types expect a function because they all run code in response to some action.  

* Call: Runs code in reaction to a method being called: `obj.Called()`
* Get: Runs code in reaction to a property being accessed: `x := obj.getter_prop`
* Set: Runs code in reaction to a property being assigned: `obj.setter_prop := 123`

#### DefineProp() and `value` descriptors

We need to understand `DefineProp()` in order to understand how to make use of a descriptor object.  
The Object class ensures every object has this method, along with many others methods for dealing with properties.  
Every object has access to the `DefineProp()` method because it's *inherited* from the Object class.  

Objects **depend** on this method because with out it, there's are no properties.  
Or getters. Or setters. Or methods.  
Which means no objects.  
Which means no AHK v2.  

* `DefineProp(name, descriptor)`
    * `name`  
        The name of the property.  
        This must follow AHK's [naming rules](https://www.autohotkey.com/docs/v2/Concepts.htm#names).  
        This would be the same as a name given to a property when assigning a value, such as: `obj.ThisIsTheName := value`
    * `descriptor`  
        A descriptor object to associate with the property `name`.  
        This determines how a property behaves. 
        Here are the five different descriptor types:  
        
        * {value:item}          ; Value property
        * {call:item}           ; Callable property (method)
        * {get:item}            ; Getter (read-only property)
        * {set:item}            ; Setter (write-only property)
        * {get:item, set:item}  ; Getter & Setter

It's a very simple, but very powerful, method.  
Let's create an object and add a property using DefineProp() and a descriptor object.  

    obj := Object                               ; Create an object
    value_desc := {value:42}                    ; Create a value descriptor object
    obj.DefineProp('ans_to_uni', value_desc)    ; Define property name as ans_to_uni and assign descriptor
    MsgBox(obj.answer_to_universe)              ; Use newly created property

Have you wondered what is really happening when use the assignment opeartor like this: `obj.num := 10`  
In the background, AHK knows that  `10` to the property `num` of the object `obj`.  
Here's what it does with that information:

    ; It creates a value descriptor for 10
    val_desc := {value: 10}
    
    ; It knows the property name is supposed to be 'num'
    prop_name := 'num'
    
    ; It takes that stuff and uses it with the DefineProp() method of obj
    obj.DefineProp(prop_name, val_desc)
    
    ; obj.num now exists and can be used
    MsgBox(obj.num)

In other words, the assignment operator turns code like this:

    obj.num := 10

Into code like this:

    obj.DefineProp('num', {value: 10})

To give another perspective, what if we're assigning a value to a map using item syntax?

    mp := Map(
        'a', 'alpha',
        'b', 'bravo'
    )
    mp['c'] := 'charlie'
    
AHK knows that you're assigning a new key:value pair to the map, so it uses the `Set()` method for you.

    mp.Set('c', 'charlie')

### `Call` descriptor

The call descriptor is the hidden key to making things callable in AHK.  
As we've established, calling is how we activate methods and functions.  
The call descriptor is what makes functions and methods callable (methods are functions).

When making a call descriptor, we use the `Call` keyword and we include a function or method reference.  
To clarify the difference between function reference and function call:

* Function reference
    You refer to the function's name.  
    This passes the memory address of the function.  
    
        ; Assign the MsgBox function reference to mb
        mb := MsgBox
        
        ; mb and MsgBox now reference the same function
        ; This is called creating an alias
        
        ; mb now acts identically to MsgBox
        mb('Are we learning things?', 'AHK Knowledge', 'YesNo')
    
* Function call
    To make a function call, parentheses are included.  
    It runs the function's code and returns some value.  
    That value is what gets assigned to the variable.  
    It does not assign the function's reference to the variable.  
    
        ret := fn()                             ; Call fn() and save return value
        if (ret = 'blah')                       ; Check if ret matches return value
            MsgBox('Return value matches.')     
        
        fn() {
            return 'blah'
        }

In other words, when making a call descriptor (or any type of callback), don't call the function.  
Reference the function

    desc := {call:some_func}        ; Yes
    desc := {call:some_func()}      ; No (unless a function reference is returned, then yes)

Let's use a call descriptor to create a msg() method inside of an object.  
The method should take in one parameter: the message to display.  

    obj := {}                       ; Make a new object
    desc := {call:msg_fn}           ; Create a call descriptor using msg_fn
    obj.DefineProp('msg', desc)     ; Define a msg property using the descriptor
    obj.msg('Hi')                   ; Call the new method
    
    msg_fn(m) {                     ; Function to run when msg is used
        MsgBox(m)                   ; Show message box with message in it
    }

And an error pops up.  

> Error: Too many parameters passed to function.

I did this to emphasize an important point. More a rule than a point.  
A behavior of call descriptors is that they will **always** pass in a reference to the object they belong to.  
Meaning all functions created to be used as methods **must** have their first parameter reserved for that object-self reference.  

The general accept name for an object's self-reference is `this`, meaning "this current object".  
When we get into classes, we'll discuss `this` and how it's used to reference everything inside of any given class object.  

Going back to the example code that didn't work.  
If you look at the `msg_fn`, it only has one parameter.  
In the code, it's called using `obj.msg('hi')` but what was **really** sent was this: `obj.msg(obj, 'hi')`  
That's what caused the error about too many parameters.  
Two were sent in to a function that only has one parameter.  

We can fix the code by adding in a second parameter.  
The first one for the object self-reference and the second one for the message.  

    obj := {}                       ; Make a new object
    desc := {call:msg_fn}           ; Create a call descriptor using msg_fn
    obj.DefineProp('msg', desc)     ; Define an msg property using call descriptor
    obj.msg('Hi')                   ; Call the new method
    
    msg_fn(this, m) {               ; Function to run when msg is used
        MsgBox(m)                   ; Show message box with message in it
    }

While the concept of `this` may seem odd, consider it has existed this whole time and you never really had to account for it until learning how to manually define methods.  
It took learning about call descriptors before you actually needed to know about it and account for it.  

This self-referencing behavior will show up multiple times throughout this guide.  
The next "getter/setter" section includes it because they play by the same self-reference rule when running code.  

### `Get` and `Set` descriptor

`Get` and `Set` descriptors are how we make getters and setters.  
We're not going deep on these topics because there's an entire section dedicated to them in the classes section, including how to use backfields to store data.

But the quick version is that in OOP, there is a programming style where accessing properties from outside the object is never allowed.  

    obj.version := 'v2'         ; This would be forbidden
    Msgbox(obj.version)         ; This would also be forbidden

Instead, you would be expected to use "getter" and "setter" methods to get and set the property value.  
Meaning every property is going to have two additional methods associated with it: One to get and one to set.  

The above code updated to use a getter and a setter:
    
    obj.SetVersion('v2')        ; Setter in action
    MsgBox(obj.GetVersion())    ; Getter being used

This is the origin of getters and setters.  
There is no right or wrong here. It's a coding preference.  
If you do it, that's fine.  
If you don't do it, that's fine, too.

Get and set, much like the call descriptor, need to be associated with a function.  
Both getters and setters need to have a parameter to accept the object's own reference.  
However, setters need **two** parameters, with the second needed for the value being assigned to the property.  

    obj := {name:'AutoHotkey'}
    obj.DefineProp('version', {set: set_fn})
    obj.version := 'v2'
    
    set_fn(this, value) {
        MsgBox('You set the new ' this.name ' version to ' value '!')
    }

Another handy use of getters is making read-only properties.  
By using only `get`, no value can be assigned to the property because it does not know *how* to set a value.  
It lacks a `set` descriptor.  
This is also why you can't assign a value to a method.  
It's a hard rule, but even if it wasn't it would still error out because that property wouldn't know how to react to being set. There's no code associated with that action.

Let's make an object called math.  
This is a common practice in a lot of languages.  
You store math stuff in it like equations and constants.  
Constants are values that never change value. Like pi and Euler's .  
So if we added a `pi` constant, we could use just a getter, so it would be read-only.  
Assigning a value to it will throw an error.  

We're also going to show how to avoid making a function for the descriptor item.  
Instead, we'll be using a fat arrow function with a variadic parameter to dump any parameters passed in.  
This shortens up the code while still retaining its original functionality.  

    math := {}
    desc := {get:(*) => 3.14159265359}
    desc := {value:'Apple'}
    math.DefineProp('pi', desc)
    
    radius := 3
    area := math.pi * radius ** 2
    MsgBox('A circle with a radius of 3 has an area of: area)
    
    math.pie := 'Cherry'    ; Pie is a value so assigning is allowed
    math.pi := 7            ; Pi is a getter only: "Error: Property is read-only"

### Shortening up descriptors

In the previous section, we showed how to use a anonymous fat arrow function to shorten up code.  
Another way we can shorten things up is by not wasting time creating a descriptor object.  
Instead, define the object directly in the `DefineProp()` call.  
Take this code for example:

    desc := {value:42}
    obj.DefineProp('SomeName', desc)

We made `desc`...but we never really use it again.  
So skip that and define the object literal inside of `DefineProp()`.
    
    obj.DefineProp('SomeName', {value:42})

How about a practical example where we give all strings a `Length` property, just like JavaScript.  
And we'll do this without creating an object for descriptor and without defining a named function.  
You do not need to understand all of this as we haven't talked about how strings can be objects or how the Prototype object works.  

    ; The string prototype doesn't know how to define properties.
    ; It never "inherited" it from the Object class.
    ; But do you know what we can do in AHK v2?  
    ; We can take a copy to that method and give it to the string prototype
    ; Now we can define methods inside the string prototype
    ; Meaning ALL strings will have the properties we define
    String.Prototype.DefineProp := Object.DefineProp
    
    ; Using the new ability to define properties, we add a "Length" property  
    ; When working with strings "this" is the string itself
    ; So we make an anonymous function that takes in "this" (the string) and
    ; then uses it with StrLen to return the length
    String.Prototype.DefineProp('Length', {Get:(this) => StrLen(this)})

    ; Whenever you want the length of a string you
    ; can use the Length property they all have now
    str := 'AutoHotkey'
    MsgBox('str is ' str.Length ' letters long.')

## Methods

We've already learned a lot about methods in the descriptor section.  

Methods are when we bind a function to an object.  
We call a method the same way we call a function, except the object name is included.

    obj.method()

Methods should be geared toward providing some kind of service to the object.  
They should be related to the object somehow.  
There is a reason array objects don't have a "StrReplace()" method.  
Because it makes no sense for an array to have method related to strings.  

When naming a method, try to follow the rules of a function and make them verb or predicate-like.  
They should describe what the method does.  
Such as `InsertAt()` and `Delete()` for an array object.  
Or `DefineProp()` for objects.  

Methods should include words like: get, set, make, destroy, move, remove, shift, count, update, allocate, etc.

This causes the code to better describe itself and gives the function/method a stronger meaning.  

### Calling methods and returning values

Calling a method is done the same as calling a function, but includes the object name.  

    some_obj.method_name()

Parameters can be passed in like with functionss:

    obj.show_message('Hello, world!')

And methods can return values like functions:

    result := obj.get_running_status()

A simple example would be with an array object.  
They have multiple methods, including `Pop()`.  
This method removes the last element of the array and then returns that element's value.

    arr := ['alpha', 'bravo', 'charlie']    ; Make an array with three items in it
    value := arr.Pop()                      ; Use Pop() to remove last value
    MsgBos(value)                           ; Show removed value

The parameters of a method are identical to that of a function.  
Meaning you can have:

    obj.method(required, &ByRef, optional:=10, maybe?, variadic*)

### Built-in Methods

These are the methods that the Object class specifically provides to all objects.  
Notice that all methods provided by the Object class are specifically geared toward object properties.  
That's because objects are made of properties and the Object class is the origin of all the methods objects will need to work with properties.  
That's why the Object class provides all objects with:

* `Clone()`
* `DefineProp()`
* `DeleteProp()`
* `GetOwnPropDesc()`
* `HasOwnProp()`
* `OwnProps()`

####  `Clone()`

A method that creates a duplicate copy of the current object.  
The copy returned is a shallow copy. 
The reason it's called "shallow" has to do with how values are stored to properties, as discussed earlier.  
All those propreties are referencing memory addresses, including objects.  
When those properties are cloned, the primitives are copied "by value", meaning new memory addresses.  
When the object references are cloned, they are copied "by reference" meaning the references to the object is what is copied.  
It is NOT copying the whole object, and that's what makes it a "shallow copy".  

The opposite of a shallow copy is a "deep copy" and that **would** involve making duplicates of objects.  

Let's do an example that shows cloning both primitives and object references, as well as demonstarting how a cloned object's properties will "reference" the same stored objects.

    some_other_obj := {a:'auto', b:'hotkey'}
    
    obj := {string: 'hi', num: 123, obj:some_other_obj}
    
    show_obj('Original object', obj)
    
    shallow := obj.Clone()
    shallow.string := 'bye'
    shallow.num := 0
    shallow.obj.b := 'Shallow.obj.b updated!'
    
    show_obj('Clone object', shallow)
    show_obj('Original object after changing clone:', shallow)
    
    show_obj(title, obj) {
        MsgBox(
            title '`n'
            '`nobj.string:`t' obj.string
            '`nobj.num:  `t' obj.num
            '`nobj.obj.a:`t' obj.obj.a
            '`nobj.obj.b:`t' obj.obj.b
        )
    }

If you want a more accurate way of seeing how your objects look when they're cloned:

    ; The original object with the memory address its referencing
    obj := {
        ; Name  Memory address
        string  : 0x13603780,       ; Address containing string 'hi'
        num     : 0x09177200,       ; Address containing number 123
        obj     : 0x12000080,       ; Address containing object some_other_obj
    }
    
    ; The cloned object with the memory address its referencing
    ; Notice the object reference did NOT change
    shallow := {
        ; Name  Memory address
        string  : 0x12546410,       ; New address containing a new string 'hi'
        num     : 0x12800420,       ; New address containing a new number 123
        obj     : 0x12000080,       ; Same address containing the same object some_other_obj
    }

####  `DefineProp()`

A method that defines a new property name and associates a descriptor type.  
We just learned about [DefineProp of the descriptor section](#defineprop-and-value-descriptors).  

To recap, it's used to define properties in objects.  

* `DefineProp(Name, Descriptor)`
    * `Name`  
        The name of the property.  
        This must follow AHK's [naming rules](https://www.autohotkey.com/docs/v2/Concepts.htm#names).  
        This would be the same as a name given to a property when assigning a value, such as: `obj.ThisIsTheName := value`
    * `Descriptor`
        A descriptor object to associate with the property `name`.  
        This determines how a property behaves. 
        Here are the five different descriptor types:  
        * {value:item}          ; Value property
        * {call:item}           ; Callable property (method)
        * {get:item}            ; Getter (read-only property)
        * {set:item}            ; Setter (write-only property)
        * {get:item, set:item}  ; Getter & Setter

Quick example of adding a value using a value descriptor.  
Then add a method with the call descriptor.  
Then use the new method with the new property.

    obj := {version: 'v2'}                          ; Creat an object with a property
    v_desc := {value: 'AutoHotkey'}                 ; Make a value descriptor
    obj.DefineProp('language', v_desc)              ; Assign property using value
    c_desc := {call: (this, msg) => MsgBox(msg)}    ; Make a call descriptor
    obj.DefineProp('message', c_desc)               ; Assign method using call
    obj.message(obj.language ' ' obj.version)       ; Use new method with both properties

#### `DeleteProp()`

A method to remove a property from an object.  
When deleting a property, it's not enough to assign it a blank line.  
The property still exists and it contains a blank line.  
To permanently remove a property, use `DeleteProp()`.  

* `DeleteProp(property)`
    * `property`  
        The name of the property to delete.  

In the Array section of this guide we'll talk about a property called `Default`.  
It's a special property you have to add to an array for it to work.  
We'll discuss how assigning an empty line to it doesn't "delete" it.  
It just set's default to an empty string.  

Instead, we use the `DeleteProp()` method to remove the property from the object.  
This removes the value and allows the array to error out when an unset value is used.  
This is how it's done (and it'll make more sense when you read about `Default`)

    arr := [1, unset, 3]            ; Make a new array with an unset value
    arr.Default := 'Not set!'       ; Give it a default value
    MsgBox(arr[2])                  ; Use unset value and get 'Not set!'
    arr.Default := ''               ; "Remove" Default property
    MsgBox(arr[2])                  ; Use element and get blank line but no error
    arr.DeleteProp('Default')       ; Delete the default property from the object
    MsgBox(arr[2])                  ; Error: Item has no value, as expected

When an array element is unset, the element still exists.  

The `unset` keyword also works with object properties.  
The catch is that a property can't be unset.  
An unset property does not exist.  
This means setting a property to `unset` not only removes the value, it removes the property.  
This makes unset act as syntax sugar for deleting properties because we don't have to access the `DeleteProp()` method.  

    ; Both of these lines will delete the test property from obj
    obj.DeleteProp('test')
    
    ; This is syntax sugar b/c it's a shorter way of doing something we can already do
    obj.test := unset

For confirmation of this, we can use the built-in `HasProp()` method to check if the property exists.  
This is a method that **everything** in AHK, even strings, have access to.  
It's one of the *four core methods* that come from the Any class, ensuring all things in AHK have these properties.  

Let's use `HasProp()` to see what happens when we unset a property:

    example := {prop : unset}           ; Create an object and define a prop property, but assign it unset

    if example.HasProp('prop')          ; Check if the example object has a "prop" property
        MsgBox('Yup')
    else MsgBox('Nope')                 ; <-- "Nope", the property doesn't exist even though it was defined

    example.prop := 1                   ; Assign 1 to the prop property, creating the property and setting it

    if example.HasProp('prop')          ; Check again if the example object has a "prop" property
        MsgBox('Yup')                   ; <-- "Yup", it now exists in the object
    else MsgBox('Nope')

    example.prop := unset               ; Finally, set prop to unset

    if example.HasProp('prop')          ; Last check if the example object has a "prop" property
        MsgBox('Yup')                   
    else MsgBox('Nope')                 ; <-- Annnnnnnnnnnnnnnd...it's gone!

This can cause a point of confusion with some people when trying to unset a property.  
I struggled with it, too, until I finally *checked* to see if the property existed.  
AHK will give you errors when you try to work with unset properties, mentioning that things like `IsSet()` require a variable (or rather a value instead of an object).  

Now you know not to try and treat unset properties like they still exist.  
This becomes a lot more important when working with classes.

#### `GetOwnPropDesc()`

A method to get the descriptor from an own property.  
All object properties use some kind of descriptor.  
Any descriptors assigned to an own property can be gotten using this method.  
This allows the user to obtain a reference to a descriptor that they may not otherwise have a direct reference to.  

* `GetOwnPropDesc(Name)`  
     * `name`  
        The name of the property to get the descriptor from.  

Let's make a method but we're going to purposely use an anonymous fat arrow function for the descriptor.  
Meaning we won't have any direct reference to that function. It's the *reason* it's an "anonymous function".  
Using this method, we'll copy the descriptor from the property and then apply it to a different property in a different object.  

    ; Create a new object.
    obj := {}
    
    ; Define a new property called message.  
    ; Assign an anonymous function to it.
    ; We have no reference to the call function of this property.
    obj.DefineProp('message', {call:(this, msg) => MsgBox(msg)})
    
    ; Use GetOwnPropDesc to get the descriptor of "message".  
    ; We now have an indirect reference to the anonymous funciton.  
    ; message_desc is not the function, it is the descriptor object.  
    ; It contains a "call" property and a reference to the anonymous function.
    message_desc := obj.GetOwnPropDesc('message')
    
    ; Create a second new object
    my_obj := {}
    
    ; Define a new property called "msg".  
    ; Use the call descriptor from "message" to turn "msg" into a method.  
    my_obj.DefineProp('msg', message_desc)
    
    ; At this point, there are 2 different objects, each with differently named methods.
    ; But both methods point to the same anonymous function and work identically.
    obj.message('Hello')
    my_obj.msg('Goodbye')

The `GetOwnPropDesc()` method only works with own props, or properties added after creation.  

AHK does provide another method that works similarly to this, but can get the function reference from any method.  
The `GetMethod()` method is another one of those "four core methods" provided by the Any class that I've talked about.  
Using this method, you can get the function reference being used by any method.  
This provides a way to get a direct references to functions we couldn't otherwise reference.  

But understand that `GetMethod()` gets a function reference from a method whereas `GetOwnPropDesc()` gets a descriptor object from method.  

    x := MsgBox         ; x contains a function reference to the same function MsgBox points to
    
    y := {call:MsgBox}  ; y contains a call descriptor object and MsgBox is a function reference

Here's the previous code but modified to use `GetMethod()` instead of `GetOwnPropDesc()`.

    obj := {}
    obj.DefineProp('message', {call:(this, msg) => MsgBox(msg)})
    
    ; GetMethod() is used instead.
    ; This gets a reference to the function.
    ; This is not a descriptor object.
    message_fn := obj.GetMethod('message')
    
    my_obj := {}
    
    ; Using the function references, we can now create a new property.  
    ; The reference is used inside the call descriptor we had to add.
    ; In the previous code, we didn't do this b/c it was already a descriptor object.
    my_obj.DefineProp('msg', {call:message_fn})
    
    obj.message('Hello')
    my_obj.msg('Goodbye')

#### `HasOwnProp(Name)`

A method to check if an object has an "own property" of the specified name.  
Returns a 1 if the property exists and has a value set.  
A 0 is returned if the property doesn't exist or if the value is usnet.  
This is a pretty basic method but also provides a much needed functionality.  

    obj := {a:'Alpha', b:unset}
    
    MsgBox(
        "obj.HasOwnProp('a'): " obj.HasOwnProp('a')     ; True: 'a' has a value
        "`nobj.HasOwnProp('b'): " obj.HasOwnProp('b')   ; False: 'b' is unset
        "`nobj.HasOwnProp('c'): " obj.HasOwnProp('c')   ; False: 'c' does not exist
    )

#### `OwnProps()`

A method that creates an enumerator object, allowing all "own properties" to be looped through with a for-loop.  
We've talked about this a bit.  
This is a method that returns an enumerator and an enumerator is an object that the for-loop uses.  

* `OwnProps()`  
    Returns an enumerator.  
    First, we can create an enumerator and then use it:
    
        obj := {a:'Alpha', b:'Bravo', c:'Charlie'}
        enum := obj.OwnProps()
        for key, value in enum
            MsgBox('key: ' key '`nvalue: ' value)
    
    Or the method call can be passed directly to the for-loop.  
    This is normally better because the for-loop can immediately dispose of the enumerator.  
    Enumerators are meant to be disposable (though they *can* be designed to be reusable if you really care enough).  
    
        obj := {a:'Alpha', b:'Bravo', c:'Charlie'}
        for key, value in obj.OwnProps()
            MsgBox('key: ' key '`nvalue: ' value)


# Arrays

Arrays are one of those *super important* data structures that almost every programming language has.  
They are invaluable and many core concepts are based around using arrays.  

The purpose of an array is to provide a way to store any set of values in an ordered way.  
Any type of value can be added to the container and each gets stored in sequential order, meaning first item is first, second item is second, etc...  
Each value added to an array is called an "element" of the array.  
And each element is referenced by its "index" number.  
The index number indicates its position in the array.  

Arrays start out empty and allow you to add as many elements as you want.  
Elements can be inserted into an array, causing the array to be expanded and elements shifted to the right to make room for the newly inserted elements.  
If elements are removed from the array, any gaps created are filled by shifting all elements to the left and filling the gaps.  
Never having gaps is a rule of all arrays.  
You can have an unset element that has no value, but the element still exists. The unset value is not a gap.

And a final rule about working with arrays is the index cannot be out of range.  
Array index needs to be between 1, the starting index number, and whatever the max index value is.  
Some methods, like InsertAt(), allow you to use an index 1 higher than max. In this scenario, it would add an element to the end of the array.  
Example: You have an array with three elements.  
Valid array indices would be 1, 2, 3, and sometimes 4 (end of array).  
You cannot assign to index 0 index 7 because 0 is outside the minimum range and 7 is outside the maximum range.  
Those elements do not exist so trying to interact with them is an error.

## Traditional arrays vs AHK arrays

I do want to note the difference between a traditionally defined array and the arrays we use in AHK.  

* **Starting Index**  
    In a traditional array, the index always starts at zero.  
    Though this might not make sense to some, it is done that way for very good reasons.  
    In short, when working with lower level stuff, EVERYTHING starts at 0.  
  
    However, some higher level languages (like AHK, Ruby, and Lua) have chosen to start indexing at one as it's more "intuitive" for the user. The first item is item 1, the second item is item 2, etc...
  
* **Arrays vs Lists** 
    Traditional arrays tend to be "homogenous arrays", meaning they can only store one data type.  
    This is the kind of array used in C and would only contain chars or shorts or ints or floats.  
    If AHK did this,an array could *only* hold strings or *only* hold floats.
  
    Instead, AHK uses "heterogenous arrays" which are more generally called lists (or tuples for the Python and Scala crowd).  
    A list works similarly to an array because it stores values in order, however there are no restrictions on data types.  
    The first element can be a string, the next an integer, the next a float, and the next could contain another array or any other object.  
  
> "Groggy, arrays seem like objects with numbers for properties."

I cannot argue with that logic because they do act like a form of key:value pair.  

    index 1 = item1
    index 2 = item2
    ...
    index 117 = item117

But the functionality is in how an array is handled.  
As stated earlier, you can't have gaps in an array. That's a big one.  
So if you use the `.RemoveAt()` method, it will remove that element and then fill in any gaps by shifting all elements to the left until the gaps are filled.  
It also allows you to `.Push()` items onto the end of the array and `.Pop()` the last item off the end of the array.  
This is what the array is about. This functionality and desired behavior.  

Arrays are also used as stacks with the `Push()` and `Pop()` behavior, which we discuss more later.  
A map or object would need special coding to reproduce this behavior and it would involve using an array.  

## Making and using arrays

While showing how to create and use arrays, I'm going to be comparing them to objects along the way, as both have a lot in common.  

Both arrays and objects can store data.  
Arrays store data sequentially.  
Objects store data associatively.  

Both arrays and objects can be created by calling their respective classes.

    arr := Array()      ; Call the array class
    obj := Object()     ; Call the object class

One of the only big differences between the Object class and the Array class is that the Array class allows you to pass in array values at creation time.  
The Object class does not provide this option and object properties must be added post-creation.  

    arr := Array('a', 'b')  ; Adding values at creation
    
    obj := Object()         ; No option to add properties
    obj.a := 'a'            ; Add them individually
    obj.b := 'b'            ; Or make an object literal instead

Both arrays and objects are so important and used so frequently, they get their own special syntax, and both are called "literal syntax".  
For "array literal syntax", it's an open and closed square bracket.  

    arr := []   ; Array literal syntax
    obj := {}   ; Object literal syntax

Both array and object literal syntax allow for adding values at creation time.  
Syntax rules for arrays are much more relaxed than for objects.  
The only rule is that all values must be separated by a comma.  

The values are assigned in the order they're declared.  
In the following example, arr[1] is alpha because alpha is the first element added.  

    arr := ['alpha', 'bravo', 'charlie']        ; Adding elements at creation
    obj := {a:'alpha', b:'bravo', c:'charlie'}  ; Adding properties at creation

Both arrays and objects can be spread out with whitespace to make them easier to read.  
And whitespace applies to everything in AHK, not just array and object literal syntax.

    ; Array literal spaced out
    arr := [
        'alpha',
        'bravo',
        'charlie'
    ]
    
    ; Object literal spaced out
    obj := {
        a:'alpha',
        b:'bravo',
        c:'charlie'
    }

Both arrays and objects can contain other objects

    collection := [
        [1, 2, 3],
        {a:'alpha', b:'bravo', c:'charlie'}
    ]

But when it comes to accessing data, they're pretty different.  
An object uses the member access `.` operator to access properties and methods.  
An array uses the indexing `[]` operator to access array values.  
This opeartor is what provides us with "array syntax"/"item syntax".

    arr := ['alpha', 'beta']
    obj := {a:'alpha', b:'beta'}

Don't forget that an array is still a type of object.  
It, too, has properties and can use the member access operator.  
But that does with the array object's properties, not the array object's array elements.  
On the flip side, an object that's given an `__Item()` method can use item syntax, just like an array can.  

Another interesting thing to point out about this "literal syntax" we're learning:  
By understanding array literal syntax and object literal syntax, we understand how to write JSON data files.  
In face, if you include the fact that you also understand strings, numbers, and the concept of `unset`, you understand the bulk of JSON.

There is a section dedicated to JSON a little later in the guide where I just clarify the few rules that set JSON apart from AHK.  
You'll be shocked to see how similar the syntax for AHK objects and arrays are to representing objects and arrays in JSON.  

## Using arrays inside arrays

Arrays can contain other arrays.  
This creates a very powerful and useful data structure called a two dimensional array.  
This data struct also goes by the names "table" and "matrix".  
And yes, this is the concept that the movie's name was derived from.  

These data structures excel at providing solutions to to problems with two inputs.  
This is because a table represents a grid, and in each grid is the solution to two inputs.  
This will make more sense in a bit. Keep reading.  

To create a matrix, make a new array and fill it with equal sized arrays.  

    ; this is a matrix, or a table
    arr := [[1, 0, 0],[0, 1, 0],[0, 0, 1]]

It doesn't look like much when presented like this.  
This is when spacing out code can be REALLY beneficial.  
By adding in horiztonal and vertical whitespace, we can actually show the grid-like nature of a 2D array.

    arr := [
        [1, 0, 0],
        [0, 1, 0],
        [0, 0, 1]
    ]

Each individual array is a row of the grid.  
Each individual element acts as a column of that row.  
Meaning the first input is the row (array) number to use and the second input is the column (element) number to use.  

             ; Column (element) 1
             ; |  Column (element) 2
             ; |  |  Column (element) 3
    arr := [ ; ↓  ↓  ↓       
              [1, 0, 0],  ; ← Row (array) 1
              [0, 1, 0],  ; ← Row (array) 2
              [0, 0, 1]   ; ← Row (array) 3
    ]

This specific type of matrix may look weird, but it's a very important matrix called an identity matrix.  
If you ever start working with matrices in graphics, you'll inevitably learn about this matrix.  
It's very VERY important.  

To use a table, we use the array as normal but we include two indexing operators.  

    table[arr_num][element_num]
    
    ; or
    
    table[row_num][col_num]

The reason for the double indexing operators is because the first indexing opeartor selects which array (row) to get.  
`row := table[row_num]` resolves to an array.  
The second indexing operator applies to the newly resolved array `value := row[col_num]`.  
In resolves and gets the specified element value.  

A matrix is about the rows and the columns.  
It's about "two inputs result in one output".  
And that makes them ***very*** useful and extremely fast things.  
There's nothing to calculate because you already have a defined result for all possible outcomes.  
It's just a matter of looking up the correct element using the two index values.  

> "Can you PLEASE give us a real world example of a table?"

Sure!  
How about one that you've most likely been using since before you were a teenager?  
In math class, did you ever have something called a "multiplication **table**"?  
I mean the word table is even in the name.  
Think about it. It's a giant grid of numbers.  
Each row repsents one number and each column represents another number.  
Pick a row and column and where they intersect is the product of those two numbers.  
That's a matrix in action. 2 inputs = 1 output.  
We can easily create a "times table" in AHK:

    mult_table := [
        [   1,   2,   3,   4,   5,   6,   7,   8,   9,  10],
        [   2,   4,   6,   8,  10,  12,  14,  16,  18,  20],
        [   3,   6,   9,  12,  15,  18,  21,  24,  27,  30],
        [   4,   8,  12,  16,  20,  24,  28,  32,  36,  40],
        [   5,  10,  15,  20,  25,  30,  35,  40,  45,  50],
        [   6,  12,  18,  24,  30,  36,  42,  48,  54,  60],
        [   7,  14,  21,  28,  35,  42,  49,  56,  63,  70],
        [   8,  16,  24,  32,  40,  48,  56,  64,  72,  80],  ; ← Row 8
        [   9,  18,  27,  36,  45,  54,  63,  72,  81,  90],
        [  10,  20,  30,  40,  50,  60,  70,  80,  90, 100]
    ]   ;                                ↑
        ;                                Col 7
    
    ; Show it in use
    MsgBox('8 x 7 = ' mult_table[8][7])

You can now use this table to solve any multiplication problem ranging from 1x1 to 10x10.  

A matrix doesn't have to be only arrays.  
You can use a map or even objects to do the same thing.  
It's still "2 inputs = 1 output".  

Let's make an object that allows for color mixing.  
You provide two colors from the primary color types and this tells you the name of the color.  
Our two inputs are the two different starting colors and the output is the color it mixes into.  

    ; show mixing of red green blue
    color_mix := {
        red   :{red:'red'     ,green:'yellow' ,blue:'magenta'},
        green :{red:'yellow'  ,green:'green'  ,blue:'cyan'   },
        blue  :{red:'magenta' ,green:'cyan'   ,blue:'blue'   }
    }
    MsgBox(
        'blue and green is: ' color_mix.blue.green
        '`nred and blue is: ' color_mix.red.blue
        '`ngreen and green is: ' color_mix.green.green
    )

There will be a section at the end of the guide with some fun script ideas.  
We'll create a game of "Rock, Paper, Scissors" using a table.  

## Array built-in properties

These are the properties that the Array class specifically provides to all objects.  

All arrays come with four different properties:  
* `Length`
* `Capacity`
* `Default`
* `__Item`

Let's talk about each one.

### `Length`  
Sets or gets the total elements of the array.  
When using Length, it tells us how many elements the array has.  
An array element that is unset is still an array element, so Length includes those.  
Length can also be thought of as the "max index" of the array.  

    ; Array with 3 elements
    arr := ['a', 'b', unset]
    
    ; Length shows 3
    MsgBox(arr.Length)

Assigning an integer to this property will set how many elements the array has.  
When expanding the array (set length to a larger number), AHK will add elements until the element number matches length.  
All elements added this way will be `unset`.  
When truncating the array (set to a smaller length), all elements past the new length are removed and discarded.  

### `Capacity`  
A number that indicates how many elements worth of memory the array should be allocated.  

When AHK makes an array, it makes it big enough to the store all the elements.  
This means that the new array has exactly enough space to accommodate everything.  
When another item needs to be added to the array, there's no more space and the array must be expanded.

Expanding an array involves making a new and bigger array.  
Then all the elements from the previous array are transferred to the new one.  
This includes the new element that was being added. It's the reason the array needed to be expanded.  
When all the data is transferred over, the old array is deleted.

Whenever an array has to expand, it does all those steps.  
It costs time to do this which is why you want to minimize expansions.  
If you know how many items your array is going to have, you can always preemptively assign the capacity to the higher number.   
This will drastically reduce the amount of array expansions you'll need to go through and it will make your code faster.  

`Capacity` is not `Length`. They are very different.  
Capacity is the total possible room for entries in the current array.  
Length is the total number elements actively in use in this "capacity block".  
If you have an array with a capacity of 7 and a length of 4, it means you can add 3 more elements to that array and it will not need to expand. But the item after that will force and expansion, because that will be the 8th item added and the capacity is only 7.

Arrays can remove elements and never worry about capacity.  
You only need to worry about capacity when the array needs to be expanded.  
It's worth pointing out that it's impossible for an array's length to ever be larger than it's capacity.  
You can't put 2 gallons of water in a 1 gallon bucket. It doesn't work that way.  
The capacity is always auto-adjusted and expanded as needed by AHK.  

This is what capacity is about.  
Honestly, the `Capacity` property isn't used too often.  
But it can be a good thing to set when you know how many items will be in an array.  
This pre-allocates all the space needed so AHK doesn't have to keep making newer, bigger arrays.  
This can help increase performance with larger arrays.
  
To help, let's visualize this code:
  
    ; Create an array with 3 items.  
    arr := ['Item 1', 'Item 2', 'Item 3']
    
    ; Make a new array with a capacity of 7
    arr.Capacity := 7
    
        ;|------------ Array Capacity / Memory Allocated -----------|
        ;|-- Array Length / In Use -|
        ; __________________________ _______________________________
        ;| Item 1 | Item 2 | Item 3 | Empty | Empty | Empty | Empty |
        ; ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾ ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
  
In the above example, the array has three items in it, but has a capacity for seven items.  
Each additional item added will add one to the length.  
Once the length and the capacity are the same (7), the array is filled.  
The next time an item is added, a new, larger array will be needed.

Let's say we know that the array is going to have at least 30 items.  
The capacity can be set to 30 whe the array is made and it won't need to be expanded until the 31st item is added.  
  
    arr := [1, 2, 3, 4, 5, 6]
    
    arr.Capacity := 30
    
        ;|------------------------- Capacity ------------------------|
        ;|-- Length -|
        ; ___________ _______________________________________________
        ;|1|2|3|4|5|6| | | | | | | | | | | | | | | | | | | | | | | | | 
        ; ‾‾‾‾‾‾‾‾‾‾‾ ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾

Some of you might be wondering "how can all the array elements be the same size?"  
Because the array isn't storing data. It's storing references to data.  
Each array element is the same size because each element holds some kind of reference to memory.  

I'm sure many people think of an array like this:

    ;  3 chars 3 chars 5 chars   6 chars     10 chars        15 chars
    ; _________________________________________________________________________
    ;| 'Ace' | 'Ant' | 'Apple' | 'Ardvark' | 'Atrocities' |  'Autocorrelation' |
    ; ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾

In reality, it's more like this:    

    ; The elements don't need to be different sizes because it's not the data being stored in them.  
    ; It's all references to stuff.  
    ; Capacity = how many more addresses can the array store
     _________________________________________________________________
    |   0x10   |   0x120  |  0x9180  |  0x210   |  0x710   |  0x1020  |
     ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
    
    Our "RAM area" (I can only do so much with text!)
     ____________________________________
    | Memory Address | Data              |
    |----------------+-------------------|
    | 0x10           |'Ace'              |
    | 0x120          |'Ant'              |
    | 0x9180         |'Apple'            |
    | 0x210          |'Ardvark'          |
    | 0x710          |'Atrocities'       |
    | 0x1020         |'Autocorrelation'  |
     ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
    
    
Each element in an array is the same size, regardless of what it is.  
The arrays store references to the values, not the values themselves.  
A memory address is the same size for all things and that's what the array is organzing.  
So when we say "give me a capacity of 30", AHK makes an array that can hold 30 addresses.  

### `Default`  
Allows the user to define a default value to be used when an unset element is accessed.  
In order for this property to work, it must be defined and assigned a value.  
Normally, if an element is unset and you try to use it, AHK will throw an error.  
We've discussed this behavior before and it is expected.  
A rule of AHK is that using an unset value **is** an error.  

But there are ways to specify that you want to work with unset values.  
The "maybe" `?` operator is one of the ways we can do that.  
Another way is to provide a "default value".  
If an array element is accessed and it's unset, the array does not immediately throw an error.  
Instead, it's designed to check the array object for a `Default` property.  
If the user defined a Default property, that value is used instead of an error being thrown.  

It allows the user to account for unset elements by giving them an anticipated value all while preventing an undesirable error from being thrown.

    arr := ['a', unset, 'c']    ; Make an array with an unset value
    MsgBox(
        '1: ' arr[1]            ; Element 1 displays correctly
        '`n2: ' arr[2]          ; Element 2 throws an error because unset
    )
    
    arr := ['a', unset, 'c']    ; Remake the same array
    arr.Default := 'Not Set!'   ; Add a default property and assign a value
    MsgBox(
        '1: ' arr[1]            ; Element 1 displays correctly
        '`n2: ' arr[2]          ; Element 2 uses the default value because unset
    )

But what if, for whatever weird reason, you set a Default property but then later in the code need to get rid of it.  
A lot of times we just assign an empty string to something to delete it.  
That doesn't work with a property.  
If you assign an empty string to the Default property, it will use the empty string as the default value.  

Default must be deleted in order for it to stop working.  
To do this, we can use the `DeleteProp()` method discussed earlier in the built-in object method section.  
This method removes the property from the object, preventing the array from finding a default value and using it.  
Here's the example code provided earlier.

    arr := [1, unset, 3]            ; Make a new array with an unset value
    arr.Default := 'Not set!'       ; Give it a default value
    MsgBox(arr[2])                  ; Use unset value and get 'Not set!'
    arr.Default := ''               ; Assign empty string to "Remove" Default property
    MsgBox(arr[2])                  ; Use element and get blank line but no error
    arr.DeleteProp('Default')       ; Delete the default property from the object
    MsgBox(arr[2])                  ; Error: Item has no value, as expected

Or, you could also remove the default value by unsetting it.  
As mentioned earlier, this removes a property from an object.

    arr.Default := unset

### Special object property `__Item`  

This property name is not unique to arrays.  
This is a special name that has meaning to all objects in AHK.  
If a property is assigned the name `__Item`, it allows the object to utilize the indexing operator.  
Meaning the object can use "item syntax"/"array syntax" like an array or map can.  

We'll discuss `__Item` a lot more in the classes section.  

    obj[item_name]

Be aware that the __Item property itself *can* be accessed, but there's no benefit in doing so.  
Using the indexing operator with an object automatically infers `.__Item`, so typing it out is pointless and redundant.  
    
    ; These mean the same thing:
    obj[item_name]
    obj.__Item[item_name]

That's why you see people write arrays as `arr[2]` instead of `arr.__Item[2]` (both of which are correct).  
This is AHK working in the background. When you type `arr[2]` it's actually doing `arr.__Item[2]` so you don't have to.  

The `__Item` name is the reason the indexing operator works with the object.  
Without that property, using the indexing operator would throw an error because the object doesn't have any items to work with.  
It is a type of getter/setter.  
We can see how it supports arrays:

    arr := ['Test']         ; Create an array literal
    arr[1] := 'Changed'     ; __Item acts as a setter for array elements
    MsgBox(arr[1])          ; __Item acts as a getter for array elements

And it works differently for other object types:

* For maps, they're used for the name of a key:
    
      first := user['first name']     ; Get value assigned to first name key
    
* For guis, they're used to get a control by name:
    
      btn := goo['close_btn']         ; Get control object of close button

* For arrays, the square brackets are used for the index number:
    
      next := arr[2]                  ; Get 2nd element of array
    
And understand that `arr[index]` is the same as `arr.__Item[index]`.  

    arr := ['a', 'b']
    MsgBox(
        arr.__Item[1]
        '`n' arr[2]
        '`n' arr.__Item[2]
    )

## Array built-in methods  

These are the methods that the Array class specifically provides to all objects.  

Arrays have 10 methods special to them.  
I've split them into four groups.  

* Adding and removing elements
    * `Pop`
    * `Push`
    * `InsertAt`
    * `RemoveAt`

* Working with elemements
    * `Delete`
    * `Get`
    * `Has`

* Duplicating
    * `Clone`

* Special object methods
    * `__New`
    * `__Enum`

### Adding and removing elements  

There are four methods used to add or remove elements from an array.  

`InsertAt()` and `RemoveAt()` allows insertion/removal of one or more elements.  
`Push()` and `Pop()` are used to manage the array as a stack, strictly adding and removing from the end of the array.

#### `InsertAt()` and `RemoveAt()`  

These two methods are used to insert and remove elements from the array.  
The act of insertion and removal also adjusts the array, shifting elements as needed.  

*   `InsertAt(index, value [, more_values*])`  
    Allows for one or more values to be inserted at a specific index.  
    A value cannot be inserted in a range that does not exist.  
    Meaning if you have two elements in an array, you can insert to 1, 2, or 3 (end of the array, same as `Push()`).  
    Using an index that's out of range will cause AHK to throw an error.  
    
    When inserting new elements into an array, a new array is created with enough capacity to accommodate all the values.  
    The original array values are copied over to the new array.  
    The new values are inserted at the correct index and all values past that are shifted right.  
    
    * `index`  
        The element location to insert the value(s).  
        Using an index of `0` is the same as the "next available index".  
        It's the same as using `Length+1` or `Push()`.  
        
        These are are all equivalent:  
        
        * `arr.InsertAt(0, value)`
        * `arr.InsertAt(arr.Length+1, value)`
        * `arr.Push(value)`  
    
    * `value`  
        A value to insert into the array.  
    
    * `more_values` - [Optional]  
        One or more additional values.  
        All values are inserted at index in the order they're declared.  
        This is also a faster way of inserting elements because the array is only remade once.
        
        Along with the example, let's visualize thigns.
  
            arr := ['a', 'b', 'f']
                ; Original array
                ; _________________
                ;| 'a' | 'b' | 'f' |
                ; ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
            
            arr.InsertAt(3, 'c', 'd', 'e')
                ; Add 3 new elements to the array
                ; Current array capacity is 3
                ; Need a new array with a capacity of 6
                ; ___________________________________
                ;|     |     |     |     |     |     |
                ; ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
                ; Copy over everything up to index 3
                ; ___________________________________
                ;| 'a' | 'b' |     |     |     |     |
                ; ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
                ; Insert the new values at index 3
                ; ___________________________________
                ;| 'a' | 'b' | 'c' | 'd' | 'e' |     |
                ; ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
                ; Copy over remaining values from original array
                ; ___________________________________
                ;| 'a' | 'b' | 'c' | 'd' | 'e' | 'f' |     
                ; ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
                ; This array now has length of 6 and a capacity of 6
                ; The old array is deleted and arr updates to this new reference.  
                ; Notice 'f' was shift to the end.
            
            ; Show the updated array
            show_arr(arr)
            
            show_arr(arr) {
                str := ''
                for index, element in arr
                    str .= 'index ' index ': ' element '`n'
                MsgBox(str)
            }


  
*   `RemoveAt(index[, length := 1])`  
    Allows for one or more elements to be removed from the array.  
    If only one element is removed, the value stored in that element is returned.  
    If more than one element is removed, an empty string is returned.  
    All remaining elements right of the removed elements are shifted left to fill in the gaps.  
    Arrays can never have a gap between elements.  
    
    * `index`  
        The index location of the element to remove.  
    * `length` [Optional]  
        The number of elements to remove.  
        The default value for this is `1`.  
    
            ; Create an array of months
            months := ['January', 'Monday', 'February', 'March']
                ;  Length: 4, Capacity: 4
                ;  ___________________________________________________
                ; | 'January'  |  'Monday'  | 'February' |  'March'   |
                ;  ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
            
            ; Item 2 need to be removed because it doesn't belong
            removed := months.RemoveAt(2)
                ;  Length: 4, Capacity: 4
                ;  ___________________________________________________
                ; | 'January'  |            | 'February' |  'March'   |
                ;  ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
                ; Update boundaries of the array
                ;  Length: 3, Capacity: 4
                ;  ______________________________________ _ _ _ _ _ _ 
                ; | 'January'  | 'February' |  'March'   |            |
                ;  ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾ ‾ ‾ ‾ ‾ ‾ ‾ 
            
    And doing a multi-remove:
    
        ; An array with multiple items that need removed
        months := ['a', 'b', 'c', 1, 2, 3, 'd', 'e']
        
        ; Starting at the 4th index, remove 3 elements
        removed := months.RemoveAt(4, 3)
            ; Remove the 3 elements
            ; Length: 8, Capacity: 8
            ;  _______________________________________________
            ; | 'a' | 'b' | 'c' |     |     |     | 'd' | 'e' |
            ;  ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
            ; All remain elements are shifted left to fill gaps
            ; Length: 8, Capacity: 8
            ;  _______________________________________________
            ; | 'a' | 'b' | 'c' | 'd' | 'e' |     |     |     |
            ;  ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾
            ; AHK updates length to mark the size of the array
            ; This array has 3 free spaces it can fill before expanding
            ; Length: 5, Capacity: 8
            ;  _____________________________ _ _ _ _ _ _ _ _ _
            ; | 'a' | 'b' | 'c' | 'd' | 'e' |     |     |     |
            ;  ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾ ‾ ‾ ‾ ‾ ‾ ‾ ‾ ‾ ‾
    
#### `Push()` and `Pop()`  

Arrays are frequently used in a "stack" manner.  
Instead of imagine a horizontal array, imagine one that grows vertically.  
Like a stack of plate.

    ____________________    ; 
    \__________________/    ; 
    \__________________/    ; A stack (of plates)
    \__________________/    ; 
    \__________________/    ; 

When you add things to a stack, you put them top.  
You wouldn't lift up in the middle and try to wiggle them in.  
And it would be dumb (and eventually impossible) to lift the plates up and put the next one on the bottom.  
The whole idea behind a stack is that you add them onto the top of the stack (array).  
We call this "Pushing" something onto the stack.

    ____________________    ; 
    \__________________/    ; Pushing a new value (plate) onto the stack
      ↓ Push(plate)  ↓      ; 
    ____________________    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
                            
And when you remove something from a stack, you remove it from the top.  
You "pop" it off the top of the stack (array).  

    ____________________    ; 
    \__________________/    ; Pop a value (plate) off the stack
         ↑ Pop() ↑          ; 
    ____________________    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 
    \__________________/    ; 


This is called LIFO because it's "Last In, First Out".  
It helps keep track of things and specifically deal with them in the order they were received.  
The most recently added item having the highest priority.  

With a stack, you only deal with the end of the array.  
You add (push) one or more items onto the top.  
And you remove (pop) one at a time.

    ____________________    ; 
    \_______Yes________/    ; This element can be removed
    \_______No_________/    ; ↑ Can't remove until this is removed
    \_______No_________/    ;   ↑ Can't remove until this is removed
    \_______No_________/    ;     ↑ Can't remove until this is removed
    \_______No_________/    ;       ↑ Can't remove until this is removed

This is a widely used programming concept.  
It's rare to find a language that doesn't provide some kind of `Push()` and `Pop()` functionality.  
For AHK v2, the Array class ensures all array objects have a `Push()` and `Pop()` method.  

* `Push(value [, more_values])`  
    A method that accepts one or more values and adds them to the end of the array.  
    This method creates an element for each value passed in.  
    Passing in multiple values at once is more efficient than passing in one value at a time.  
    * `value`  
        The value to add to the end of the array.  
    * `more_values` [Optional]
        More than one value can be included when pushing.  
        It is more efficient to push everything available at once if possible.  
        Each value must be separated from the next one by a comma.
    
        ; How to make an array full of alphabet letters
        alphabet := []                      ; Make a new array
        loop 26                             ; Loop once for each letter
            letter := Chr(96 + A_index)     ;   'a' starts at ASCII 97. Use A_Index to increment.
            ,alphabet.Push(letter)          ;   Push each letter onto the array
        
        ; An array of all 26 letters is made
        str := 'Alphabet:`n'
        for letter in alphabet
            str .= letter ' '
        MsgBox(str)
    
* `Pop()`  
    A method that removes the last element of the array and returns that element's value.  
    
        arr := ['item1', 'item2', 'item3', 'item4', 'item5']            ; Make an array of items
        While arr.Length                                                ; While lenght is true (not 0)
            MsgBox('"' arr.Pop() '" was removed from the array.')       ;   Pop a value off the array and show it
        
        MsgBox(                                                         ; Show after the look finishes
            'Array elements: ' arr.Length                               ; There are 0 elements left b/c they were all popped off
            '`nArray is empty!'                                         ; The while-loop breaks when length is 0 (false)
        )

A great example of when AHK uses a stack is when it's tracking a thread.  
Each time a thread runs and reaches a function call, it makes a note of what line it jumped from.  
It "pushes" this number onto a stack that we'll call the "jump stack".  
And when the thread reaches a return, it "pops" the last value off the jump stack and then knows to jump back to that line to continue running code.  
When there are no more jumping points and a return is reached, the thread exits.  
This is how AHK knows to stop a thread.  

Let's walk through this.  
Start by making an array.  
This will be our stack of "jump back points".  

    jstack := []

The script starts and the thread begins at line 1.  
It goes down the script, doing the things it's supposed to.  
When it reaches line 5, a function call encountered.  

    1 | #Requires AutoHotkey v2+
    2 | #SingleInstance Force
    3 | 
    4 | x := 30
    5 | msg := two_thirds(x)
    6 | MsgBox(msg)
    7 | return

AHK add 5 to the jump stack to remember this is where the thread needs to *return* to when it finishes the function.  

    jstack.Push(5)
    ; arr = [5]

At this point, the thread jumps down to the line the function is defined on, taking any parameters with it.  
The thread arrives at line 20 and the number "30" is copied into `num`.  
The thread goes to the next line and encounters is_positive(), another function call.

    19 |
    20 | two_thirds(num) {
    21 |     if is_positive(num)
    22 |         return num * 2 / 3
    23 |     return ''
    25 | }

This function call happens on line 21.  
AHK pushes this new jump point onto the stack.  
AHK can now remember where to jump back to.

    jstack.Push(21)  ; contents: [5, 21]

The thread jumps down to the function definition for is_positive() and brings that 30 value with it.  
30 is not less than 0, so line 104 is reached and a return is encountered.  

    100 | 
    101 | is_positive(num) {
    102 |     if (num < 0)
    103 |         return 0
    104 |     else return 1
    105 | }
    106 | 

At this point, the thread saves the 1.  
It then goes to the jump stack and pops off the last jump point (21).  

    back_to := jstack.Pop()  ; contents: [5]

It now jumps back to line 21, bringing the 1 with it.  
1 is true, so the line continues to 22.  
The expression evaluates to 20 (30 * 2 / 3).  
And now this needs to be returned.

    19 |
    20 | two_thirds(num) {
    21 |     if is_positive(num)
    22 |         return num * 2 / 3
    23 |     return ''
    25 | }

AHK does the same thing.  
Remember value, pop next jump back point off stack.  

    back_to := jstack.Pop()  ; contents: []

Jumps back to line `5` bringing the number 20 with it.  

    1 | #Requires AutoHotkey v2+
    2 | #SingleInstance Force
    3 | 
    4 | x := 30
    5 | msg := two_thirds(x)
    6 | MsgBox(msg)
    7 | return

20 gets assigned to msg.  
msg is shown.  
Another return is encountered.

AHK always checks if the jump stack is empty before popping.  
It sees it's empty so it halts the thread by issuing the Exit() function.

    if !jstack.length
        Exit()

This is what happens when you "return" to a hotkey or a timer or the AET (auto execute thread).  
AHK sees there's nothing to "jump back to" and it just stops the thread.

* Side note about `return` vs `Exit()`:  
    Try to use `return` almost exclusively.  
    There is RARELY a time when you need to use Exit().  
    If you can't explain to some one specifically why Exit() is *needed* in your code, you shouldn't use it.  
    Part of this has to do with structuring your code.  
    The thread should be able to navigate your code wihtout the need of an Exit().  
    
    It's not that it's **forbidden** to use Exit(), it's that it can cause unintended problems and other bugs that are hard to find.  
    When the normal flow of code doesn't happen, things might not get updated or set or switched later in the code.  
    It's very easy for something to not work as-intended due to an early terminated thread.  
    That's why it's a good coding habit to let your threads return naturally and let AHK exit it for you.  
    What if you're using code someone else wrote? Like a library.  
    What if they're code expects completion but you terminate a thread early? That can cause problems.
    
    Just avoid using `Exit()` whenever possible and rely on `return` because AHK will use `Exit()` when there's nothing left to jump back to.

#### Origin of push, pop, and stack

This is one of those "pieces of programming history" I love telling.  
The terms stack, push, and pop all originate from dinner plates!

In a dining facility, plates are stored in stacks.  
Pepole learned really quick that you don't store stacks of plates on tables because it only takes that ONE clumsy guy to knock an entire stack (or two or more) of plates over.  
So now it's common to put plates inside of a plate dispenser, which are like big tubes that go down into a storage box of some type.  
They put a spring in the bottom that the plates sit on.  
As you put plates on them, they "push" the spring and other plates in the stack downward. 
The spring provides resistance so people can reach the top plate.  
And when a person takes a plate from the top of the stack, they're "popping" the plate off.  

This is the origin of these terms.  
It's all based on the behavior.  
The "stack" is a stack of plates (or an array of elements).  
You add one or more plates to the stack by pushing them down on top of the other plates (or push items "into" the array from the end)
You only take one plate at a time (or you only take one element from the end at a time).  
You never take plates from the middle or start (never take elements from the middle or start).  
And would you want to take plates from the middle? That's why those dispensers exist! To prevent people from doing that and messing things up (same goes for the array stack! You'll mess up the order!)  
Instead, you respect the stack and always follow the rules so nothing gets broken:  
Take one plate at a time off the top.  
Add one or more plates to the stack by pushing them down on top of the others.  

Stack, push, pop.

### Working with elemements

The next three methods are used to deal with individual elements.  

#### `Has(index)`
A method used to check if a specific element contains a set value.  
A 1 is returned if that index has a set value.  
A 0 is returned if that index value is unset.  

*   `index`  
    The element number to check.

        arr := [1, unset, 3]
        MsgBox(
            'index 1 is set: ' arr.Has(1)
            'index 2 is set: ' arr.Has(2)
            'index 3 is set: ' arr.Has(3)
        )

#### `Get()`
A method used to get a value from the specified element.  
This method isn't used too often because array syntax/item syntax is used to get values.  
`arr.Get(2)` is the same as `arr[2]`, with the latter being almost always preferred.  

* `Get(index [, default])`
    * `index`  
        The index number of the element to get.  
    * `default` [Optional]  
        Provide a default value to be used if an array element is `unset`.  
        This works similar to the `.Default` property, however this takes precedence over it.
        
            arr := ['Auto', unset, unset, 'rocks']
            arr.Default := 'v2'
            
            w1 := arr.Get(1, 'Hotkey')          ; Element 1 set. Get element 1.
            w2 := arr.Get(2, 'Hotkey')          ; Element 2 unset. Use default param.
            w3 := arr.Get(3)                    ; Element 3 unset. Use default property.
            w4 := arr[4]                        ; Use array syntax to get element 4
            
            MsgBox(w1 w2 ' ' w3 ' ' w4 '.')

If you're wondering "why does `Get()` exist if we can use square brackets?"  
I would respond with, "What do you think using brackets does in the background?"  
It usese the Get() method to get the value.  

#### `Delete()`  
Delete a value from an array element.  
This **does not** delete the element from the array. It only deletes the value.  
The array element still exists, but is "unset".  
To remove an element, the `RemoveAt()` method should be used.  

* `Delete(index)`  
    * `index`  
        The index number of the element value to unset.  
        
            arr := [1, 2, 3]
            arr.Default := 'UNSET Value'
            
            ; Show the value of the 2nd element
            show(arr, 2)
            ; Delete the value from the 2nd element
            arr.Delete(2)
            ; Show 2nd array element after deletion
            show(arr, 2)
            
            show(arr, index) {
                MsgBox(
                    'Length: ' arr.Length
                    '`nCapcity: ' arr.Capacity
                    '`nHas(' index '):' arr.Has(index)
                    '`narr[index]: ' arr[index]
                )
            }
        
### Duplicating with `Clone()`

A method that creates a duplicate copy of the current array.  
The copy returned is a shallow copy. 
The reason it's called "shallow" has to do with how values are stored, as discussed earlier.  
All those values are references to memory address, including objects.  
When those primitive values are copied over, they are copied "by value". We've been over this.  
When an object is copied over, it is copied "by reference".  
The object is NOT duplicated. Only the *object's reference* is copied over.  

This is why they're called "shallow copies".  
The opposite of a shallow copy is called a "deep copy" and that **would** involve making duplicates of objects.  

A method that creates a duplicate copy of the current array.  
The copy returned is a shallow copy.  
The reason it's called "shallow" has to do with how properties with object references work, as discussed earlier.  
Remember that object's are referenced, so when a copy is made, a copy of the *object's reference* is made.  
It is NOT cloning the whole object, and that's what makes it a "shallow copy".  
The opposite of a shallow copy is a "deep copy" and that **would** involve making duplicates of every single object referenced.  

* `Clone()`
    Creates a shallow copy of the array and returns it.
    
        arr := [1, 2]               ; New array with some values added
        clone := arr.Clone()        ; Make a clone
        clone[2] := 'b'             ; Change the second element of clone
        show_arr(arr)               ; Shows index 1 is 1 and index 2 is 2
        show_arr(clone)             ; First index of clone is same but second is changed
        
        show_arr(arr) {
            str := ''
            for index, element in arr
                str .= 'index ' index ': ' element '`n'
            MsgBox(str)
        }

### Special object methods `__New()` and `__Enum()`

AHK has multiple "special names" for object methods that do special stuff.  
We'll discuss these more and in-depth in the classes section.  
Arrays have two of these methods: `__New()_` and `__Enum()`  

`__New()` is the method that runs when you create a new array.  
It's what sets up the array and initializes it.  
It makes the internal array and also populates it if you provided values.  

__New is almost always called by the class that makes the object.  
e.g. when we call the Array() class, it makes the object and then __New() gets called. The user doesn't call it.  
However, when we talk about the `super` keyword, we'll learn about when the user may need to call __New.  

The other special method is `__Enum()`.  
When an object has an `__Enum()` method, it means it is designed to be passed to a [for-loop](https://www.autohotkey.com/docs/v2/lib/For.htm) statement.  
The __Enum method provide the for-loop with an enumerator object.  
This is a specially object that provides a list of values to be cycled through and it gives these values, one at a time, to the for-loop.
In the case of arrays, the code inside of __Enum makes an enumerator object that will go through each index and each value

    arr := ['alpha', 'bravo', 'charlie']        ; Make an array of strings
    for index, value in arr                     ; Pass arr to for-loop. Expect 2 variables back.
        MsgBox('Index ' index ': ' value)       ;   Show each index number and the stored value

The amount of parameters you pass to a for-loop determines what info you get back.  
If only one parameter is used with an array, it's designed to always give back a value.

    arr := ['alpha', 'bravo', 'charlie']        ; 
    for value in arr                            ; If only one parameter is used
        MsgBox('value: ' value)                 ;   Only the value is given

Wheras using one parameter with a map will provide you with the key name only.  
And for-looping through a Gui (yes, they have an __Enum method) provides you with all the gui's controls.  
One parameter provides just the HWND of the control while two parameters provides the HWND and the actual Gui Control Object as well.  

Fun fact: If you write your own enumerators, you can have up to NINTEEN `19` different parameters.  
An example would be if someone made a "user" object and designed it so that when you for-loop through it, it gives you 5 specific pieces of info

    ; Pretending that useres is filled with a list of people
    ; and that the __Enum method is set up to give 5 pieces of data back
    ; The user's real name, age, username, email address, and gender are all provided each loop
    for name, age, email, username, gender in users.GroggyOtter
        do_stuff_with_this_data()


# JSON

This was never intended to be a topic, however after adding a section about object literals and then adding a section about arrays and array literals, I wanted to point out that you already understand the bulk majority of JSON.  
So, why not just make a section about it and teach the few unknown things?"  

If you don't want to understand JSON, skip this part.  
But it's simple to learn and you already know how to write it by virtue of knowing the rules from AHK.  

[Here is the main site for JSON.](https://www.json.org/json-en.html)  
It includes a ton of great information including step-by-step flow charts for writing your own JSON parser.  
It also includes a great 
Shameless plug: I have written my own [full JSON parser called JSONGO](https://github.com/GroggyOtter/jsongo_AHKv2/), if you're interested in checking it out.

JSON is not a language.  
It's not code or a script.  
It's about **data**.  
More specifically, it's a *data interchange format*.  
JSON was originally based around how JavaScript handles objects, arrays, and data types.  
In fact, JSON means "JavaScript Object Notation".  
However, it's design was simplistic, easy to implement, and ended up becoming a perfect way to describe data in *any* language using only basic text.  
Other languages that wanted to work with JavaScript could easily understand its associtive arrays and sequential arrays (objects and arrays) because it was serialized in a way that it can be easily processed and it's definitive.  

JSON was so simplistic and effective to use that people started transforming data from one language (that wasn't JavaScript) into JSON and then transforming the JSON into *another* language (that was also not JavaScript).  
This is the evolution of the JSON format and why it's not synonymous with JavaScript anymore.  
It's simple and easily describes two of the most essential data types to any language.  
It is now considered the most widely used "data interchange format" out there.  

## A JSON object must be a "value"

When we talk about a "JSON file", we're really talking about the text and what it represents.  
The file represents a "value".  
In JSON, a value is defined as any of the data types or any of the data structures.  

A JSON file with just the number `17` or just the word `true` is a valid JSON file.  
Those are valid JSON values and can be parsed.  
However, a JSON file is almost always going to be a data structure (object or array).  

## Data types

JSON has five data types it deals with.  
These are used to represent primivite values. Meaning "data on the lowest level".  
Each one of these is considered a type of JSON value.  

* Strings - String/characters/text. This includes support for unicode.  
* Numbers - ALL languages use pure numbers.  
* `true` - A primitive truthy value.
* `false` - A primitive falsy value.
* `null` - A null or empty or unset or undefined primitive.

Most languages have most, if not all, of these primitive types.  
AHK obviously has strings and numbers.  
AHK's `unset` would be represented by `null`, as they're equivalent in concept even though different in name.  

But AHK does not have a dedicated primitive for Boolean `true` and `false`.  
This exception showcases why JSON is useful and versatile.  
When we write a JSON library, we can account for the absence of a `true`/`false` value.  
AHK considered all `true` things to be `1` and `false` things to be `0`.  
When converting JSON text into an AHK object, we can account for that and just set `true` things to `1` when converting.  

### Data rules

Here are the hard rules to all the data types

* Strings
  In JSON, strings must be between "double quotes".  
  The backslash is the escape character for strings and it has special meaning.  
  It is used to make escape sequences, similar to AHK's [backtick `` ` `` escape character](https://www.autohotkey.com/docs/v2/misc/EscapeChar.htm).  
  There are only three main escape sequences for normal characters:
    * `\"` : A literal double quote.  
    Necessary to distinguish from end of string.
    
    * `\\` : A literal backslash.  
    Because the backslash is **the escape character**, all instances of a backslash have to be escaped so that it's not mistaken as an escape character.  
    This is a necesary evil to make things work correctly.
    
    * `\/` : [OPTIONAL] A literal forward slash.  
    This is the only optional one and its main reason for existing is so it will play better with HTML tags.  
    Escaping a forward slash is completely optional.   
    Valid: `"string/chars"`  
    Valid: `"string\/chars"`  
    
  There are also 5 special characters that don't have characters to represnt them, so an escape is used
    * `\b` : Backspace character.  
    The character that is generated when you press the "Backspace" key.  
    AHK equivalent to using `Chr(8)` or `` `b ``
    
    * `\f` : Form feed character.  
    Form feeds usually indicate the end of a header or a section, but are not frequently used.  
    AHK equivalent to using `Chr(12)` or `` `f ``
    
    * `\n` : Line feed character.  
    The character for making a new line.  
    AHK equivalent to using `Chr(10)` or `` `n ``
    
    * `\r` : Carriage return character.  
    An old tradition from teletype writers that got implemented into "Window's returns".  
    If you need it, this is the escape for it.  
    AHK equivalent to using `Chr(13)` or `` `r ``
    
    * `\t` : Horizontal tab character.  
    Tab character for indentation.  
    AHK equivalent to using `Chr(9)` or `` `t ``
    
    * `\u####` : Unicode character.  
    The `####` needs to be exactly 4 hex characters, such as `\u0021` (exclamation point).  
    This allows `0x0000` through `0xFFFF` or the BMP (Basic Multilingual Plane), covering most of the world's written languages.  
    AHK equivalent to using `Chr(0x####)`

* Numbers - ALL languages use pure numbers.  
  Specifying numbers is a little more technical.  
  It can be an integer or float.  
  Exponents are supported.  
  Examples: `1`, `-5.9`, `0.2`, `1.34e200`, `-5E-123`
  
      Breakdown: -123.345e-678
      
      1. Whole  2. Fractional   3. Exponent
      -123      .345            e-678
  
  1. Whole number
     * Can be negative/start with a negative sign.  
     * A whole number cannot start with a zero unless the whole number **is zero**.  
        * Valid (whole is zero): `0`, `0.1`, `-0e+10`, `0.999E-1000`  
        * Invalid (whole is not zero):  `-0002`, `01.1`, `010000E-1`
  2. Fractional number  
    * An optional decimal point can included to incidate fractional or float numbers.  
    * If a decimal point is used, one or more numbers **must** come after it.  
  3. Exponents
    * Used to express scientific notation and handle exponentiation.  
    * Must start with a lower `e` or an upper `E`. Both are accepted.  
    * An optional plus `+` or minues `-` sign can be included before the number.  
    * One or more numbers must come next.
  
  Valid examples: `0`, `-0`, `1`, `123456789`, `-2`, `-2.2`, `-123.987E10`, `11235423.0e-12`, `1e+99`

* `true`  
  All in lowercase, no quotation marks: `true`

* `false`  
  All in lowercase, no quotation marks: `false`
  
* `null`  
  All in lowercase, no quotation marks: `null`

## Whitespace

Whitespace is defined as:

* Space: The space character
  AHK syonyms: `' '`, `Chr(32)`, `A_Space`
* Tab: The horizontal tab character
  AHK syonyms: `` '`t' ``, `Chr(9)`, `A_Tab`
* Line feed: The new line character
  AHK syonyms: `` '`n' ``, `Chr(10)`
* Carriage return: The "go to start of line" character
  AHK syonyms: `` '`r' ``, `Chr(13)`

You can use these characters anywhere inside of a JSON text **except** strings.  
The exception being spaces, of course.  
The other three white spaces must use their backspace equivalents mentioned in the strings part of data types.  

Meaning the purpose of whitespace is to format the code that's viewable to humans.  
When it comes time to process the file, everything but the spaces are stripped out and deleted.  

## Data structures

JSON has two types of data structures.  
And they work very similar to the two data types structures we've already learned about: objects and arrays

* Arrays  
  Arrays are a type of value.  
  Arrays also store values in sequential order.  
  
  These are written identically to AHK array literals.  
  Opening and closing square brackets are required.  
  All values must be separated with a comma.  
  
      An empty array:  
      []
  
      An array of values:
      ["String1", 2, "String3", 4.123]
  
      An array of arrays (called a matrix):
      [[1, 0, 0],[0, 1, 0],[0, 0, 1]]

      A matrix spread out with whitespace for easier viewing:
      [
        [1, 0, 0],
        [0, 1, 0],
        [0, 0, 1]
      ]

* Objects  
  Objects are a type of value.  
  Objects also store values in an associative way called a "key:value pair".  
  
  The key must always be a valid JSON string. No other type of value can be used.  
  A colon must come between the key and the associated value, just like in AHK object literals.  
  The associated value can be any type of JSON value, including other data structures.  
  Finally, all key:value pairs must have a comma between them, just like in AHK object literals.  
  
  Objects are written very similarly to AHK object literals.  
  The biggest difference is that a JSON key is always a string and an AHK key (property) can be ANYTHING.  
  But unlike a JSON string, an AHK can't have things like spaces or special symbols like in it like: `!@%&` etc...  
  
      An empty object:
      {}
  
      An object with a key-value pair:
      {"a":"Alpha"} 

      An object with multiple key-value pair:
      {"a":"Alpha", "b":"Bravo", "c":"Charlie"} 

      An object spread out with whitespace:
      {
          "a":"Alpha",
          "b":"Bravo",
          "c":"Charlie"
      } 
  
      An object containing objects:
      {
          "1-3 tracker": {"One":1, "Two":2, "Three":3},
          "4-6 tracker": {"Four":4, "Five":5, "Six":6},
          "7-9 tracker": {"Seven":7, "Eight":8, "Nine":9}
      } 

      An object containing objects spread out more:
      {
          "1-3 tracker": {
              "One":1,
              "Two":2,
              "Three":3
          },
          "4-6 tracker": {
              "Four":4,
              "Five":5,
              "Six":6
          },
          "7-9 tracker": {
              "Seven":7,
              "Eight":8,
              "Nine":9
          }
      } 

## Why use JSON?

The big rule is that JSON text must represent a single value.  
This value could be a number or a string, but as stated earlier, it's almost always going to be an array or object full of other data.  
Between these two data structures, you can create intricate and complex data structures capable of storing more data than you can imagine.  

From a handful of items to storing millions of entries, each one spanning multiple levels deep.  

It's a simplistic way to get data between systems.  
It is not about compressing data to store. JSON isn't efficient at data storage.  
It's fluidic and adaptable. It lets everyone speak the same "data language" for the basics of data structures.  
It allows complex structures to be transferred via plain text without the need to create specialized compatability codes between everything.  

Instead, enough people said "hey, let's make this the standard" that it became the standard "data language" so many others "speak and understand".  
It's hard to find a language that doesn't "speak JSON".

## Some examples

Here's an examle of a JSON string with lots of different data types in it:

    {
        "string": {
            "simple": "Hello, World!",
            "withQuote": "She said, \"Hello, World!\"",
            "newLine": "This is a line.\nThis is another line.",
            "tab": "This\tis\ta\ttabbed\tstring.",
            "backslash": "This is a backslash: \\",
            "unicode": "Unicode example: \u0041\u0068\u004B\u0076\u0032",
            "carriageReturn": "This will overwrite\rHello",
            "alert": "This is an alert sound: \u0007",
            "backspace": "This will remove a character: \bHello",
            "jsonString": "{\"name\":\"John\",\"age\":30,\"city\":\"New York\"}",
            "AutoHotkey": "v2"
        },
        "boolean": [
            true,
            false
        ],
        "nullValue": null,
        "object": {
            "nestedString": "Nested Hello",
            "nestedNumber": 100
        },
        "array": [1, 2, 3, 4, 5],
        "matrix": [
            [1, 0, 0],
            [0, 1, 0],
            [0, 0, 1]
        ],
        "number": {
            "whole": {
                "positiveInteger": 117,
                "negativeInteger": -420,
                "zero": 0,
                "negativeZero": -0
            },
            "fraction": {
                "positiveDecimal": 3.14159,
                "negativeDecimal": -1.61803,
                "zeroDecimal": 0.007
            },
            "exponent": {
                "float e nosign": 5.67e3,
                "int E negsign": 8E-5,
                "float e possign": 6.28e+3,
                "float E nosign": 1.234E6
            }
        }
    }

Or that entire thing can be represented as a single continuous string.  
This is because the parser doesn't care about whitespace.  
It's a serialized form of data and this what
It's going to look through each character one item at a time.  
This may look like a blob of text to you and me, but to the parser, this is great!

    {"string":{"simple":"Hello, World!","withQuote":"She said, \"Hello, World!\"","newLine":"This is a line.\nThis is another line.","tab":"This\tis\ta\ttabbed\tstring.","backslash":"This is a backslash: \\","unicode":"Unicode example: \u0041\u0068\u004B\u0076\u0032","carriageReturn":"This will overwrite\rHello","alert":"This is an alert sound: \u0007","backspace":"This will remove a character: \bHello","jsonString":"{\"name\":\"John\",\"age\":30,\"city\":\"New York\"}","AutoHotkey":"v2"},"boolean":[true,false],"nullValue":null,"object":{"nestedString":"Nested Hello","nestedNumber":100},"array":[1,2,3,4,5],"matrix":[[1,0,0],[0,1,0],[0,0,1]],"number":{"whole":{"positiveInteger":117,"negativeInteger":-420,"zero":0,"negativeZero":0},"fraction":{"positiveDecimal":3.14159,"negativeDecimal":-1.61803,"zeroDecimal":0.007},"exponent":{"float e nosign":5670,"int E negsign":0.00008,"float e possign":6280,"float E nosign":1234000}}}

### Comparing JSON text to an AHK object

Here's an example of a pizza order represented using JSON.  
It shows pizza is the main object.  
It tells you properties of the pizza, such as size, crust type, crust thickness, toppings, and more.

    {
        "pizza": {
            "size": "large",
            "crust": "pan",
            "crustThickness": 0.5,
            "sauce": "tomato",
            "isVegetarian": false,
            "isSpicy": false,
            "toppings": {
                "meats": [
                    {
                        "name": "ham",
                        "portion": "full"
                    },
                    {
                        "name": "bacon",
                        "portion": "right half"
                    },
                    {
                        "name": "chicken",
                        "portion": "full"
                    }
                ],
                "vegetables": [
                    {
                        "name": "pineapple",
                        "portion": "full"
                    },
                    {
                        "name": "mushrooms",
                        "portion": "left half"
                    }
                ],
                "cheeses": [
                    {
                        "name": "mozzarella",
                        "portion": "full"
                    }
                ],
                "others": [
                    "garlic",
                    "oregano",
                    "chili flakes"
                ]
            }
        },
        "price": {
            "currency": "USD",
            "amount": 15.99
        },
        "ratings": {
            "average": 4.5,
            "reviews": 350
        },
        "details": {
            "orderNumber": 98765,
            "orderedAt": "2003-10-30T14:00:00Z",
            "deliveryAddress": {
                "street": "714 Delaware St",
                "city": "Lanford",
                "zipcode": "61071"
            }
        }
    }

Comparing the two:

     _______________________________________________________________________________________________________
    |                  AutoHotkey Code                  |                   JSON Text                       |
    |---------------------------------------------------+---------------------------------------------------|
    |                                                   |                                                   |
    |    pizza_order := {                               |   {                                               | 
    |        pizza: {                                   |       "pizza": {                                  | 
    |            size: "large",                         |           "size": "large",                        | 
    |            crust: "pan",                          |           "crust": "pan",                         | 
    |            crustThickness: 0.5,                   |           "crustThickness": 0.5,                  | 
    |            sauce: "tomato",                       |           "sauce": "tomato",                      | 
    |            isVegetarian: false,                   |           "isVegetarian": false,                  | 
    |            isSpicy: false,                        |           "isSpicy": false,                       | 
    |            toppings: {                            |           "toppings": {                           | 
    |                meats: [                           |               "meats": [                          | 
    |                    {                              |                   {                               | 
    |                        name: "ham",               |                       "name": "ham",              | 
    |                        portion: "full"            |                       "portion": "full"           | 
    |                    },                             |                   },                              | 
    |                    {                              |                   {                               | 
    |                        name: "bacon",             |                       "name": "bacon",            | 
    |                        portion: "right half"      |                       "portion": "right half"     | 
    |                    },                             |                   },                              | 
    |                    {                              |                   {                               | 
    |                        name: "chicken",           |                       "name": "chicken",          | 
    |                        portion: "full"            |                       "portion": "full"           | 
    |                    }                              |                   }                               | 
    |                ],                                 |               ],                                  | 
    |                vegetables: [                      |               "vegetables": [                     | 
    |                    {                              |                   {                               | 
    |                        name: "pineapple",         |                       "name": "pineapple",        | 
    |                        portion: "full"            |                       "portion": "full"           | 
    |                    },                             |                   },                              | 
    |                    {                              |                   {                               | 
    |                        name: "mushrooms",         |                       "name": "mushrooms",        | 
    |                        portion: "left half"       |                       "portion": "left half"      | 
    |                    }                              |                   }                               | 
    |                ],                                 |               ],                                  | 
    |                cheeses: [                         |               "cheeses": [                        | 
    |                    {                              |                   {                               | 
    |                        name: "mozzarella",        |                       "name": "mozzarella",       | 
    |                        portion: "full"            |                       "portion": "full"           | 
    |                    }                              |                   }                               | 
    |                ],                                 |               ],                                  | 
    |                others: [                          |               "others": [                         | 
    |                    "garlic",                      |                   "garlic",                       | 
    |                    "oregano",                     |                   "oregano",                      | 
    |                    "chili flakes"                 |                   "chili flakes"                  | 
    |                ]                                  |               ]                                   | 
    |            }                                      |           }                                       | 
    |        },                                         |       },                                          | 
    |        price: {                                   |       "price": {                                  | 
    |            currency: "USD",                       |           "currency": "USD",                      | 
    |            amount: 15.99                          |           "amount": 15.99                         | 
    |        },                                         |       },                                          | 
    |        ratings: {                                 |       "ratings": {                                | 
    |            average: 4.5,                          |           "average": 4.5,                         | 
    |            reviews: 350                           |           "reviews": 350                          | 
    |        },                                         |       },                                          | 
    |        details: {                                 |       "details": {                                | 
    |            orderNumber: 98765,                    |           "orderNumber": 98765,                   | 
    |            orderedAt: "2003-10-30T14:00:00Z",     |           "orderedAt": "2003-10-30T14:00:00Z",    | 
    |            deliveryAddress: {                     |           "deliveryAddress": {                    | 
    |                street: "714 Delaware St",         |               "street": "714 Delaware St",        | 
    |                city: "Lanford",                   |               "city": "Lanford",                  | 
    |                zipcode: "61071"                   |               "zipcode": "61071"                  | 
    |            }                                      |           }                                       | 
    |        }                                          |       }                                           | 
    |    }                                              |   }                                               |
    |___________________________________________________|___________________________________________________|
    

See?  
You already know how to write JSON! You only need to learn the handful of rules that differ from AHK syntax.  
You can now read it **and** write it.  

If you ever need to check a JSON file to see if it's valid, you can use [JSONLint](https://jsonlint.com/), [JSON formatter](https://jsonformatter.org/), or any other online validator.  
VS Code also has built-in JSON support, so save it as a JSON file or set the current file type to JSON.  
It will point out any errors.  

If you ever want to challenge yourself, consider writing a JSON parser.  
Something that turns JSON text into AHK data and AHK data into JSON text.  

If you get stuck, post to the subreddit.  
For some, it'll be a hard pass, because it *is* difficult at first.  

Plenty of JSON parsers already exist for AHK, including my own [JSONGO](https://github.com/GroggyOtter/jsongo_AHKv2/tree/main/src), written natively in AHK v2.  

# Object-oriented programming

Here's the big topic; the one some people dread.  
I honestly think this topic is disliked or misunderstood so much because the people who teach it like to overcomplicate things and not explain stuff well enough.  
You guys know me. I strive to make things as understandable as possible.  

OOP stands for object-oriented programming (I'm sure you knew that by now).  
The name explains itself: Programming done mainly through the use of objects.

We still use variables in our code, but the theory is to turn the majority of "things" in our code into "objects".  
And we do this because it's a logical way of organizing and structuring code.  
We don't pass variables around in global space or rely strictly on function calling.  

Objects represent the "thing we want to create", the properties are its data, and the methods are the actions of the object.  
That's how they should be seen because that's how they are designed to behave.  

## The 4 pillars of OOP

You'll hear about the "pillars of object-oriented programming" when the topic of OOP gets brought up.  
They're considered the four key benefits to using the object-oriented style.  
These four pillars are:  

- Encapsulation
- Polymorphism
- Inheritance
- Abstraction

I know. I know!! Calm down and do NOT freak out.  
These are four very fancy words that each have a simple meaning.  
My programming teacher threw me to the wolves when it came to these topics.  
I won't do you like he did me.  
Each of these will get broken down individually and we'll talk about them like a normal person would.  
Let's keep it simple.

## Encapsulation
We have already mentioned encapsulation in this guide.  

To "encapsulate" something means to bundle it up. To contain things inside of something.  
When we discussed point objects earlier, we were encapsulating x and y coordinates into a single object.  
The object "encapsulated" the data.  

The idea of logically storing like-values (properties) and object actions (methods) into one item (object) is the whole idea behind encapsulation.  

Another benefit of encapsulation is it makes things easier to work with.  

> "Give us a realistic scenario, Groggy!"  

OK.  
Earlier I talked about making a card game.  
Would you rather work with five individual "card" variables or a single object that stores five card values?  
Treat the object like a "hand of cards object".  

Any function calls would require only passing in one object instead of five variables.  
But more than that, if it was an object, you most likely wouldn't be passing it to functions.  
There would be a method that gets whatever info you want from the hand of cards.  
And you would check that value against some "logic" that determines how you did.  

The whole idea behind Classes and how they are structured exemplifies the idea of encapsulation.  
This should become more apparent in the upcoming Class section.

## Inheritance
This might be the biggest feature of OOP.  
To inherit means "to receive something".  
In real life, you can inherit things.  
In programming, a class can inherit methods and properties from another class.  

And in AHK, the word to remember with inheritance is the class keyword "extends" and we'll talk about this more later.  

How does inheritance work?  
The short, simple answer is:  
When a class extends from another class, it will inherit the properties and methods of the class it extends from.  

Even though we haven't talked about classes yet, I'm going to throw some class code at you.
You are not expected to understand what's typed.  
But you can run the code, see the results, read the comments, and understand what's happening without understanding why.

This demonstrates the basics of inheriting things:
    
    ; Make an instance of the Example class
    instance := example()
    
    ; The example class has no properties or methods
    ; But it DID inherit the greeting property and test() method from main_class
    instance.test()
    
    
    ; Define a class called main_class
    Class main_class {
        ; Define an instance property
        greeting := 'Hello'
        
        ; Define an instance method
        test() {
            MsgBox(this.greetings)
        }
    }
    
    ; Define another class but extend it from main_class
    ; No methods or properties have been added
    Class example extends main_class {
        
    }

In this code, we make an instance object from the `example` class.  
The example class has nothing defined in it.  
Yet we can call the `test()` method.  
That's because example extends from main_class and main_class has a test() method.  
example *inherited* the `test()` method as well as the `greeting` property.  

How about looking at AHK's on language for inheritance.  
We know AHK has an Object class. It creates object literals (empty objects).  

    obj := {}

AHK also has an Array class. It creates array objects.  

    arr := []

The Array class "extends" from the Object class.  
This is covered in the [Array class docs](https://www.autohotkey.com/docs/v2/lib/Array.htm).  
Meaning all arrays are a type of object and all arrays will inherit the methods and properties that objects get.  

We've discussed what methods an [methods an Object has](https://www.autohotkey.com/docs/v2/lib/Object.htm) in an earlier section.

But here's where inheritance comes into play.  
An array is still an object. The docs tell us so.   
It's the very first thing you see on the [Array class docs page](https://www.autohotkey.com/docs/v2/lib/Array.htm).  

    Array extends Object

And there's that keyword **extends**.  
This means arrays are objects and thus inherit all of the methods and properties from Object.  

It makes sense, right?  
An array is still an object. It needs to be able to define properties and delete properties and and check for properties.  
That's what objects *do*.  
But it's also an array. So along with the properties and methods arrays "inherit" from objects, they also get their own methods and arrays added.  
These are used specifically to work with the array component of the object.  

And THAT is what inheritance in OOP is about.  
Being able to inherit things from the class you extend from.  

Sometimes you'll create a class that doesn't need to extend anything. That's perfectly normal.  
If you don't extend from anything, AHK automatically assumes you mean `extends Object`, because you're almost always going to be working with an object.  

Being able to extend classes and utilize inheritance is not a requirement, it's a featuer of OOP.  
It can make coding so much easier.  
It can make complex tasks more attainable.  
It's a tool.  
Use it when it's needed and don't worry about it if you don't need it.  
It doesn't have to be harder than that.  

## Polymorphism

Some people get confused by this topic, so I'm going to make it a point to be as crystal clear as I can here.  

Polymorphism all revolves around methods and it comes in two flavors:  
- Method overloading:  
    Method can accept different types and/or different amounts of parameters.  
    You've already kind of learned about this with optional parmas, variadic params, etc.
- Method overriding:  
    An existing method can be replaced/overridden with another method.  
    We haven't done anything with this but we will.  
    You can replace a method with another method. That's about it.

What does that fancy word `polymorphic` actually mean?  
The term is derived from Greek, with `polys` meaning "many" and `morphē` meaning "forms" or "shapes".  
So it's saying that methods can have many forms or shapes.  

Let's understand what method overloading and method overriding mean.

### Method overloading  

Overloading is when a method is designed to accept different **types** and/or different **amounts** of parameters.  

Imagine you have a job and at your job people give you two important numbers.  
It doesn't matter what those numbers mean. The point is you need those numbers to do your job.  
And you are able to receive those two numbers in multiple ways.  
Regardless of how you receive them, you can still do your job because you have your two numbers:

* A person can walk up to you and give you two pieces of paper, each with a number on it.  
* A person can hand you an envelope. Inside is two pieces of paper, each with a number on it.  
* A person from the next floor can yell two numbers over the railing down to you.  
* A person from the next building can call you and tell you two numbers over the phone.
* A person at home sick can email you two numbers.

In this scenario, YOU are a polymorphic method. Specifically, you're an overloaded method.  
You are able to accept multiple types of input and still do your job.  
You can get numbers from paper, from paper in a package, from a screen, or from sound.  
All because you've been programmed to know how to read and how to listen and how to understand when someone is providing you with two numbers. 

Polymorphic methods and functions work the same way.  
They can take in different kinds of parameters or even different amounts of parameters.  
You design the code to check for specific values and then use those values.  

> "Give us a real example that isn't basic or generalized!"  

OK, let's bring back our buddy the point object.  
We're going to make a polymorphic function.  
The point of this function is to click somewhere.  
It needs an x and a y coordinate to click at.  
We're making it polymorphic by allowing it to accept two different kinds of input.  
It can accept two numbers or it can accept a single point object.  

    ; Clicker requires an x and y coordinate
    ; 
    ; It can accept two numbers:
    ; clicker(100, 100)
    ; 
    ; Or it can accept a point object:
    ; point1 := Point(100, 100)
    ; clicker(point1)
    clicker(x, y?) {
        if (x is Point)                                 ; Do one thing if x is a point object
            Click(x.x, x.y)                             ;   If yes, click using point coordinates
        else if IsNumber(x) && IsNumber(y)              ; Do another thing if s and y are both numbers
            Click(x, y)                                 ;   If yes, click using x and y
        else if !IsNumber(x) || !IsNumber(y)            ; Otherwise, invalid input
            throw Error(                                ;   Throw an error
                'Parameter error.'
                '`nClick requires:' 
                '`nTwo numbers or a point object',
                A_ThisFunc
            )
    }

In the above example, it's polymorphic because it can accept two numbers or a point object containing the two numbers needed.
Without method overloading (without polymorphism), this would require two separate methods:

    clicker_num(x, y)
    clicker_obj(pointObj)

### Method overriding

One of the pillars of OOP we talked about earlier was inheritance.  
Classes can inherit methods and properties from other classes.  
But sometimes you might want to alter or update or completely relace an already existing method.  
You have the ability to do that with classes.  

If a class inherits a method, you can replace it with your own version.  
That's method overriding.  

Doing this, we sacrifice the original functionality. Until you realize you don't have to sacrifice the original functionality.  
It can be implemented into your new method and then your updated code can then run.  

Later on, we'll be talking about the keyword `super` and the property `Base`.  
There's a good example of method overriding in that section.  

That's what polymorphism is all about.  
Method overriding and method overloading are two more tools we can add to our coding arsenal.  
You don't HAVE to use them, but if you find a need to do these things, you can.

## Abstraction
zzz

When you're writing code, you want to focus on ease of use. Making it simple.  
Abstraction is all about focusing on the bigger picture.  

First, let's talk about a common concept within OOP.  
There are two different kinds of methods and properties.  
I don't mean static and instance. But if that's where your mind was, nice job!  
Instead, I mean methods and properties are split up into two main categories: public and private

* Public:  
  Public methods are methods designed specifically as "actions" to be called.  
  They're the methods that "do stuff" with the data of the object.  
  If you write a script that uses a class and you share it, the methods the user is expected to interact with would be the public methods.
  The user NEEDS to know about these to use the object effectively.  
  And public things need to be documented so people using the code know *how* to use it.  
  
  Using v2 arrays an example, all the methods listed on the docs page, like Push, Pop, and Clone, would all be considered "public methods"
  
* Private:  
  Everything else that shouldn't be accessed by the user is private.  
  These are the methods and properties the objects use internally to get stuff done.  
  The user has no reason to use these as they're not designed for the user.  
  They're blocks of code that help service all the other stuff.  
  
  Private properties or methods cannot be accessed from outside the object.  
  Doing so throws an error.
  
  If we're using v2 arrays as an example, think of all the stuff that happens in the background.  
  There's a method for allocating memory for the array, for releasing it, for shifting elements to fill gaps, to swap elements, and much more, all of them reliant on one more different methods.  
  ALL of those internal methods are private and we never call them. We *can't* call them.  
  AHK calls them when we're running code to make an array, push a value into the array, change the capacity of the array, etc.

These public/private concepts are called "access modifiers" and AHK doesn't support them.  
Instead, everything in AHK is considered public.  
That's part of it's ease-of-use but also considered a weakness of the language. There's always a tradeoff.  

In AHK, anyone can access any function OR property in the code.  

So why are we talking about private and public methods inside of the abstraction section if AHK doesn't even deal with private and public things?!?  

*Because it's important you understand the concept of **public things**, the things that the user needs to know about, vs **private things**, things the user does NOT need to know about.*

**This is what abstraction is about.**  
All those private methods and properties we don't document? Those are all "abstracted away".  
They're irrelevant and no one needs to know about them.  
Sure, these private methods and properties exist and they serve a purpose and they do their job, but it's part of the bigger machine and it's pointless to document them and tell the end user about them.  
Instead, we only focus on the public methods and properties so that anyone who wants to use our object can learn how to.  
We spare them the small, technical details like what private properties we used or what private methods we used to accomplish some task.  
We've abstracted away the unimportant stuff and instead focused on the useful and important stuff.  

Let's look at this from another angle.  
Pretend that I spent a month writing this huge class that ends up being really useful.  
It doesn't matter what it does. That's irrelevant. We're just saying it's really useful.  
The class is over 3000 lines of code.  
And the documentation for the class consists of:

* The constructor, or how to use the class to make objects.
* 6 methods that can be used to do different useful stuff with the object.  
* 2 properties of the object that control different things.

Now take a brief moment and think about what I just said.  

There is a useful class that's made up of over 3000 lines of code.  
However, to utlize this code, all you need to do is read about the constructor, the 6 methods, and the 2 properties.  
The user doesn't need to read through 3000 lines of code or understand every function and every property and how everything works.  
They only need to know how to make the object and the handful of methods and properties to use the object.  

All of those lines of code are completely abstracted away by 1/2 dozen methods, a couple properties, and some reading of how to use them.

**THAT is what abstraction is about.**  

And when it comes to the topic of abstraction, I'd argue the entire purpose of programming languages is abstraction.  
Assembly is abstraction for machine language.  
Low level languages like C or Rust are an abstraction for assembly.  
AHK is an abstraction for C++.  
Each step up the chain makes it easier to write code b/c more complicated tasks are simplified so the code can focus on their bigger project.  
But it's not ALL positive.  
Each level of abstraction that we go up, we lose a little control.  
And each level up we go, we add a little overhead to do the stuff that simplified the coding process.  

It's a constant tradeoff between ease of use and speed of implementation vs overhead and less control.

### Documentation is important

A relevant tangent to abstraction:  
You'll notice that I keep referring to documentation.  
And I keep saying "the user needs to know what methods and properties to use."  

You convey this information by writing documentation for your code.  
Normally, you store basic instructions at the top of the code so anyone who has the code has documentation...  
But you can also include more in-depth and detailed documentation on a code repo, such as GitHub.  

This provides instructions on how to use any constructors, methods, and/or properties provided by the object.  

Remember, you don't need to document the "internal" stuff. The stuff the user doesn't need to be messing with.  
Only document the stuff that you want the user to know about.  

## Recap

The super short version of all four pillars:  
- **Encapsulation**: Grouping/bundling things together logically.  
- **Polymorphim**: Method overloading and method overriding allow for a lot of flexibility in our code when using classes.
- **Iheritance**: Classes inherit the methods and properties of the class they extend from.  
- **Abstraction**: Abstract away the complexity of your code by making it easy to use. Only explain the important (public) methods and properties and abstract away the irrelevant (private) stuff.  

And you don't have to understand ALL of this perfectly at this very moment.  
Just understand the basics of each pillar and see it in the code you write.  

I promise it starts making sense after a while.  
And if you ever say to yourself "is it really as simple as...", the answer is probably yes.  

Eventually, you'll be at a point where you understand these four things so well, you'll be able to teach others about them. 👍


















# Classes

As a heads up, this section is kinda big.  

Classes are like super objects.  
They're still objects but they have a special structure, special method names you can use, they have multiple ways you can use them.  
They're specialized objects. 

Classes are a fundamental part of object-oriented programming.  
They're core to OOP because they are **what facillitate** OOP.  
Each pillar of object-oriented programming can be tied directly to classes:  

- Abstraction: Classes allow us to abstract code into a handful of methods and properties, making it easier to understand and use.
- Encapsulation: Classes, or rather objects in general, encapsulate values and code (properties and methods) into a single item.
- Inheritance: Classes extend from other classes, which causes inheritance. The entire idea of inheritance is provided by the class structure.
- Polymorphism: Classes allow methods to be overloaded and allows methods to be overridden (replaced) which is what polymorphism is.

With all those in mind, classes ultimately give us a way to build our code and give it structure.  
They provide a lot of tools that can make your coding life easier.  
And they provide a kind of framework for us to use.  

Ultimately, I want you to see classes as the tool I see them as.  
I want you to be able to throw together a class like it's nothing and understand exactly what's going on with everything.  
You should be able to know when to use `__New()` and when to use `__Get()` and when to make a static property vs an instance property and how to work with an object internally via the `this` keyword.  

Let's dive into this GroggyGuide and not just learn, but understand, classes.  

## Classes have different uses

Classes can be used in different ways and this can be a point of confusion for some people.  
Let's learn about this tool and how to use it.  

* A class can be used to create objects
* A class can be the object that is used
* A class can do both of these things

Let's expand on each.

### Classes can be used to create objects

By default, classes are designed to let you create objects (called instance objects).  
These objects can then be used to do whatever they do.  
A lot of AHK classes work this way, including the `Array` class.  
Calling `Array()` creates an array object.  
(Before anyone asks, using `[]` calls the Array() class, too.)  
That array object is then used to store a set of values sequentially.  
When we need another array, we call the Array class again and get another array object.  
This is a class that makes individual objects that we make use of.  
We're not using the Array class itself to store the data.  
  
### Classes can be the object that is used
A class does not have to create objects.  
It's still an object at its core and it has its own properties and methods.  
This means we can group like-things into a class and use that class as an object of some type.  
Classes are not *required* to make objects. They have the option to.  
It's prefectly fine to have a class full of static properties and methods.  

An example of using a class as an object would be an auto-clicker.  
You don't make "instances" of an auto-clicker. You **use** an auto-clicker.  
It has a running status property.  
It has a toggle method to turn it on and off.  
And it has some other code that drives the spamming.  
You're not making objects with this class, you're using the class to bundle up those properties and methods into one item that represents an auto-clicker.  

### Classes can do both of these things
A class isn't restricted to only creating objects or only being used as an object.  
As you'll learn later, we have static (class) properties and methods and then we have non-static (instance) properties and methods.  
Your class is determined by how you set it up.  
If you want to set it up with both class and instance methods, you're allowed to do that.  
The class has methods and properties you can use and it can still be called to create objects.  

The option is there. The tool is there if you want to use it.  

As an example of an object that does both is a project of mine called [`Peep()`](https://github.com/GroggyOtter/PeepAHK).  
It's a useful script that helps troubelshoot code by allowing you to "see" the contents of anything.  
If you have a variable or an array or a gui or even an unknown item, you can pass it to Peep() and it will visually show you that thing contains.  
You "use" the class by passing items into it and then Peep displays the contents to you.  
But Peep also returns a peep object, which contains a copy of the information peep just showed you.  
You can save multiple peep objects and compare them to help troubleshoot your code or identify at what point a problem is happening.  

It's a good example of a class that does both and it's a shameless plug for a useful tool that's completely free of charge.  

## The Class class documentation page

Every class in AHK has a documentation page.  
That includes the [`Class` class](https://www.autohotkey.com/docs/v2/lib/Class.htm).  
There's some stuff on this page I want to discuss from that page:

* Classes are objects
* Classes have a static Call() method
* Classes have a Prototype property

### Classes are objects

First, the very top of the docs page tells you the Class class extends from the Object class.  

    class Class extends Object

Meaning all classes are a type of specialized object.  
In fairness, most things in v2 are a specizled type of object.  
But the point is that a class is an object by all rights.  
It is still a container.  
It is still made up of properties and/or methods.  
And it is still used like an object.  

### Classes have a static Call() method

All classes are created with a Call() method already defined.  
This doesn't mean much to you because we haven't learned about `static` or `Call()` yet.  
So here's a quick intro to these topics.

* When something is defined as `static`, it indicates that property or method belongs to the class and not to the instance objects.  
* `Call()` is a special method name. If any object has a call method, it can be called. Like a function.  

We will discuss static and Call() more in their respective sections.  

If something has a `Call()` method, it makes that thing callable.  
This includes objects and class (which are a type of object).  

All classes, included ones by AHK, started out with 


Let's go back to earlier when we discussed **polymorphism**, specifically **method overridding**.  
It's the ability for us to change or update a method.  
The Call() method that comes with a Class can be overridden with a new Call() method.  
This allows the class to be called and have some other code runing instead of making an object.  
I'm not warning to *not* override Call(), I'm letting you know it's an option and it can be a desireable thing.  

If you make an auto-clicker class and want to turn it on/off by calling `AutoClicker()`, you would make a new Call() method and put the toggle code in there.  
The class now toggles the auto-clicking code on and off when called instead of making a new object.  

> "But what if I want to make my own class Call method AND I want the class to still make objects?"  

Great question!  
This is still possible to do.  
In fact, I'm not going to tell you how because later on, when we talk about the keyword `super`, I will **show you** how to do it.  
*Spoiler alert: The key is the Prototype object.*

### Classes have a Prototype property

This is kind of important to understand, so pay attention.

Every class has a property called `Prototype`.  
This property contains an object and it stores the properties and methods we want our instance objects to have.  

How does it do this?  

When the class is called, it clones the prototype object.  
Then the code does whatever it needs to set up the object.  
Such as an array making the internal array and putting the values in it.  
Finally, the newly constructed object is returned to the caller.  
And the next time the class is called, the process starts over and a new object is made.  

That is why it's called the "Prototype".  
It's the *original object* that all other objects are based off of.  
Just like they make prototype cars or guns or electronics or whatever.  
You have the one finished, working model that all the others are based upon.  

Let's take a look at a Prototype object of an AHK class as an example.  
When we make a new array `arr := Array(1, 2, 3)`, we're calling the Array class.  
It clones the Prototype object, puts the values into the array, and returns the object.  
When we use our new array object, we have access to these properties and methods:  

    ; Properties
    arr.Length
    arr.Capacity
    
    ; Methods
    arr.Clone()
    arr.Delete()
    arr.Get()
    arr.Has()
    arr.InsertAt()
    arr.Pop()
    arr.Push()
    arr.RemoveAt()

We know array objecst have these members because they're fully documented in the [Array class docs page](https://www.autohotkey.com/docs/v2/lib/Array.htm).  

The reason our new array object has those all of those is because `Array.Prototype` is an object that has all those.  
The first thing the class does when you call it is make a duplciate of the prototype with `Array.Protototype.Clone()`. Remember, prototype contains and object and all objects have a Clone() method.  
That clone is the array object that will be returned to you for use.  

And if you want to have a little fun, we can PROVE this is true using our code.  
Everything in AHK has the `HasMethod()` method. Because it's part of the `Any` class...and everything extends from Any is some way. (It's covered in that GroggyGuide I keep linking).  

So make a list of method names, loop through them, and check to see if `Array.Prototype` has those methods:  

    ; A list of method names
    methods := ['Clone', 'Delete', 'FakeName', 'Get', 'Has', 'InsertAt', 'MakingAPointHere', 'Pop', 'Push', 'RemoveAt']
    
    ; Loop through methods and check if the Prototype from Array has them
    for method in methods
        if Array.Prototype.HasMethod(method)
            MsgBox(method '() EXISTS!')
        else MsgBox(method '() is not a method of Array.Prototype')

Let's go a step further in understanding.  
This is essentially what the `Array.Call()` does when you call it:

    Call(items*) {
        arr := this.Prototype.Clone()       ; First, duplicate the prototype of the class
        if (items.Length > 0)               ; Check if any items were passed in
            for item in items               ;   If yes, loop through each item
                arr.Push(item)              ;     And add each one to the array
        return arr                          ; Return the new array object to the caller
    }

#### Please don't call them "blueprints"  
This is a quick tangent dealing with how some people like to describe Classes.  
There's always some guy in the group who wants to explain to people that "classes are like blueprints".  

I really dislike this description because it's not accurat at all.
A class doesn't even have to make objects. We've established this.  
How is an Auto-Clicker like a blueprint?  

It would be more accurate to say "the Prototype object of classes act as a blueprint".  
And I think people refer to it as a blueprint because they think the Prototype is building objects from scratch each time.  
That's not accurate.  

The reality of it all is that the object is already built. It's done. It was done the moment the class initialized.  
That `.Prototype` property **IS** the object that we will use.  
When we call a class and expect a new instance object, the class is duplicating the prototype object, not building a new one.  
This is why it's called a `Prototype` and not `Blueprint`.  
Prototype is a much more accurate and fitting description.  
When we want to produce anything in real life, we always make a prototype first.  
We usually make multiple. But regardless of that, you never start mass producing anything until you've gotten a prototype that you're comfortable with.  
And then EVERYTHING after that is based off that prototype.  

It's the PERFECT word choice for that object.

## Making a class

All that other stuff we just learned about is going to be used in the upcoming sections to help us understand classes, how they work, and how they're structured.  

Now we can get onto creating classes.  
Let's start by creating a basic class.  

Use the `class` keyword, provide a class name, and then add some curly braces to contain the class code.  

    class Example {
        ; Methods and properties go here
    }

This is where it all starts.  
An empty class.  
Now we need to learn about the different parts.  

## `Extends` keyword 
When defining a class, we have to decide what type of *thing* our new class is going to be.  
This is what the `extends` keyword is for.  
You're choosing another class to extend from. That class will be the "base"/basis for your class.  

Let's see how AHK's own classes use extend, starting with the Array class.  
The very first line of the [Array class docs](https://www.autohotkey.com/docs/v2/lib/Array.htm) says:

    class Array extends Object

So Array is based on Object.  
And if we check the [Object class docs](https://www.autohotkey.com/docs/v2/lib/Object.htm#DefineProp):  

    class Object extends Any

OK, let's keep playing detective and go to the [Any class docs](https://www.autohotkey.com/docs/v2/lib/Any.htm).  
It tells you that `Any` is the root class. It is the ONLY class in AHK that never `extends`.  
That means `Any` is the top. The alpha. The progenitor.  
**EVERYTHING** in AHK comes from the `Any` class, either directly or indirectly.  
Why is this important?  

Because every class extends from another and this is what faciliates inheritance.  
(I promise this is all going to come together in a moment.)  
Let's visualize the Any class and include the methods it provides (we're skipping properties):

    class Any {
        ; This class supplies these 4 instance methods
        GetMethod()
        HasBase()
        HasMethod()
        HasProp()
    }

Any has 4 methods it's provided.  
Because they're not `static` methods, they don't actually belong to the Any class. We'll discuss `static` more in the next section, but for now just understand a static method belongs to the class and non-static methods are actually part of the Prototype object we talked about in the last section.  

Let's rewrite the code so we can see the prototype in action:

    class Any {
        ; This class supplies these 4 instance methods
        Prototype := {
            GetMethod()
            HasBase()
            HasMethod()
            HasProp()
        }
    }

That's more accurate and we have an idea of what the Any class looks like.  
Now, let's look at the Object class.  
We know that `class Object extends Any`.  
Meaning the Object class inherits the prototype object of Any.  

    class Object extends Any {
        prototype := {
            GetMethod()
            HasBase()
            HasMethod()
            HasProp()
        }
    }

All objects will have access to those 4 methods.  
The Object class adds its own methods, including a static one.  

    class Object extends Any {
        ; Static-methods from Object
        static Call()
        
        prototype := {
            ; Methods from Any
            GetMethod()
            HasBase()
            HasMethod()
            HasProp()
            
            ; Methods from Object
            Clone()
            DefineProp()
            DeleteProp()
            GetOwnPropDesc()
            HasOwnProp()
            OwnProps()
        }
    }

The static method added is a `Call()` method and you'll remember that makes our class callable.  
This is the methods that makes us a new empty object when we call the object class:

    obj := Object()

The rest of the methods belong to the prototype.  

When you make a new empty object by calling `Object()`, you're creating an instance of the Object class.  
And that instance has access to these methods:

    ; Added by the Object class
    Clone()
    DefineProp()
    DeleteProp()
    GetOwnPropDesc()
    HasOwnProp()
    OwnProps()

    ; Inherited from the Any class
    GetMethod()
    HasBase()
    HasMethod()
    HasProp()

OK, let's go one extension further.  
The Array class extends from Object:

    class Array extends Object {
        ; Methods from Array
        static Call()
        
        Prototype := {
            ; Inherited from Any
            GetMethod()
            HasBase()
            HasMethod()
            HasProp()
            
            ; Inherited from Object
            DefineProp()
            DeleteProp()
            GetOwnPropDesc()
            HasOwnProp()
            OwnProps()
            
            ; Added by Array
            Clone()
            Delete()
            Get()
            Has()
            InsertAt()
            Pop()
            Push()
            RemoveAt()
            __New()
            __Enum()
        }
    }

Extends is all about inheriting methods and properties and deciding what you want your class based upon.  

This was a weird way of explaining what `extends` does, but it's what I ended up with after multiple rewrites. It DOES explain it.  
And helps solidify the concept of the Prototype object.  
And it will make the next section easier to understand.

> "How am I supposed to know which class to extend from?"  

Great question!  
Like I said before, it's about deciding on what you want the basis of your *thing* to be.  
Usually, `extends Object` is the default choice.  
It gives your objects the basics of being used as an object.  
Then you add more methods and properties to the class.  

If you wanted to make a new specialized type of Array, your class would probably extend Array.  
This ensures your object inherits the Call() that makes the array, it inherits the methods to use an array like Push() and Pop(), and then you'd write your customizations based on whatever upgrades you have in mind.

## The class members: Properties and methods

We've learned about making a class.  
We've learned about extending a class.  
Now we can get into the good stuff: Class members. The things that actually make up a class.  

We're going to learn everything I can think of to teach you.  
From instance members to static members to specially named members.  
And example code to go with it all.

Let's take our first step by starting with adding a property to a class and then using it.  

## Adding and using a property
Let's start by making a new Example class.  

When the class is called, it should produce an object that has a `greeting` property.  
Then we'll use that property.  

To add a property to a class give it a name and then assign it a value.  
It's written the same as making a variable, except you're declaring it inside the body of the class.  

    class Example extends Object {      ; Make a new class
        greeting := 'Hello, world!'     ; Add an instance property just like you would a variable
    }

And to use a property, we reference it.  
Just like we would a variable.  
The only difference is that the object name is included and is separated with a dot `.`.  

    instance := Example()
    MsgBox(instance.greeting)
    
    class Example extends Object {
        greeting := 'Hello, world!'     ; Add a property just like you would a variable
    }

We created an instance of example and then used its greeting property.  
Each instance is just that...it's own instance of the class.  
Making an instance of an array creates an array object.  
Making an instance of the example class creats and example object.  

All instance objects from a speicific class will have the same properties and methods as others.  
However, each stores its own values.  

    i1 := Example()                             ; Make 2 instances
    i2 := Example()
    MsgBox(i1.greeting '`n' i2.greeting)        ; They always start the same
    i2.greeting := 'Goodbye, world!'            ; Change greeting of i2
    MsgBox(i1.greeting '`n' i2.greeting)        ; Each holds its own value
    
    class Example extends Object {
        greeting := 'Hello, world!'
    }

## Adding and using a method

Methods are the actions of the object. They let us do stuff.  

To create a method, give it a name, parentheses (required), parameters (if any), and curly braces for the body of the function.  
You'll quickly realize this is the exact same way we create a function, except it's declared inside a class object.  

    class Example extends Object {          ; Create a class
        show_message(msg) {                 ;   Create a method with 1 parameter
            MsgBox(msg)                     ;     Use the parameter with MsgBox
        }                                   ;   End of method
    }                                       ; End of class
    
    show_message(msg) {                     ; For comparison, here's that method as a function
        MsgBox(msg)                         ; Written identically but outside of the class
    }

To use a method, we use it like a normal function except we include the object name. Just like with properties.

    inst := Example()                       ; Make an example object
    inst.show_message('AutoHotkey!')        ; Use its method to show a message
    
    class Example extends Object {
        show_message(msg) {                 ; Method accepts 1 parameter
            MsgBox(msg)                     ; Show msg using MsgBox
        }
    }

Pretty simple!  
Let's take that class and make some changes. 

We're going to add a property and then change the method to use the new property.  
The method will make use of the `this` parameter.  
All methods have a `this` parameter and it contains a reference to the current object.  
Think of it like saying "THIS object!"  
We'll talk more about `this` in its own section later.  

    inst := Example()                       ; Make a new instance of Example
    inst.message := 'Classes kick asses'    ; Set the message property
    inst.show_message()                     ; Call the method
    
    class Example extends Object {          ; Create a new class
        message := ''                       ; Add an empty message property
        
        show_message() {                    ; Method to show a message
            MsgBox(this.message)            ; Uses the value stored in THIS object's message property
        }
    }

Adding methods and properties to objects is pretty easy.  
It's no different than defining a variable or a function inside the class.  
And this bundles everything up (encapsulation at work).  

But what we've worked with so far are "instance methods" and "instance properties".  
Let's switch it up and create methods and properties that instead belong to the class.  
That's where the keyword `static` comes into play.

## Creating class members with `static`

We've talked about `static` previously.  
Adding `static` before a property or method makes it belong to the class.  
Instead of making instance objects, the class IS the object that's used.  

Let's recreate the last class but change the instance members to class members.  
The class `Example` will own those members and we can use them by using the class name.

    ; Notice we don't make an object to use
    ; The class IS the object to use
    Example.message := 'Value added to class'
    Example.show_message()
    
    class Example extends Object {                  ; Create a new class
        static message := ''                        ; Add a class property
        
        static show_message() {                     ; Add a class method
            MsgBox('this.message: ' this.message)
        }
    }

## Methods return values just like functions

Remember that methods are functions.  
They can return values just the same.  
By default, all functions (and methods) return an empty string unless a `return` and a value are provided.

Let's make a class for math functions.  
We'll give it an add `add()` method and a multiply `mult()` method.  
The add method only takes in 2 numbers (because it's designed that way.)  
The multiply method takes in any amount of numbers (again, because designed that way.)  
Both will do their math then return the final answer to the caller, just like a function would.  

    ; Add 2 numbers
    answer := 16
    universe := 26
    sum := math.add(answer, universe)
    
    ; Multiply 4 numbers
    product := math.mult(7, 6, 5, 2)
    
    ; Show the results
    MsgBox('The sum of answer and universe: ' sum
        '`nMultiply these: 7 x 6 x 5 x 2 = ' product)
    
    ; Create a math class for our math methods
    class math {
        ; Method to add 2 numbers and return the sum
        static add(num1, num2) {
            return num1 + num2
        }
        
        ; Method to multiply any amount of numbers and return the product
        static mult(nums*) {
            p := 1
            for num in nums
                p *= num
            return p
        }
    }

To be clear, we wouldn't do math like this because we have operators for things like addition `+` and multiplication `*`.  
Adding function calls into it just makes things slower.  
But this still exmplifies the point of returning a value.  

## The hidden `this` parameter

The keyword `this` is one of those things you don't know about unless you see someone use it or have it explained to you.  

Every method in a class has a hidden `this` parameter.  
And it will always contain a reference to the current object.  
If we have a instance method that uses `this.prop := 1` and we make an object called `obj42` and run that method, `this.prop := 1` is the same as typing `obj42.prop := 1`.  
But if we another object called `doggy` and we run the method, `this.prop := 1` is the same as `doggy.prop := 1`.  

`this` is constantly a reference to the current object running the doce.  
It's saying "***This*** object! Here! The one that's running. THIS object!"  

When using `this` in a class object, `this` is always equal to the class name.  
If the class is called `autoclicker`, then the `this` is the same as typing `autoclicker`.  

Let's do a code example:  

    Example.method()

    class Example {                 ; Make a class
        static num := 0             ; Property to use with method
        
        static method() {           ; Make a method that shows "this" being used
            MsgBox(this.num)        ; Show value of "this" objects num property
            Example.num++           ; Increment the num property of Example.num
            MsgBox(this.num)        ; Show this.num again. It went up.
            this.num++              ; Increment this.num
            MsgBox(Example.num)     ; Example.num shows the new number
        }
    }

For class objects, `this` is useful because it replaces having to type the class name each time.  
Usually, class names are longer than 4 letters, so `this` is almost always faster.  
But it doesn't offer much more benefit than that.  

However, with instance objects, `this` is invaluable because we often don't know the names of the instances that will be made.  
We don't **need** to know the names of the instances because `this` will always contain a reference to "this" object. It will always ***reference*** the same object as using the object's name. Meaning the object name and `this` are identical.  

 `this` and `obj` both refer to the exact same object, (remember object references from earlier...? Yup, here's a tie-in!) then y

When we write our code, we utilize `this` as a placeholder *because* we don't know the object's name.  
That's why all instance objects using `this` only affect their object.  

Another example:

    ; Make 2 new instances
    i1 := Example()
    instance2 := Example()
    
    ; Increment both
    i1.increment()          ; Increment's this.num++ is the same as i1.num++
    instance2.increment()   ; Increment's this.num++ is the same as instance2.num++
    instance2.increment()
    
    ; Show each instance tracks its own 
    i1.show()
    i2.show()
    
    class Example {
        num := 0
        
        increment() {
            this.num++
        }
        
        show() {
            MsgBox("this object's num is set to: " this.num)
        }
    }

In the above example, the `increment()` and `show()` methods both use `this.num` to refer to the current object's num property.  
For the `i1` object, `this.num` = `i1.num`  
For the `instance2` object, `this.num` = `instance2.num`  

> "Where does `this` come from, Groggy?"  

Great question!  
And I'm going to forward you to that other GroggyGuide I keep referencing.  
A link will be in the links section.  

The short answer to your question is it comes from call descriptors.  
When you make a call descriptor, it's automatically set up to pass in the object's reference.  
And when working with methods, the very first parameter passed in is always `this`.  
That's why it's a hidden parameter.  

The `this` parameter is a very convenient thing that you'll get used to quickly and end up using regularly.  
To the point where it just feels natural to use it.

## The `Base` property and hidden `super` parameter

Everything in AHK has a `Base` property.  
It's the only property defined in the `Any` class meaning all items will have it.  
Even a strings and numbers have a base property.  

`Base` is important because it helps track the origin of everything.  
The name says it all: what item is *based* upon.  

Base does not contain a string. It contains a reference to an object.  
We've talked about object references earlier in the guide.

When dealing with **instance objects**, `Base` contains a reference to the Prototype object it was cloned from.  
Using an array object as an example, its `Base` is equal to `Array.Prototype`.  
`Array.Prototype` is a reference to the Prototype object.  
`Base` is a reference to the Prototype object.  
They mean the same thing b/c they ARE the same thing.  
Anywhere you can use `arr.Base`, you can also use `Array.Prototype` and it'll work just the same.  

    ; Make an array
    arr := []
    
    ; Check if Base property is equal to the Array's Prototype object
    if (arr.Base = Array.Prototype)
        MsgBox('arr.Base and Array.Prototype are the same object reference.') 

When dealing with **class objects**, `Base` contains whatever class the current class extended from.  
Using the Array class as an example: `class Array extends Object`  
So the `Base` of the Array class is the Object class. Because that's what Array class is "based" on.  

    ; Using Array as an example
    if (Array.Base = Object)
        MsgBox('Yes, Array.Base is the same object reference as Object.') 
    
    ; Using a custom class as an example
    if (my_class.Base = Map)
        MsgBox('Yes, my_class.Base is the same the Map class b/c my_class extends from Map.') 
    
    ; Create a class based on the map class    
    class my_class extends Map {
        
    }

We learned about `Base` so we can learn about the keyword `super`.  
`super` is another hidden parameter and it works similarly to `this`.  
It always has a reference to the current object's Base property.  
In other words, using `super` is the exact same thing as using `this.Base`. They can be 

> "Groggy, why in the world would we ever need to use super? Why would we need the Base property?

Great question, but I already answered this earlier in the guide.  
Earlier in the guide while discussing polymorphism, I said this:

> Later on, we'll be talking about the keyword `super` and the property `Base`.  
> There's a good example of method overriding in that section.  

Method overriding is a fantastic example of when we would use `super`.  

At the risk of repeating myself, I want to make it clear when we create a new instance object, we clone the class Prototype object.  
It's the *original object* that all others are based off of. It ***is*** the prototype.  
If you override an instance object method, it's not destroyed. The current object loses its reference to the method but the Prototype object still has the original copy of the method.  

A few of you are probably perking up because you might see where this is going.  

Let's say we make a new class that creates specialized arrays.  
However, it always fills the first three array elements with `a`, `b`, and `c`.  
It doesn't matter why this is useful. It's a task; our goal.  
How do we code it?  

We add a `__New()` method to our class.  
This will run code when a new object is created.  
And that code can ensure the array's first 3 elements are set correctly.  

**Now we've hit our problem.**  
If we add our own `__New()` method, the original one that Array comes with will get overridden.  
How do we make our class still create and Array AND make sure that the elements are set up correctly?  

The answer is can be either the `Base` property or the `super` keyword.  
Or if you said `Array.Prototype`, wow, nice call. Also a correct answer and an impressive one.  

First, we override the `__New()` method by providing our own version.  
This replaces the original __New with ours, but remember, this object is a **copy** of the Prototype object.  
Meaning the original __New method still resides in the Prototype.  

In our __New method, we make the first line a call to the original method so it will set up our object correctly.  
We know where the Prototype is stored:  

    Array.Prototype.__New()

And earlier we learned that `Base` is a property containing a reference to the Prototype object that this object is based on.  
So we don't have to use `Array.Prototype` because that's the same as typing `this.Base`.  

    this.Base.__New()

Oh man, things are starting to come together.  
Earlier we said that `super` is the equivalent of `this.base`.  
Finally, we can see an example of using super:

    super.__New()

That's right, all three of these lines of code reference the exact same object.  

    super = this.Base = Array.Prototype (in this example)

Now that we know how to code our solution, let's write it:

    myarr := super_array(1, 2, 3)               ; Create a super array
    view_array(myarr)                           ; View it

    class super_array extends Array {           ; Create a specialized array extending from Array
        __New(items*) {                         ;   Override the original __New() with our own
            super.__New('a', 'b', 'c', items*)  ;     Call the original __New() from the Prototype object
        }
    }
    
    ; Hand function to display array contents
    ; Keep a copy for yourself
    view_array(arr) {
        result := ''
        for index, value in arr
            result .= 'Index ' index ': ' value '`n'
        MsgBox(SubStr(result, 1, -1))
    }

When the class gets called, it gets passed a list of items to add to the array.  
Those are passed in as an array of parameters.  
We make a call to `super.__New()` and pass in the items, however we add `'a', 'b', 'c'` first, so they're the first 3 items in the array.  
Then we include `items*` last so the reset of the values can be added.  

What we have now is a class that makes arrays, but will always make them with a, b, and c as the first elements.  
We did this by overriding `__New()` with our own version but then using `super` to call a method from the prototype that we had just overridden.  

To reiterate, `super` is not a commonly used keyword and you probably won't use it too often.  
If at all.  
But if you need to override a method and still want to be able to use the original, now you know how to do it. 👍

## Creating an auto-clicker using a class

After learning all that, let's make something userful.  
We'll create an auto-clicker using a class structure.  
To do this, we'll make a class called `AutoClicker`.  
We need 2 properties. One for tracking running status and one for the delay between clicks.  
We also need 2 methods. One for toggling the auto-clicker on and off and one for handling the autoclicking.  
All of these need to be static b/c they all belong to the class. We are not making autoclicker objects.  
In fact, let's make it so calling the class is what toggles it on and off.  
To do this, we'll override the Call() class and replace it with our own (polymorphism anyone?)  

We mentioned documenting the class.  
Remember that we only care about documenting things the user needs to know about.  
These would be considered "public" members.  
This includes the `Call()` method (calling the object) and the `Delay` property for setting time between each click.  

The other two members, `run_clicker()` and `running`, would be "private" or internal members.  
We don't document those because the user shouldn't be taught about them or use them.

And look at that! Abstraction makes an appearance at the party!  
Only teach the user about the stuff they need to know about.  

The `Call()` method replaces the need for a `toggle()` and also removes its ability to create new objects.  
Which is good. Because like stated earlier, this class is not supposed to make auto-clicker objects.  
Plus, making the class callable to toggle it makes the code cleaner:  
Calling the class: `AutoClicker()`  
Vs having to call a method: `AutoClicker.Toggle()`.  

And we'll discuss `Call()` later. It has it's own sub-section.  

    #Requires AutoHotkey v2.0.19+                           ; Always have a version requirement

    *F1::AutoClicker()                                      ; Make a hotkey and assign it the autoclicker

    ; An auto-clicker object that will spam left clicks
    ; Bind toggle() to a hotkey to turn autoclicker on and off
    ; 
    ; Properties:
    ; delay - Set the delay between each click, in ms.
    ;         To click once every 100ms:
    ;         AutoClicker.delay := 100
    ; 
    ; Methods:
    ; Call() - Calling the class switches it on/off
    ;          Assign this to a hotkey
    ;          *F1::AutoClicker()
    class AutoClicker extends Object {                      ; Make a class
        ; === Public ===
        static delay := 100                                 ; Delay between clicks in ms
        
        static Call() {                                     ; Make the class callable to switch it on/off
            this.running := !this.running                   ; Switch running property between true <-> false
            this.run_clicker()                              ; Run the method that handles the auto-clicking
        }
        
        ; === Private ===
        static running := 0                                 ; Track running status of autoclicker
        
        static run_clicker() {                              ; Handles autoclicking
            if !this.running                                ; If the running property is off
                return                                      ;   Stop here so the rest doesn't run
            Click()                                         ; Click the mouse
            callback := ObjBindMethod(this, 'run_clicker')  ; Create a boundfunc to run this method again
            SetTimer(callback, -this.delay)                 ; Use settimer to run callback one more time using delay property
        }
    }

## Dynamic properties

Dynamic properties are a special type of property.  
They provide us with things called "getters and setters".  
These are methods that run when a property is assinged a value (set) or its value is retrieved (get).  
Dynamic properties are AHK's getters and setters.  

### Unerstanding getters and setters

"Getters and setters" are OOP terms for methods that are supposed to be used to get and set property values.  
You'll also hear getters referred to as `accessors`, because the get/access properties.  
And setters are referred to as `mutators`, because they set/change/mutate properties.  
Plus, how cool do those terms sound? I always loved the terms "accessors and mutators".  

Getters and setters serve a couple purposes.  
They help to protect a property.  
And they allow you to run code when a property is accessed or changed.  

Some people will tell you that EVERY PROPERTY should have a setter and getter for it b/c it's a great practice.  
Some people will tell you that you should NEVER use them because they're not necessary.  
And, like with anything that has a spectrum of opinions, the best answer usually falls in the middle.  

I will not tell you either of those things.  
Instead, I'd rather teach you what they do and then let you decide.  
I've said it many times and I'll keep saying. These are tools. Use them as you see fit.  

Do you want to validate data when it's being assigned to a property?  
Setters can be really good for that. They can run validation code before storing the value. Or error out if it's bad.  

Do you want a property to be formatted a certain way when you retrieve it?  
Getters can be really good for that. They can run the code needed to format it the way you want it to look.

We're going to make examples of both of these in the upcoming get/set sections.  

But the point is that you should use a dynamic property when it makes sense to you to do so.  
Use them when you need them because they definitely can serve a great function.  
But don't force using them if you don't need them.

### Creating a dynamic property

To create a dynamic property, give it a name and some curly braces for the body.  
It's the same as defining a method without the parentheses.  
Inside the body is where the `get` and `set` methods go.  
Notice that set and get also lack parentheses.

    class example {                         ; Start class
        DynamicProp {                       ;   Add dynamic property
            get {                           ;     Add getter/accessor
                ; Get code here             ;       Code here
                return this._DynamicProp    ;       Always return something
            }                               ;     End of getter
            set {                           ;     Add setter/mutator
                ; Set code here             ;       Code here
                this._DynamicProp := value  ;       Value holds the new value
            }                               ;     End of setter
        }                                   ;   End dynamic property
    }                                       ; End class

That's the basics of making a dynamic property.  
There's more to it than that, as we'll discuss, but this is the general structure of it.  

Let's make some functional code that shows the get and set methods being activated.

    obj := Example()            ; Make an example object
    obj.dyn := 'AutoHotkey'     ; Activates set
    MsgBox(obj.dyn)             ; Activates get
    
    class Example {
        ; Add a dynamic property
        dyn {
            ; Only "get" and/or "set" can be used in a dynamic property.
            
            ; Runs in response to the dynamic property being accessed
            get {
                return 'You just accessed the dyn property.'
            }
            
            ; Runs in response to the dynamic property being changed
            set {
                MsgBox('You assigned ' value ' to the dyn property.')
            }
        }
    }

### Class dynamic properties

Just like everything else in a class, dynamic properties can be `static`.  
This causes it to be a setter/getter for the class.  
At this point, this should be pretty obvious.  

### The `get` method

The `get` method is the getter of AHK.  
It runs code in response to the user trying to access, or "get", the property.  
This is what makes a getter useful. Being able to run code in response to the property being accessed.  

Let's say you have a class and it has a property that stores a pure number.  
However, when you "get" the number, you want it to be formatted with commas in it.  
But we don't store numbers with commas in them.  
So the user can get the number and convert it OR we could write a getter to do the work.  
A getter can format the code as desired before it gets returned to the caller.

    ; test the setter and getter
    MsgBox(Example.num)
    Example.num := 123456789
    MsgBox(Example.num)

    class Example {
        static _num := 1000000                          ; num backfield
        static num {                                    ; num dynamic property
            get {                                       ; Getter
                return this.add_commas(this._num)       ; Return the formatted number
            }
            
            set {                                       ; Setter
                this._num := value                      ; Set the new value
            }
        }
        
        static add_commas(num) {                        ; Method to handle adding commas to numbers
                snum := String(num)
                len := StrLen(snum)
                next := Mod(len, 3)
                if !next
                    next := 3
                str := ''
                loop parse snum
                    if next
                        str .= A_LoopField
                        ,next--
                    else
                        str .= ',' A_LoopField
                        ,next := 2
                return str
        }
    }

#### Read-only properties with `get`

If you ever want to make a property read-only, make a dynamic property and only give it a getter.  
If a dynamic property lacks a setter and you try to set it, AHK will throw a read-only property error.  

    ; Use pi to calculate area
    radius := 3
    area := Round(math.pi * radius * radius, 5)
    MsgBox('A circle with radius ' radius ' has an area of ' area '.')
    
    ; Throw a "read-only property" error by trying to assign a value to it
    math.pi := 2
    
    class math {
        static pi {
            get {
                return 3.14159
            }
        }
    }

### The `set` method

The `set` method is the setter of AHK.  
It runs code in response to a value being assigned to the dynamic property.  
Similar to `get`, set is really useful because we can run code in response to the property being altered.  

Scenario: We have a property and want to make sure it's ALWAYS an integer.  
If we make a setter, we can set it up to check the value and ensure it's set to an integer.  
In fact, validation is a core uses of setters.  

    example.num := 50                                               ; Set integer
    MsgBox(example.num)                                             ; Show it
    example.num := 9.99999                                          ; Set float
    MsgBox(example.num)                                             ; The fractional part was removed
    example.num := 'dog'                                            ; Set to a string (ERROR!)

    class example {
        static _num := 0                                            ; Backfield for num
        static num {                                                ; num property should always be an int
            get {
                return this._num                                    ; Return backfield
            }
            
            set {
                if IsNumber(value)                                  ; Check if it's a number
                    this._num := Integer(value)                     ; If yes, cast it to integer
                else throw Error(                                   ; Otherwise, notify user of error
                    'You assigned a non-number to example.num',
                    A_ThisFunc,
                    'Value: ' value
                )
            }
        }
    }

#### The hidden `Value` parameter of `set`

If you haven't noticed yet, the `set` method has a hidden `Value` parameter.  
This parameter is what stores the new assigned value.  
`Value` has been used many times so far, and will be used again, including in the next example.  

### Backfields - Storing dynamic property values

Where is the value of a dynamic property stored at?  
This is something I struggled with when I started working with classes in v1.  
"How can a dynamic property be a method and also store a value?"  
And there's a perfectly logical answer. It can't.  
Dynamic properties are methods. They can't hold a method and a value.  
Instead, you would store the value in another property.  
This is where "backfields" come in.  
This an "unofficial best practice" type of thing.  
You make another property with the same name as the dynamic property, but you start it with an underscore.  
The underscore is what makes it a backfield and acts as a mark that the property is "internal".  

Let's say there is a dynamic property called `age` that contains a setter and getter.  
`age` isn't where the value is stored.  
`age` is the setter/getter and they would use a backfield called `_age` to store the actual value.  

This also ties in with abstraction.  
We don't document backfields.  
Even though they DO contain the number, they're not meant for the user to interact with.  
Instead, we document the dynamic property `age` as though it were the thing holding the value.  
We've abstracted away the unimportant stuff. Do you think anyone cares you used a backfield to store the value and that the setter is validating the data assigned?  
No. They don't. Not at all.  
It's a property containing an age. It can be set. It can be gotten. That's all that matters.

Here's an example of a class with an `age` property setup just like we mentioned.  

    Example.age := 10
    MsgBox(Example.age)
    Example.age := 500
    

    ; An example class containing an age
    ; Properties:
    ;   age - Contains the age of a person
    ;         This value can be from 0 to 125
    class Example {
        ; Add a dynamic property
        static age {
            ; Introduction to a fat arrow function
            ; We'll learn more about this later
            ; It's a quick way to write function that returns an expression
            get => this._age
            
            ; We use our setter to valide the age given then store it
            set {
                ; If not a number, error!
                if !IsNumber(value)
                    throw Error('Age must be a number.', A_ThisFunc, 'Type provided: ' Type(value))
                
                ; if not in bounds, erro!
                if (value < 0 || value > 125)
                    throw Error(
                        'Bad age range.'
                        '`nAge must be a number bewteen 0 and 125.',
                        A_ThisFunc,
                        'Age provided: ' value
                    )
                
                ; If the thread makes it hear, it's a valid age
                ; Assign it to the age backfield
                this._age := value
            }
        }
    }

> "But Groggy, can't people just directly access _age?"  

Yes, they could.  
If they want to look through your code and find that property and change it, then that's on them.  
If the code fails, it's a "them problem", not a "you problem".  
In AHK we can't protect our class properties with access modifiers. We don't have them.  
Everything in AHK is considered "public" and that's how the language is designed.  

If someone chooses to go against your documentation, they can deal with consequences and they can fix any problems it causes.  

### Dynamic property parameters

Yes, dynamic properties can have parameters.  
Earlier, I said dynamic properties are written like functions without parentheses.  
That was more accurate than you probably realized.  

Dynamic properties are pretty much only properties in name.  
They emulate being an property but everything about them performs like a funciton.  
And now we're reinforcing that by showing they can use parameters, like a function can.  

To create a dynamic property that uses parameters, define it exactly like a function but replace the parentheses with square brackets.  

    ; See how much they look alike?
    class example {
        
        ; Methods use ()
        method(req, opt:=0, var*) {
            
        }
        
        ; Dynamics use []
        dynamic[req, opt:=0, var*] {
            get {
                
            }
            
            set {
                
            }
        }
    }

The parameters of dynamic properties are the exact same kind functions use.  
You can have required, optional, variadic, and VarRef params.  
Required params must be first and there can only be one variadic param and it must be last.  
Like I said, exact same parameter setup as a function.  

Let's write some example code showing a dynamic property using different parameters. 

    ; Use the setter with parameters
    example.dyn['setting it',,'a', 'b', 'c'] := 1
    
    ; Uset the getter with parameters
    MsgBox(example.dyn['getting it', 42, 1, 2, 3, 4, 5, 6, 7, 8, 9])

    class example {
        static dyn[req, opt:="Didn't set it", arr*] {
            get {
                result := req '`n' opt
                for item in arr
                    result .= '`n' item
                return result
            }
            
            set {
                MsgBox(
                    value
                    '`n' req
                    '`n' opt
                    '`n' arr[1] ' ' arr[2] ' ' arr[3])
            }
        }
    }

If a dynamic property has no parameters, don't include the square brackets.  
That's bad syntax and it'll throw and error.  
Only include them when you're including one or more parameters.  
Otherwise, write them like we've been writing them prior to this section.  

> "When would I use dynamic parameter property...?"  

That's up to you.  
You'll get sick of hearing it, but it's another tool.  
You decide when you want to use it. Or not use it.  

If you ever find yourself using dynamic properties and you have some reason to pass in a parameter when you set or get a value, that's when you'd use it.  

> "You suck at this. Seriously, give us a real example!"  

Oh my gawd, fine!  

Let's say we have a class that contains a string.  
Sometimes you want that string to be in all `UPPERCASE`.  
Sometimes you want all `lowercase`.  
And sometimes you want `Title Case`.  

You could use a dynamic property getter with an optional parameter to do that.  
When using the property, include the case type with it: `classname.propname['Upper']`  

    Example.title := 'THe sHawsHanK reDempTioN'
    MsgBox(
        Example.title['']                                       ; As-is
        '`n' Example.title['lower']                             ; lowercase
        '`n' Example.title['uper']                              ; uppercase (even though it's mispelled)
        '`n' Example.title['TITLE']                             ; title case
    )
    
    class Example {
        static title[style:=''] {
            get {
                switch SubStr(style, 1, 1), 0 {                 ; First letter is all that matters
                    case 'u': return StrUpper(this._title)      ; u for uppercase
                    case 'l': return StrLower(this._title)      ; l for lowercase
                    case 't': return StrTitle(this._title)      ; t for title case
                    default: return this._title                 ; Everything else defaults to as-is
                }
            }
            
            set => this._title := value                         ; Anothe courtesy fat arrow example
        }
    }

### Dynamic properties vs making getters and setters

Some people might be looking at dynamic properties and saying "They're methods..."  
Honestly, I wouldn't argue with you on that point.  
Pretty much anything you can do with a dynamic property you can code yourself with setter/getter methods and just slightly modified syntax.  
But I will advocate for dynamic properties because using them looks cleaner IMO.

    ; Using dynamic properties vs using accessors and mutators
    Example.alpha := 'dynamic'
    Example.SetBravo('getter setter')

    Msgbox('Example.alpha: ' Example.alpha
        '`nExample.GetBravo(): ' Example.GetBravo())

    ; In this code we have the backfields _alpha and _bravo
    ; _alpha is serviced by the dynamic property
    ; _bravo is service by the GetBravo() and SetBravo() methods
    ; They do the exact same thing but in differently coded ways
    class Example {
        static _alpha := ''
        static alpha {
            get {
                return this._alpha
            }
            set {
                MsgBox('Running dynamic setter code.`nValue: ' Value)
                this._alpha := Value
            }
        }
        
        static _bravo := ''
        static GetBravo() {
            return this._bravo
        }
        static SetBravo(Value) {
            MsgBox('Running setter method code.`nValue: ' Value)
            this._bravo := Value
        }
    }

### AHK does not have class access modifiers

Class access modifiers were mentioned earlier and I wanted to clarify what they were real quick.  

In some languages, you can mark your properties and methods as private or public.  
If a property is private, nothing outside of the class can modify the property.  
If you have a private property, you need a public getter and setter for it if it's going to be changed from outside the class.  

AHK does **not** have a concept of public and private.  
Everything in AHK is public.  
However, if you branch out to other languages like C++, C#, Java, Ruby, or Swift, you'll encounter these modifiers.  
Even JavaScript, which didn't have them for years, added private properties in ES2022.  

Maybe we'll get them in v2.1?  
Or maybe v3 when that comes out 50 years from now?  

Things I can suggest to help make it clear what methods and properties a user should use (public) vs ones they shouldn't (private):

* In the class documentation, only document public things.  
  AKA the stuff you want the user to know about.  
* In the body of the class, move public members to the top and private members to the bottom.
* Use comments to label each group, marking the bottom ones as `PRIVATE` or `INTERNAL`.

And some example code to go with it:

    ; A class for doing something really useful
    ; Properties:
    ; age - Tracks the user's age.
    ;       This number must be between 0 and 125.
    ; 
    ; Methods:
    ; quit() - Causes the script to shut down
    class example {
        ; === User members ===
        static age {
            get => this._age
            set {
                if !IsNumber(value)
                    throw Error('Age must be a number.', A_ThisFunc, 'Type provided: ' Type(value))
                if (value < 0 || value > 125)
                    throw Error('Bad age range.')
                this._age := value
            }
        }
        
        static quit() => ExitApp()
        
        ; === Private ===
        static _age := 0
    }

## Special class member names

In AHK, you can name a method or property anything you want as long as it conforms to [AHK's naming rules](https://www.autohotkey.com/docs/v2/Concepts.htm#names).  
However, there are certain names that have special meaning when added to a class.  
These methods and properties add different functionality to your classes and objects.  
We've already mentioned a couple of them: `Call()` and `__New()`  
But there are more than that, and each has its own unique functionality.

Methods: 
* `Call()`: Called when the object is called.
* `__New()`: Called when a new object is created.
* `__Delete()`: Called when an object is destroyed.
* `__Enum()`: Called by a for-loop to get an enumerator.
* `__Init()`: Used by AHK to initialize the object.  
  (Don't mess with this method. Seriously.)

Meta-Functions:
* `__Call()`: Called when an undefined method is used.
* `__Get()`: Called when an undefined property is accessed.
* `__Set()`: Called when an undefined property is assigned a value.

Properties:
* `__Item`: Called when array syntax/item syntax is used with an object.  

### Make anything callable with `Call()`  

Putting parentheses after something is what we define as "calling" something.  
Anything that can be "called" in AHK is callable because it has a `Call()` method.  
The language is setup so that `obj.Call()` and `obj()` mean the same thing.  
By using only `()` after a name, it's inferring that you want `.Call()`.  
This applies to AHK's built-in functions:
    
    ; Using only ()
    arr := Array('auto', 'hotkey', 'v2')
    MsgBox(arr[1] arr[2] ' ' arr[3], 'GroggyGuide')

    ; Using .Call()
    arr := Array.Call('auto', 'hotkey', 'v2')
    MsgBox.Call(arr[1] arr[2] ' ' arr[3], 'GroggyGuide')

Ready to have your mind blown?  
Functions are actually objects.  
I'll let that sink in for a second.  

. . .

Want proof?  

    ; Assign a property to an AHK function
    MsgBox.test := 'AutoHotkey'
    ; Use the call method to display the test property
    MsgBox.Call(MsgBox.test)

More proof?  

    ; Do the function have a call method?
    if (my_func.HasMethod('Call'))
        MsgBox('Yes. Funcitons are objects and they have a Call() method.')
    
    ; Make a function
    my_func() {
        return 'hi'
    }

Still not convinced?

    ; Check if a function inherits from the object class
    if (my_func is Object)
        MsgBox('Yes, my_func is a type of object.')

Crazy, right?  

Let's get back to classes.  
If you want your instance objects to be callable, add a `Call()` method to the class.  
And if you want your class to be callable, add a `static Call()` to the class.  

A quick reminder about adding `static Call()` to a class:  
This will remove the static call that normally comes with a class to create instance objects.  
There's nothing wrong with overriding this method, but be aware that you're replacing its ability to generate objects.  
There are times when this is the desired outcome so you can make your class usable by being called without having to worry about generating unwanted objects.  

In the event you want to add your own custom `static Call()` but also make use of the original, I refer you to the section about [`Base` and `super`](#the-base-property-and-hidden-super-parameter) because I've already covered how to do that.  

But here's the code:

    class my_class {
        static Call(params*) {
            ; Call the original Call() method
            super.Call(params*)
            
            ; Your additional code goes here
        }
    }

A really good example of using `static Call()` is found in the section where we [created an auto-clicker](#creating-an-auto-clicker-using-a-class).  
In that code example, the class is made callable to toggle the auto-clicker on and off with the added bonus of disabling object creation.  

Syntax:

    ; Causes an object ot be callable
    ; params* = Any amount of parameters you want to add
    Call(params*) {
        return 'value'
    }

Let's make a an example of a class that generates callable objects.  
Criteria for this class: 

* The object will generate a number between 1 and 100 when called.  
* The number should be returned.
* The number should also be logged.
* The log should contain every number generated by the object.
* There should be a property that provides the last generated number.

This is an example of how we would do this:

    inst := Example()                                   ; Make a new instance of the object
    n1 := inst()                                        ; Generate a random number
    n2 := inst()                                        ; And another number
    n3 := inst()                                        ; And a last one

    MsgBox(
        'n1 var = ' n1                                  ; Show first num 
        '`nn2 var = ' n2                                ; Show second num 
        '`ninst.last = ' inst.last                      ; Show third num using .last property 
        '`n`nLog:`n' inst.get_log()                     ; Show full log
    )

    class Example {                                     ; Make a class
        ; === User Stuff ===
        Call() {                                        ; Instance objects are callable
            num := Random(1, 10)                        ;   Generate a random number
            this.log.Push(num)                          ;   Save to log
            return num                                  ;   return number
        }
        
        get_log() {                                     ; Shows log of numbers
            txt := ''                                   ;   Text containing all logs
            if (this.log.Length < 1)                    ;   If no logs
                txt := 'NONE'                           ;     Set to none
            else for index, item in this.log            ;   else go through each log
                txt .= 'Roll ' index ': ' item '`n'     ;     Add roll number and generated
            return txt                                  ;   Show all numbers
        }
        
        ; === Internal Stuff ===
        log := []                                       ; Used to store every roll done by this object
        
        last {
            get => this.log[this.log.length]            ; Fat arrows are discussed in their own section later
        }
    }

### `__New()` and `__Delete()`, the constructor and the deconstructor

<Delete runs when the reference count for an object reaches 0>

When a new object is created, the first thing AHK does is check for a constructor.  
Meaning it checks to see if the object has a `__New()` method.  
If the object has one, that method is called to help initialize, or "construct", the object.  
It runs any code that needs to be ran, deals with the parameters provided by the user, initializes properties in the object, and whatever else needs to be done in reaction to the object being created.  
This is the purpose of a constructor in any OOP language.  

When an object is being destroyed, AHK checks for a deconstructor.  
Which means it checks for a `__Delete()` method, just like it checked for __New when the object was made.  
This is usually done for maintence or cleanup reasons.  
It can also be used to save information you might not want lost when the object is destroyed.  
The deconstructor allows code to be ran in reaction to it being in the process of being destroyed.  
This can be a useful thing in certain situations, but `__Delete()` is not something you'll see commonly used.  
It's a tool that's there if you need it.

Syntax:

    ; Runs when a new object is constructed
    ; Any amount of parameters can be passed in
    ; When a class is called to create the object,
    ; it generally passes its params to __New()
    __New(params*) {
        
    }
    
    ; Runs when an object is destroyed
    ; Generally, no parameters are defined as none are passed in.  
    ; This method is called by AHK in realized to the object being destroyed.
    ; And it doesn't pass in any parameters.
    __Delete() {
        
    }

Let's make an example class and come up with some "features" we want to add to it:  

* The main class should track how many objects it has created.  
* The main class should also track how many objects are still left.  
* And each object crated should have it's on unique ID called `uid`.  

Time to implement it:  

    ; Run a test using the class
    test()
    
    test() {
        ; Create 5 different objects
        objA := my_class()
        objB := my_class()
        objC := my_class()
        objD := my_class()
        Sleep(250)
        objE := my_class()
        
        ; View the UIDs of each
        uids := ''
        loop parse 'ABCDE'
            uids .= '`n' obj%A_LoopField%.uid
        MsgBox('The Sleep(250) is apparent in the 5th uid: ' uids)
        
        ; Destroy 3 of the objects
        objA := 0
        objC := 'hi'
        objD := []
        
        ; Showing the tracked data
        MsgBox(
            'my_class has created a total of ' my_class.objects.created ' objects.'
            '`nOf those, there are ' my_class.objects.active ' still active.'
        )
    }
    
    class my_class {
        ; Tracks total objects created and number of active objects left
        static objects := {created:0, active:0}
        
        ; Using the current DTS with the total objects created to create a unique ID
        static get_uid() {
            return A_Now A_MSec this.objects.created
        }
        
        ; Each new object made, add 1 to created and 1 to active tracker
        __New() {
            my_class.objects.created++
            my_class.objects.active++
            this.uid := my_class.get_uid()
        }
        
        ; At destruction, remove 1 from the active tracker
        __Delete() {
            my_class.objects.active--
        }
    }

### `__Enum()` the enumerator

For those who aren't familiar with the word "enumeration", it's a fancy term meaning "to go through something one thing at a time".  

Enumeration comes from the latin *enumerare* which means "to list" or "to count up".  
That's pretty much what an enumerator does. It has a list of things and it counts/iterates through them.  

A really easy way to explain this is by using a real life example.  
In this example ***you*** are going to be an enumerator object and you have a list of names.  
I am going to be the for-loop that needs those names.  
As an enumerator, here's what is expected of you:  
1. Have a list of *something*.  
2. Every time I say "next!" I want you to tell me the next name on the list.  
3. Start with first name and cross each name off after you've given it to me.  
4. When there are no more names, say "End of list" and then throw the list in the trash.  

This is EXACTLY how an enumerator object works with a for-loop.  
   
1. An enumerator has a list, usually an array, of items.  
   It can be more complex, but ultimately there needs to be some type of list of items.  
2. Every time the for-loop calls the enumerator (says "next!"), it should save the next value/set of values ByRef and also returns true.
3. The value/set of values also need to be removed from the list of things.  
4. When the list of things is empty, the enumerator should return false.  
   This signals to the for-loop "No more items. Break loop."  
   And as a thanks for its service, the for-loop destroys the enumerator and puts it out of its misery.  

Now that we're caught up on enumerators, how does it tie in with `__Enum()`?  
When you pass an object to a for-loop, the first thing it does is look for an `__Enum()` method so it can get an enumerator object.  
If the object doesn't have an __Enum, then the object itself is treated like an enumerator, which usually results in an error being thrown because the object isn't set up to be an enumerator object.  

Array's come with an `__Enum()` method and the docs tell us so.  
Consider all 3 examples below work the same way

    arr := ['alpha', 'bravo', 'charlie']
    
    ; 1. Make an enumerator object using __Enum() and then use it
    enum := arr.__Enum()
    for index, value in enum
        MsgBox('Index: ' index '`nvalue: ' value)
    
    ; 2. Call __Enum() directly with the for-loop
    for index, value in arr.__Enum()
        MsgBox('Index: ' index '`nvalue: ' value)
    
    ; 3. Omit __Enum() because the for-loop uses it automatically
    for index, value in arr
        MsgBox('Index: ' index '`nvalue: ' value)

`__Enum()` is not the only thing that can return an enumerator object.  
Any method can return an enumerator if it's designed to.  
Example: ALL objects in AHK inherit a method called `OwnProps()`. Its even mentioned in the [inheritance section](#inheritance).  
This method creates an enumerator object containing a list of all "own properties".  

> "What in the hell is an ***own*** property??"  

Great question!  
It's a property that's added to an object, not inherited.  
If you make an array, it has a length and capacity property but no "own properties".  
Length and capacity are inherited so they're not own properties.  
If you add a property to the array, that is the array's first "own property".  
Do not confuse the object's properties with the array's values.  
They are not the same.  

The reason I used an array object as the example is because arrays contain two different enumerators.  
The `OwnProps()` method creates an enumerator containing all "own properties".  
The `__Enum()` method creates an enumerator containing all the values in the array.  

    arr := [1, 2, 3]                        ; Make a new array object
    arr.test := 'AHK'                       ; Add a property to the array object
    MsgBox('Array items: ' arr.Length)      ; Proof the length property exists
    
    for prop, value in arr.OwnProps()       ; Loop through array object's own properties
        MsgBox(prop ': ' value)             ;   Only "test", no "Length" or "Capacity"
    
    for index, value in arr.__Enum()        ; Loop through the array's elements
        MsgBox(prop ': ' value)             ;   1, 2, and 3 are shown

Syntax:

    ; The __Enum meta-function returns an enumerator object
    ; This provides a list of items to a for-loop, one item at a time
    ; param_total = The total number of parameters received each iteration  
    ;               Normally this is 1-2 but can be as high as 19
    ;               for value in obj would pass in a 1
    ;               for index, value in obj would pass in a 2
    ;               for index, value, extra in obj would pass in a 3
    __Enum(param_total) {
        
    }

While I don't have a really clever example of making an `__Enum()` method, I will show you an easy way to make a class that's identical to a normal object but can be passed directly to a for-loop.  
You create an `__Enum()` method and have it return the enumerator from the `OwnProps()` method.  
This allows the object to be passed to the for-loop without having to include `.OwnProps()`.  

    obj := MyObject()                   ; Make a new basic object
    obj.test := 'Hi'                    ; Add a first property
    obj.language := 'AHK'               ; Add a second property
    obj.time := A_Hour ':' A_Min        ; Add a final property
    
    for prop, value in obj              ; Pass object directly to for-loop
        MsgBox(prop ': ' value)         ;   Lists all own props
    
    ; Create a class that's based on the Object class
    class MyObject extends Object {
        ; Add an __Enum that for-loops can use
        __Enum(param_total) {
            ; Return the OwnProps enumerator
            return this.OwnProps()
        }
    }

### `__Init()`  

I'm only mentioning this one for the sake of education.  
This is the method that AHK uses to initialize things.  
It's really not meant for the user to mess with unless you REALLY know what you're doing.  
If you have use for __Init(), your skills are probably far beyond this guide.  

Seriously. Don't mess with it.  
You want the `__New()` method, not this.  

(All the scripts I've written, help I've given, and guides I've composed, I've never come up with a need to use or show the use of this method.)

## Meta-functions: Handling undefined things

AHK has three special methods called "meta-functions".  
Meta-functions are provided so that the coder can react to actions involving undefined things.  
There are three actions you can take with any class:  

* **Call**ing a method
* **Get**ting a property
* **Set**ting a property

Each meta-function runs code in reaction to one of those things being done with an undefined item.  

* `__Call()`: Runs when an undefined method is called.
* `__Get()`: Runs when an undefined property is accessed.
* `__Set()`: Runs when an undefined property is assigned a value.

While it's easy to think of meta-functions as "methods that handle undefined things", it's more accurate to think of them as "methods that let you override AHK's default behavior for undefined things."  

When you call an undefined method, AHK's default behavior is to throw an error.  
__Call() allows you to run code instead of that default response happening.  

When you use an undefined property, AHK's default behavior is to throw an error.  
__Get() allows you to run code instead of that default response happening.  

And when you set and undefined property, AHK's default behavior is to define that property for you and then assign that value.  
__Set() allows you to run code instead of that default response happening.

Let's go over each one of these.

### `__Call()` - Handles undefined method calls

If an undefined method is called and the class has a `__Call()` meta-function, it'll run the meta-function instead of throwing an error.  
This allows the user to handle the situation instead of defaulting to AHK throwing the error.  
`__Call()` applies to instance objects: `instance.undef_method()`  
`static __Call()` applies to the class object: `my_class.undef_method()`  

Syntax:  
Called in response to an undefined property being used.  
The __Call meta-function requires two parameters:
  
    __Call(prop_name, dyn_param_arr) {
    }

  * `prop_name`  
    Receives a string containing the name of the method called.
  * `dyn_param_arr`  
    Receives an array containing all parameters passed in.  
    If there are no params, the array is empty.


Let's say we make an object and then call `obj.Derp()`.  

1. AHK checks if `Derp()` exists and runs it.
2. If `Derp()` is not defined, AHK checks for `__Call()` and runs it.  
3. If `__Call()` is not defined, AHK throws an error to notifiy the user.  

If you don't have a need to handle undefined method calls and you're OK with AHK throwing an error, you'll never use this meta-function.  
But in the future, if you find a scneario where you need this sort of control in your code, you now know how to do it.  
It's another tool that you can choose to use.  

Let's make a __Get() method that shows a custom snarky message then force closes the script.  

    Example.greet()     ; Call a defined method
    Example.derp()      ; Then call an undefined method

    class Example {
        static greet() {
            MsgBox('Hello!')
        }
        
        ; Activate when an undefined method is used
        static __Call(name, params) {
            ; Code that handles whatever you want to have happen
            ; In this case, we're posting a message then exiting the script
            Msgbox('Ohhhhhh, you messed up!'
                '`nYou know ' name '() isn`'t a method!'
                '`nThe script will close as soon as you hit OK!'
            )
            ExitApp()
        }
    }

### `__Get()` - Handles undefined property usage

When a class has a `__Get()` meta-function, this method will be called in response to an undefined property being accessed or used.  

This works the same as __Call works for methods: it allows the user to choose how the situation is handled instead of defaulting to AHK throwing an error.  
`__Get()` applies to undefined properties of instance objects.  
`static __Get()` applies to undefined properties of the class.  

Syntax:  
Called in response to an undefined property being used.  
The __Get meta-function requires three parameters:
  
    __Get(prop_name, dyn_param_arr) {
        ; Something is expected to be returned from "get"
        return 
    }

  * `prop_name`  
    Receives a string containing the name of the property being used.
  * `dyn_param_arr`  
    Receives an array containing all parameters passed in.  
    This only applies to dynamic properties.  
    If there are no params, the array is empty.


Let's say we make an object and then use an undefined property: `MsgBox(obj.UndefProp)`  

1. AHK checks if `UndefProp` exists and gets its data.  
2. If `UndefProp` is not defined, AHK checks for `__Get()` and runs it.  
3. If `__Get()` is not defined, AHK throws an error to notifiy the user.  

It works pretty much the same as __Call, except for properties.  

    MsgBox(Example.greet)           ; Use a defined property
    MsgBox(Example.derp)            ; Use an undefined property

    class Example {
        static greet := 'Hello'
        
        ; Activate when an undefined property is used
        static __Get(name, params) {
            ; Code that handles whatever you want to have happen
            ; In this case, we're posting a message then exiting the script
            Msgbox('Ohhhhhh, you messed up!'
                '`nYou know ' name ' isn`'t a property!'
                '`nThe script will close as soon as you hit OK!'
            )
            ExitApp()
        }
    }

Like __Call, you're not expected to use this.  
Add it to the list tools you're learning about.

### `__Set()` - Handles the setting of properties

Some of you might have already pieced together that when you assign a value to an undefined property, AHK creates the property and assigns the value to it.  
That's the default behavior.  
And the purpose of a meta-function is to allow us to override default behavior.  

This is why `__Set()` is the unique one of the bunch.  
Adding this method to your class will cause it to run every time an undefined property is added.  
This allows you to decide how setting the property is handled.  
You could set the value.  
You could run code in response to a specific value or a specific property name being used.  
Whatever you want to do.  

Syntax:  
Called in response to an undefined property being assigned a value.  
The __Set meta-function requires three parameters:
  
    __Set(prop_name, dyn_param_arr, value) {
        ; Code to run each time a new property is set
    }

  * `prop_name`  
    Receives a string containing the name of the property being set.
  * `dyn_param_arr`  
    Receives an array containing all parameters passed in.  
    This only applies to dynamic properties.  
    If there are no params, the array is empty.
  * `value`  
    Receives the value assigned to the property.

If we assign a new property to an object: `obj.num := 42`

1. AHK first checks for the `__Set()` meta-function and if it exists, it runs it.
2. If `__Set()` is not defined, AHK defines the property and then assigns the value for you:  
   `obj.DefineProp('my_num', {value: 42})`  
   Yes, that's the technical way to define a property. AHK does all that when you use `:=`.  
   Are you understanding abstraction yet?  

> "Hey Groggy! What if I want to add a property in my code without having __Set activate?"

You have that option.  
I just mentioned the proper way to define a property.  
Using the `DefineProp()` method with a value descriptor object will not activate the __Set meta-function.  

    Example.test1 := 'Operator assignment'              ; Assignment activates __Set
    descriptor := {value:'DefineProp() assignment'}     ; Make a descriptor object
    Example.DefineProp('test2', descriptor)             ; DefineProp() does not activate __Set

    MsgBox(                                             ; Show both values are added
        'Example.test1: ' Example.test1
        '`nExample.test2: ' Example.test2
    )

    class Example extends Object {
        static __Set(name, param_arr, value) {          ; Runs whenever an assignment is made
            MsgBox('Caught you!'
                '`nYou want this: ' value 
                '`nAssigned to here: Example.' name
            )
            this.DefineProp(name, {value: value})       ; Define the property and value
            
            ; this.%name% := value                      ; Not this! This would cause an infinite loop
        }
    }

Descriptors are covered in that other GroggyGuide I keep mentioning. Link at the bottom.

### Recap

That covers all three meta-functions.  
You have three new tools to use.  

`__Call()` handle default behavior of undefined methods being called.  
`__Get()` handle default behavior of undefined properties being used.  
`__Set()` handle default behavior of undefined properties being assigned.  

Here's one last example I wrote up and decided to include:

    MsgBox(Example.derp)                                ; Use an undefined property
    MsgBox('Fuse: ' Example.fuse['a', 'b', 'c'])        ; Special fuse property
    arr := Example.split['Auto|Hot|Key', '|']           ; Special split property
    for value in arr                                    ; Loop through array values
        MsgBox('Split ' A_Index ': ' value)             ;   And show each element
    
    class Example {
        static default_value := '<UNSET>'
        static __Get(name, params) {                    ; Called when undefined methods are used
            if !params.Length                           ; If no params
                result := name ': ' this.default_value  ;   use default value
            else switch name, 0 {                       ; Switch check names
                case 'fuse': result := fuse(params)     ; if fuse, run and return fuse fn
                case 'split': result := split(params)   ; else if split, run and return split fn
                default: throw Error(                   ; Otherwise throw an error
                    'Invalid action.',                  ; Invalid word with params provided
                    A_ThisFunc
                )
            }
            return result
            
            ; Fuses multiple array elements into one
            fuse(arr) {
                str := ''
                for item in arr
                    str .= item
                return str
            }
            
            ; Splits a string into array elements
            split(params) {
                arr := []
                loop parse params[1], params[2]
                    arr.Push(A_LoopField)
                return arr
            }
        }
    }

## The `__Item` property

## The `__Class` property

Everything in AHK comes from some class.  
The `__Class` property tracks which class something came from.  
The `Base` tracks object inheritance. Meaning the prototype that the object is based on.  
`__Class` is tracks class in heritance. It stores the name of the class that created it.  
An instance object's __Class property will always be the name of the class that created it.  
A class object's __Class property will always be Class. That's because a class is always created from the Class class.  

    inst := Example()                           ; Create an instance of Example

    MsgBox(
        'inst.__Class: ' inst.__Class           ; Shows: Example
        '`nExample.__Class: ' Example.__Class   ; Shows: Class
    )

    class Example extends Array {               ; Create a class extending from Array
    }

While not a common property to see used, it does serve a purpose in certain circumstances.  

# Fat Arrows
Fat arrows are handy way to write short functions.  
They are not needed. It's considered syntax sugar, or something that streamlines code or makes it easier to use.  
But I'm going to go over them b/c they're applicable to classes.  

To make a fat arrow function, you use the fat arrow operator =>  

    (params) => Expression

This type of function is called an anonymous function because it has no name or identifier.  
To create a named function, assign the fat arrow to a variable.  

    ; Fat Arrow function
    square_num := (num) => num * num
    
    ; Use it
    MsgBox('3 squared is: ' square_num(3))

The best way to think about the fat arrow operator:
- It makes a function where all you supply is the part after "return".  
- It doesn't need curly braces.  
- It doesn't need a name.  

    ; Normal Function
    example(params) {
        return some_expression
    }
    
    ; A little transition between the two
    ; (NOT valid code, just visualizing)
    example(params) { return some_expression }
    
    ; Function made using fat arrow syntax
    ; => replaces the: { return }
    example := (params) => some_expression
    
    ; Without an assignment, it's an anonymous function
    (params) => some_expression

Here's an example of writing a squaring function multiple different ways.  

    sq_fat := (num) => num * num    ; Assigning a fat arrow function to a variable
    sq_fat_fn(num) => num * num     ; Create a fat arrow function
    sq_fn(num) {                    ; Create a normal function
        return num * num
    }
    
    MsgBox(                         ; All 3 perform the same:
        '3 squared is: '
        '`n' sq_fat(3)
        '`n' sq_fat_fn(3)
        '`n' sq_fn(3)
    )

The expression you provide what would normally come after a return statement.  
And we know it's an expression because the return documents tell us so.  
If it's an expression, it can't include control flow like loops, if/else, switch, etc.  

    test() {
        ; A function's return statement cannot use control flow statements
        ; This is a syntax error
        return loop 3
            if (A_TickCount > 0)
                MsgBox('derp')
    }
    
    ; Equally, a fat arrow function cannot use control flow statements
    ; This is a syntax error
    test := () => loop 3
        if (A_TickCount > 0)
            MsgBox('derp')

Parameters work the same, regardless of function type.  
Pass in data you want to pass in and then use that data in the expression.  

Again, you never need to use fat arrows.  
It's there if you want to use it.  
Anything a fat arrow function can do, a normal function can do.  

So why the recap on fat arrows?  
Because they can be used when creating properties and methods.  
A method is a type of function.  
A fat arrow creates a short function.  
You can use fat arrows when applicable.  

Why to use them?  
Fat arrows can really clean up code.  
Small, basic functions become one-liners instead of taking up 3 lines.  
The syntax is minimalistic while still being descriptive.  

The inclusion of fat arrows is one of my favorite parts of v2.  
*/

; Let's create a class using only fat arrows

; Test out class:
; This will activate the dynamic property
fat_arrow_example.dynamic_prop := 'Test value'
; And this activates the setter meta-function.
fat_arrow_example.undefined_obviously := true
; Check the other properties and methods
MsgBox(
    'fat_arrow_example class properties and methods:'
    '`n.prop = ' fat_arrow_example.prop
    '`n.method() = ' fat_arrow_example.method()
    '`n.dynamic_prop = ' fat_arrow_example.dynamic_prop
    '`n.not_there (Undefined) = ' fat_arrow_example.not_there
)

; Create a class using only fat arrows
class fat_arrow_example {
    ; Fat arrow properties:
    ; This is the same as making a getter as it cannot be set.  
    ; prop {
    ;     get => 'A "getter" property. Cannot be set.'
    ; }
    static prop => 'getter property return value'
    
    ; Using fat arrows with getters and setters
    static dynamic_prop {
        get => 'dynamic_prop getter return value'
        set => MsgBox('Trying to set dynamic_prop to: ' value)
    }
    
    ; Different fat arrows methods:
    static __New() => MsgBox('the fat_arrow_example class was referenced for the first time!')
    static __Delete() => 'Nope! Classes cannot be destroyed! I have to make sure you are paying attention.'
    static __Get(name, param_arr) => 'Error: The property ' name ' does not exist.'
    static method(params*) => 'Method return value'
}


## Fat Arrow Tips
These are some tips for those who want to use fat arrows.  
2 things:
Fat arrows can do if/else
Fat arrows can do multiple steps.

- If/Else
We can't use if/else statements because they're not valid expressions. They're control flow.  
However, there's an operator called the ternary operator (?:) and it allows for decision making like if/else.  
Because ternary is an operator, it means it can be used in expressions.  
Meaning we can make decisions with fat arrows using this operator.  

    ; If-else statement
    if (ThingToCheck)
        TrueCode
    else
        FalseCode
    
    ; The same if-else with ternary operators
    ThingToCheck ? TrueCode : FalseCode

ThingToCheck is whatever condition is being checked.  
If it evaluates true, then run the TrueCode expression.  
Otherwise, run the FalseCode expression.  

Let's make a fat arrow function that tells you if something is true or false.

    ; If the value passed in evaluated as true, show true. Otherwise show false.
    TrueFalse(value) => value ? MsgBox('True') : MsgBox('False')
    
    ; Test it
    TrueFalse(1)        ; Non-zero numbers are true
    TrueFalse(0)        ; Zero is always false
    TrueFalse('Hi')     ; A string with ANY characters is true
    TrueFalse('')       ; An empty string is always false

- Multi-statements
Another trick with expressions is knowing about the multi-statement operator (,).  
Commas between statemenets creates a multi-statement.  
This allows us to perform multiple steps if needed.  
Put a multi-statment in parentheses and you have a single expression.  
Fat arrows use single expressions.  

Let's create an example method that does multiple steps.  
add_one() will increment a class property, announce odd or even, then return the string "Success"

    ; Test it
    loop 4
        MsgBox(example.add_one())

    class example {
        static number := 0
        ; Multiple steps in one expression
        ; The last statement is the returned value
        static add_one() => (this.number++, MsgBox(this.number ' : ' (Mod(this.number, 2) ? 'Odd' : 'Even')), 'Success')
    }

It might be cleaner to write things on multiple lines.  

    ; Test it
    loop 4
        MsgBox(example.add_one())

    class example {
        static number := 0
        
        static add_one() => (
            this.number++,
            MsgBox(this.number ' : ' (Mod(this.number, 2) ? 'Odd' : 'Even')),
            'Success'
        )
    }

But at this point, maybe it's better to just write it as a normal method.  

Between multi-statements and ternary operators, you can write entire code blocks on a single line.  
It's possible but consider if you SHOULD do it.  
You're sacrificing readability just to cram things on one line.   
If you need to edit it later, it'll be difficult to do.  
And fewer lines doesn't mean faster code.  

Use fat arrows when it's appropriate.  







# Documentation for AHK's built in classes

Links to all of AHK's classes can be found on the [Class Object List page](https://www.autohotkey.com/docs/v2/ObjList.htm).  
There's also a page decided to [information on objects and classes and how to use them](https://www.autohotkey.com/docs/v2/Objects.htm).  
This page contains information on objects, arrays, maps, classes, and their specifics.  
While each of those has its own dedicated class reference page, this page is more about getting the user to understand the use and purpose of all those things.  

This is the page I personally have bookmarked for the AHK docs and it's also one of my favorite doc pages.  
How geeky is that? I have a favorite doc page...

Not only does this page provide a link to the documentation of every class in AHK, it also visualizes AHK's entire class structure.  
It shows each class, where it extends from, and every class that extends from it.  
The `Any` is all the way to the left and not indented.  
That's because it's the top level class; the only class that doesn't extend from anything.  
It is THE base class from which everything else is derives.  

Next, there are four classes indented one level from the `Any` class:  
 - `Object`
 - `Primitive`
 - `VarRef`
 - `ComValue`

This means all of these classes extend from `Any`.  
And everything else indented belongs to one of those classes, with most extending from the `Object` class.  

And that's how this page is laid out.  
Great doc page!

## Doc page structure and layout

All of the documentation pages for classes are structured the same (for the most part).  
Which is good, because it makes using the docs much easier.

This is the general layout of most class documentation pages:

* Title and extension
  * Extension describes what class the current class will inherit from.  
    * e.g. `Array extends Object`
* Use and general information section
  * Explains what the class does and other general information about the class.
* Table of contents
  * Lists all available methods and properties
    * Static methods, methods, and properties
* Definitions
  * Everything listed in the table of contents has its own section.  
    This provides relevant information, like parameters for methods or contents of properties.  
* Example section
  * Provides examples of the class/object being used.  
  * Not all pages have example sections (which is unfortunate).

Some of the classes don't follow this page structure, such as GUI controls.  
Instead, they get a giant page with each control listed and the info not being well organized.  
I'm still holding out for a revamp/update to the docs where each gui control gets its own proper page.  

If you want to better understand AHK's class structure, check out my guide:  
[GroggyGuide: Everything in v2 is an object, descriptors described, the secret Any class, methods are just callable properties, and more.](https://www.reddit.com/r/AutoHotkey/comments/1hvwd64/groggyguide_everything_in_v2_is_an_object/).



































## Special class properties
### `__Class`
### `__Item`
### `Base`
### `Prototype`
## Special class methods
### `Call()`
### `__New()`
### `__Delete()`
### `__Enum()`
### `__Init()`
## Meta-functions
### `__Call()`
### `__Get()`
### `__Set()`

### 
### 



## The Big Class Cheat Sheet

This big block of text is a single giant class.  
And inside it is an example of everything you can have in a class.  
This includes all special methods and special properties.  

This is why you don't make methods or properties with the following names:  

- `Call()`
- `__New()`
- `__Delete()`
- `__Enum()`
- `__Init()`
- `__Call()`
- `__Get()`
- `__Set()`
- `__Class`
- `__Item`
- `Base`
- `Prototype`

And now for the giant example class:

    ; Description: Define a class.  
    ; A class name is required. We'll name ours "my_new_class".  
    ; All classes must extend from another class.  
    ; This determines what methods and properties your class inherits.  
    ; If no extension is provided, "Extends Object" is used by default.  
    ; This makes sense as most things in AHK are objects.  
    Class my_new_class extends some_other_class {
        
        ; === METHODS AND PROPERTIES ===
        
        ; PROPERTY
        ; Description: Properties tend to store data like numbers, strings, and objects.  
        ; These act as variables for objects.  
        ; Static properties belong to the class.  
        ; Non-static properties belong to the Prototype and are what each instance object receives.  
        static class_property := 'This property belongs to my_new_class'
        instance_property := 'This is a property all instances of my_new_class will get.'
        
        ; METHOD
        ; Description: Methods are used to run code. To "do stuff".  
        ; Static methods belong to the class.  
        ; Non-static methods belong to the Prototype and are what each instance object receives.  
        ; Methods work identically to functions.  
        static class_method(params*) {
            ; This method is called using: 
            ; my_new_class.class_method()
            MsgBox(A_ThisFunc)
        }
        
        instance_method(params*) {
            ; This method is called using: 
            ; instance := my_new_class()
            ; instance.instance_method()
            MsgBox(A_ThisFunc)
        }
        
        ; DYNAMIC PROPERTIES
        ; Description: These are properties that work like setter/getter functions.  
        ; A setter is code that runs when you assign (set) a property value.  
        ; A getter is code that runs when you access (get) a property value.  
        ; Only include square brackets if parameters are expected.  
        ; Static dynamic properties belong the class.  
        ; Non-static dynamic properties belong to the Prototype and are what each instance object receives.  
        dynamic_prop[parameters] {
            ; Get runs when the dynamic_prop is accessed.
            get {
                MsgBox('You tried to get dynamic_prop from an instance of my_new_class.')
            }
            
            ; Set runs when a value is assigned to the dynamic property.  
            ; A hidden "Value" parameter is provided containing the assigned data.  
            set {
                MsgBox('You set the value of dynamic_prop to: ' value)
            }
        }
        
        
        ; === SPECIAL PROPERTIES ===
        ; These are properties that all classes and instance objects have.
        
        ; __Class
        ; Description: A string containing the name of the class of origin.  
        ; All classes are based on the Class object. Or it wouldn't be a class.  
        ; Instance objects return the class they originated from.  
        __Class => 'my_new_class'
        static __Class => 'Class'
        
        ; Base
        ; Description: A reference to the origin of the current object.  
        ; It is the object upon which the current object is "based" upon.  
        ; This is an object reference, not a string.  
        ; Static base belongs to the class and is always a reference to the object it extends from.  
        ; Non-statc Base belongs to the instance objects and will always be a refrence to the Prototype that made them.  
        Base => my_new_class.Prototype
        static Base => Object
        
        ; __Item
        ; Description: A special dynamic property.  
        ; Including this in the class allows the class/instance to use item syntax. 
        ; obj[some_value]
        ; The __Item property is what Array and Map objects use.  
        ; Item syntax is also called array syntax.  
        ; Static __Item: The class can use item syntax.
        ; __Item: The instance objects can use item syntax.
        __Item[param] {
            get {
                MsgBox('Tried to get a property')
            }
            set {
                something := Value
            }
        }
        
        
        ; === SPECIAL METHODS ===
        ; These all have special meaning when used in a class:  
        ; __New(), __Delete(), __Enum(), __Item[], Call()
        
        ; __New()
        ; Description: Runs when the object is created. Initializes stuff.  
        ; my_new_class() is the same as calling my_new_class.__New()
        ; Static __New(): Runs the first time the class is referenced.  
        ; __New(): Runs when an instance object is created.  
        ; Instance __New is  also known as a "constructor" because it constructs an object.  
        __New(params*) {
            MsgBox('Intialize stuff.')
        }
        
        ; __Delete()
        ; Description: Runs when an object is destroyed/released.  
        ; Static __Delete(): Will never work because classes are read-only. Can't be destroyed.  
        ; __Delete(): Runs when an instance object is destroyed/released.  
        ; Instance __Delete is  also known as a "destructor" because it runs when the object is destroyed.
        __Delete(params*) {
            MsgBox('Clean up stuff.')
        }
        
        ; __Enum()
        ; Description: Used by for-loops. Provides a list of "things" to loop through.  
        ; This method is expected to return an enumerator-like object.  
        ; Static __Enum(): The class can be passed to a for-loop.  
        ; __Enum(): The instance object can be passed to a for-loop
        __Enum(params*) {
            return Enumerator
        }
        
        ; Call()
        ; Description: Makes an object callable.  
        ; Static Call(): The class can be called/run code. Also prevents the class from creating instance objects.  
        ; Call(): The instance objects can be called/run code.  
        Call(params*) {
            MsgBox('Do this stuff when called')
        }
        
        ; Description: The initialization method.  
        ; Only including for completeness and to educate.  
        ; This initializes and sets up stuff for the object.  
        ; Unless you know exactly what you're doing, don't mess with this method.  
        ; There is a 99.9% chance what you want to do should be done with the __New() method.
        __Init() {
            MsgBox("Seriously, you don't need to create __Init methods.")
        }
        
        ; === META-FUNCTIONS ===
        ; Meta-functions are used to handle "undefined" methods and properties.  
        ; These special functions can be used to run code instead of throwing an error.  
        
        ; __Call()
        ; Description: Called when an undefined method is called.  
        ; This applies to both static and instance versions.  
        __Call(method_name, param_arr) {
            MsgBox('This object does not have a ' method_name ' method.')
        }
        
        ; __Get()
        ; Description: Called when an undefined property is accessed (gotten).
        ; This applies to both static and instance versions.
        __Get(prop_name, param_arr) {
            MsgBox('This object does not have a ' prop_name ' property.')
        }
        
        ; __Set()
        ; Description: Called when an undefined property has a value set to it.
        ; This applies to both static and instance versions.
        __Set(prop_name, param_arr, value) {
            MsgBox('The value of ' value ' could not be set to ' prop_name '.')
        }
        
        ; === Nested Class ===
        ; Classes can be defined inside of classes.  
        ; Remember, it's just another type of object.  
        ; A nested class belongs to the class it's defined in and doesn't use the "static" keyword.
        ; Also, nesting a class inside another has nothing to do with inheritance or extends.  
        ; This nested class extends Array even though it is located inside the class my_new_class.
        class nested_class extends Array{
            static prop := 'belongs to: my_new_class.nested_class'
            prop := 'instance of: my_new_class.nested_class'
        }
    }



/*
The Point Class
Earlier we talked about using Point objects to encapsulate x and y coordinates. Keep them together.  
And we also talked about it having the ability to create clones.  
Let's code this.  
We're going to make a class that creates point objects.
*/

    ; Create a Point class
    class Point {
        ; Properties to store X and Y coordinates
        x := 0
        y := 0
        
        ; Constructor
        ; This runs whenever a new instance is created
        ; It receives any parameters passed in
        __New(x?, y?) {
            ; If x/y values were passed in, update the values
            if IsSet(x)
                this.x := x
            if IsSet(y)
                this.y := y
        }
        
        ; A method to create and return a clone of this point object
        clone() {
            return Point(this.x, this.y)
        }
        
        ; A method to reset x and y to 0
        reset() {
            this.x := 0
            this.y := 0
        }
    }














; === Documenting Your Class + JSDocs ===
I've mentioned documenting things.  
This is a very important part to coding in general.  
Adding a couple comments can make code easy to understand later.  

But when dealing with classes and OOP, documenting your class is paramount.  
It gives people instructions on how to use the object.  
General advice for documenting a class:
- The class itself.  
  Breifly describe what it does.  
  Include methods and properties.  
  Their descriptions should be kept minimalistic.  
  More detail can be included with their code.

- The methods
  Include a description, parameters, and return value.
  Descriptions should only include what NEEDS to be known about the method.
  Each parameter should be included and what's expected.
  Include any default values when applicable (optional params).
  If the method returns something, include that information.

- The properties
  Include a description and a type.  
  Like methods, keep the description brief and only include what needs to be known.  
  It's a good idea to inclue the type, like: String, Number, Array, Map

We're going to continue using our "point object" example.  
We'll document it with regular comments first
*/

    ; This class constructs "Point" objects
    ; Point objects contain x and y coordinates.  
    ; Constructor:
    ; point_obj := Point(x, y)
    ; Properties:
    ; X - The X coordinate of the point.
    ; Y - The Y coordinate of the point.
    ; Methods:
    ; Clone() - Creates a new Point object with the current object's values.
    ; Reset() - Resets X and Y back to 0.
    class Point {
        ; Constructor
        ; X is optional. Defaults to 0.
        ; Y is optional. Defaults to 0.
        __New(x:=0, y:=0) {
            ; Save values to object
            this.x := x
            this.y := y
        }
        
        ; Clone() - Create a duplicate of the current object.
        ; Creates a new Point using the current A new point object is created using the current object's x/y values
        ; Returns - Point object
        clone() => Point(this.x, this.y)
        
        ; Reset() - Resets the x and y coordinate to 0.
        reset() {
            this.x := 0
            this.y := 0
        }
    }

/*

Let's talk about JSDoc documentation.  

This is an optional way to document your code.  
AHK doesn't differentiate between JSDoc comments and normal comments.  
It sees both as just regular AHK comment blocks.  
However, THQBY's add-on is designed to identify and make use of JSDoc comments.  

What does that mean?  
It means using JSDoc comments and its special tags, you can build documentation INTO your code.  
The add-on then uses this information to show you how to use the code while you use it.  
Your own comments get translated into realtime documentation for using your code.  
If that sounds cool, it's because it is cool.  

To create a JSDoc comment, make a normal comment block:

    /*
    Normal comment block
    */

    /** Except add another asterisk to the opener
     * @description This is a JSDoc Comment
     */

/*
AHK sees both of these as comment blocks because they start with /* and end with */.  
However, THQBY's add-on sees /** and knows it's a JSDoc comment.  

As a general formatting rule, each line of a JSDoc comment starts with an asterisk.  
These asterisks are aligned off the first asterisk that starts the JSDoc comment block.
This is a common formatting convention and NOT a requirement.  
The only requirements for a JSDoc comment is start with this /** and end with this */.  

JSDocs uses different @tags to define information.  
There are tons of them and they can be found at the JSDoc website. Link below.  
Be aware that not all tags are supported as JSDocs are targeted at JavaScript.  
"So why does AHK use them?"  
Because AHK is very closesly structured to JS and a lot of the tags are very applicable.  
THQBY chose to implement them with AHK to help us in writing more user-friendly code.  

These @tags are how the add-on works.  
When you type something, the autocomplete and info tooltips all exist and work b/c of JSDoc comments.  
Earlier, when I mentioned my add-on enhancement update, this is what it enhances/updates.  
I rewrote the file that handles all the AHK definitions.  
The update included information for EVERYTHING and includes almost every property, method, variable, etc.  

I'm mentioning this so people will use it. It exists to make writing AHK code easier.  
It took TONS of time to create and I make no money off it. It's free. Use it.  

    https://github.com/GroggyOtter/ahkv2_definition_rewrite

If you want more information on JSDoc, check out their main site.  
This includes all tags (though this add-on doesn't support all of them).
    
    https://jsdoc.app/
    
Let's talk about some of the @tags  
Only certain tags are implemented in the add-on.  
The ones I regularly use:  
    
    - @description INFO - Describes the thing and gives information.
    - @type {TYPE} - Identifies the data type, such as String, Number, Array, Gui.Control, etc.
    - @param {TYPE} NAME - Used to identify a parameter, info about it, expected type, and whether it's optional.
    - @returns {TYPE} INFO - Describes a return value, its type, and any extra info.
    - @example - A special tag that allows you to provide example code on how to use something.  
      The code will show up in in the tooltip as syntax highlighted code.  
    - @see - Includes extra information, usually links, to other applicable things.  

The following are ones I use to make header comments.  
This is a comment that goes at the top of the file and gives information about the code.

    - @file NAME INFO - The name of the file and a description of what it does. Like @description for the whole file.  
    - @author NAME <EMAIL> - Name of the person who wrote the code.  
      Optionally, add a contact email. Must include angle brackets around email.  
    - @date DATE - The date the code was created.  
      This is not a standard JSDoc tag but a good one to include.  
    - @version X.X.X - Current version number.
      You choose what versioning system to use. Semantic versioning ([Major].[Minor].[Patch]) is most common.  
      This tag can be used with things other than the header. A class might have versions. Or even a method.  
      You choose when to track versions of something.  

Special inline tags:  

    - {@link URLHere|Hyperlink Text Here} - The link (hyperlink) tag is special.  
      Its purpose is to create hyperlinks anywhere in a JSDoc tags and can be used freely.  
*/

; Let's write come examples of using JSDocs.


; Example Header template
/*******************************************************************************
 * @file - NameOfFile.ahk - A description of what this file contains or does.
 * @author Your Name Here <OptionalEmailAddress@goes.here>
 * @date 2025-01-01 (Creation date of file.)
 * @version v1.0.0
 ******************************************************************************/


; Example of documenting a function or method:
/**
 * @description string_contains()  
 * A function that check if a string contains one of the provided words.  
 * @param {String} str - The string to check.
 * @param {Integer} [case_sense=0] - Optional.  
 * Require word matches be casesensitive.  
 * "AHK" and "ahk" would not be case-sensitive matches.  
 * @param {Primitive} word_list - Include one or more words to check for.  
 * Numbers can be used as they're converted to string.  
 * @returns {String} The first matching word is returned.  
 * If no match is found, an empty string is returned.  
 * @see {@link https://www.autohotkey.com/docs/v2/lib/InStr.htm|`InStr()` Docs}
 * @example
 * text := 'Hello, world!'
 * ; Even though hello comes first, the word "world" is returned.  
 * ; This is because "hello" is not a case-sensitive match to "Hello".  
 * word := string_contains(text, 1, 'Auto', 'Hotkey', 'hello', 'world')
 * if word
 *     MsgBox('"' word '" was found in the text!')
 */
string_contains(str, case_sense:=0, word_list*) {
    for word in word_list
        if InStr(str, word, case_sense)
            return word
    return ''
}


; Documenting a variable/property
/**
 * @description index  
 * Tracks the current index of the key_list array.
 * @type {Integer}
 */
index := 1

/**
 * @description key_list  
 * An array of keys to send in order.  
 * Used with the `index` variable.  
 * @type {Array}
 * @example
 * Send(key_list[index])
 * index++
 * if (index > key_list.Length)
 *     index := 1
 */
key_list := ['a', 'z', 'b', 'y', 'c', 'x']


/*

Some might be wondering "What if I don't use VS Code?"  
JSDocs won't negatively affect your code.  
Unless the editor you're using is designed to utilize JSDocs, they're just seen as AHK block comments.  

But you really should try VS Code and this add-on if you haven't yet.  
It's worth.

/* Learning by example:




















Let's create two different examples showing the different uses of classes.  
One that creates objects.  
One that is used as its own object.  

=== Class that creates objects ===
Earlier, we talked about the idea of a "Point object".  
It's designed to bundle x and y coordinates together.  
Now we're going to write a class that creates point objects.  
We're going to call it "new_point".  

Whenever we want to make a new point object, we call new point and provide and x and y coordinate.

    ; x50 y100
    point := new_point(50, 100)

If a parameter is omitted, that parameter should default to 0

    ; x0 y50
    point := new_point( , 50)

We'll add some methods to the class, too.  
Including the Clone() method discussed earlier and a Reset() method to reset coordinates.  
*/

; Make a new point object
point1 := new_point(, 100)
; Check the coordinates
; x is 0 because we didn't assign a value.
Msgbox('x: ' point1.x '`ny: ' point1.y)

; Make a clone of the point
point2 := point1.Clone()
; Then change point2 coords
point2.x := 7, point2.y := 7

; Values are not the same:
MsgBox('point1: x' point1.x ' y' point1.y
    '`npoint2: x' point2.x ' y' point2.y)

; Test the reset method:
point2.reset()
MsgBox('point2: x' point2.x ' y' point2.y)

; A Point object constructor class
; Point objects contain an x and y coordinate.
class new_point {
    ; Constructor
    ; Param 1 is for the X value
    ; Param 2 is for the Y value
    __New(x:=0, y:=0) {
        ; Save the values to the object
        this.x := x
        this.y := y
    }
    
    ; Method clones the current point object
    ; A new point object is created using the current object's x/y values
    clone() => new_point(this.x, this.y)
    
    ; Resets both x and y back to 0
    reset() {
        this.x := 0
        this.y := 0
    }
}

/*
Now let's create the other kind of class.  
This one doesn't create objects but is used as its own object.  
We're making an AutoClicker.  
It will include methods to start, stop, and toggle the autoclicker.  
There will also be click counter to track total clicks since script start.  
There's a method to show this count.  
We can then bind these methods to hotkeys.  
*/

; Make some hotkeys to control your code
; F1 turns the clicker on/off
*F1::autoclicker.toggle()
; F2 uses the start() method
; This starts it and if already started, does nothing
*F2::autoclicker.start()
; F3 uses the stop() method
; This stops the autoclicker vs toggling it on/off each push
*F3::autoclicker.stop()
; F4 shows the total clicks the autoclicker has done
*F4::autoclicker.show_total_clicks()

*Esc::ExitApp()

/**
 * @description An autoclicker  
 * 
 *     autoclicker.Start()  ; Starts autoclicking
 *     autoclicker.Stop()   ; Stops autoclicking
 *     autoclicker.Toggle() ; Switch between start/stop
 */
class autoclicker {
    /**
     * @description Tracks if the autoclicker is running
     * @type {Integer}
     */
    static running := 0
    /**
     * @description Allow user to adjust delay between clicks
     * @type {Integer}
     */
    static delay := 1
    /**
     * @description Record total click count since starting script
     * @type {Integer}
     */
    static click_count := 0
    
    /**
     * @description Starts the autoclicker
     */
    static start() {
        ; Do nothing if already running
        if this.running
            return
        this.running := 1
        this.run_clicker()
    }
    
    /**
     * @description Stops autoclicker
     * Sets running to false
     */
    static stop() => this.running := 0
    
    /**
     * @description Toggles running status on <-> off
     */
    static toggle() {
        if this.running
            this.stop()
        else this.start()
    }
    
    /**
     * @description Main method for autoclicking.
     * Stops when running is set to false.
     */
    static run_clicker() {
        if !this.running
            return
        Click()
        this.click_count++
        callback := this.run_clicker.Bind(this)
        SetTimer(callback, -this.delay)
    }
    
    /**
     * @description Shows user total clicks
     */
    static show_total_clicks() {
        TrayTip('Clicks: ' this.click_count)
    }
}


/*

This next section is going to demonstrate each special method in use.  
There will be a basic example and a more applicable example.

Call()
__New()
__Delete()
__Enum()
__Item

__Call()
__Get()
__Set()
*/

; === Call ===
; Call makes something "callable", meaning it's the thing that happens when you inclued parentheses.  
; Adding call to your class makes the instance objects callable.  
; This example teaches more than just using call.  
; It shows crossing over data.  
; In this case, we store a count in the main class.  
; Each time an object is created, we increase the count and assign it to the new object.
; It's a simplistic concept but one that might be useful in your future code.

    instanceA := example()  ; Make one instance
    instanceB := example()  ; Make a sescond
    instanceA()             ; call first
    instanceB()             ; call second
    
    class example {
        ; Track number of objects made
        static count := 0
        
        ; Runs each time an object is created
        __New() {
            ; Increase class count
            example.count++
            ; Assign class count to this object
            this.index := example.count
        }
        
        call() => MsgBox('The index of the object called is: ' this.index)
    }

; The static version of Call() has a specific side effect.  
; Class already has a static Call(). It's what creates instance objects.  
; If you add your own static Call(), you overwrite that one it normally has.  
; By doing this, your class can do something like return a string instead of an object.  
; If you still want the default Call() behavior, I refer you to the "super" section earlier in the guide.  
; This scenario would be a good example of when to use super.

; In this next code snippet, we're going to make a class that returns a string instead of an object.
instance := example()

; example class returns a string now when called
MsgBox(
    'Type: ' Type(instance)
    '`nvalue: ' instance
)

class example {
    ; Static Call() overrides the original Call() of the class
    ; Now a string is returned
    static Call() => 'Hello'
    
    static test() {
        if (super.DefineProp = this.base.Prototype.DefineProp)
            MsgBox('Yes')
    }
}




; Examples of every "thing" in a class being used.

























; A - Define a class
Class my_cool_class extends Object {
    /** Property
     * @description 
     * A property is used to store data.  
     * A static property belongs to the class.
     * A non-static property is a property each instance will have.
     * 
     * @example
     * ; Make 2 instances of example
     * x := example()
     * y := example()
     * 
     * ; Show (get) the prop property of each one
     * MsgBox('example.prop: ' example.prop
     *     '`nx.prop: ' x.prop
     *     '`ny.prop: ' y.prop
     * )
     * 
     * ; Set properties
     * example.prop := 'class prop updated'
     * x.prop := 'x prop updated'
     * y.prop := 'y prop updated'
     * 
     * ; Show (get) the prop property of each one
     * MsgBox('example.prop: ' example.prop
     *     '`nx.prop: ' x.prop
     *     '`ny.prop: ' y.prop
     * )

     * 
     * class example {
     *     static prop := 'example class prop'
     *     prop := 'instance prop'
     * }
     */
    static c_prop := 'A Class Property'
    
    /** Instance Property
     * @description  
     * A property that will be included with all instances made by my_cool_class.  
     * The lack of the static keyword makes it an instance property.  
     * Instance properties (and methods) technically reside inside the 
     * Prototype object of the class. In this case:
     * my_cool_class.Prototype.i_prop
     * Be we don't really deal with prototype directly.  
     * The class structure itself handles that.
     * 
     * @example
    ; Make an instance object
    my_instance := my_cool_class()
    ; Get an instance property value:
    MsgBox(my_instance.i_prop)
    ; Set a new instance property value:
    my_instance.i_prop := 'Hello'
    
     * ; Define a class
     * class example {
     *     ; Define a property
     *     i_prop := 'instance property'
     * }
     */
    i_prop := 'An Instance Property'
    
    /** Class method
     * @description  
     * A method that belongs to my_cool_class.  
     * The static keyword is what defines it as a class method.  
     * 
     * Methods work almost identically to functions.  
     * This includes use of parameters and returns.
     * @param req - A required method parameter.  
     * A value MUST be provided for these parameters.  
     * Required parameters must be defined before optional and variadic parameters.  
     * @param opt - An optional method parameter.  
     * If a default value is assigned to a parameter, it becomes optional.  
     * If that parameter is omitted, the default value is used.  
     * Optional params must be defined after required params but before the variadic param.  
     * @param var - A variadic method parameter.  
     * This turns the parameter into an array and allows any number of values to be passed in.  
     * It allows for "varying" amounts of values, hence variadic.  
     * There can be only variadic parameter and it must be the last defined parameter.  
     * @returns - Any value can be returned.  
     * If no value is defined, an empty string is always returned.  
     * This is default behavior for all types of functions in AHK.
     * @example
     * ; Use the example class message method
     * example.message()
     * ; And pass in a string
     * example.message('Hello, world!')
     * 
     * ; Define a class
     * class example {
     *     ; Define a method for creating message boxes
     *     ; Optional method message can be passed in
     *     static message(msg:='No message provided') {
     *         MsgBox(msg)
     *     }
     * }
     */
    static c_method(req, opt:=0, var*) {
        ; Methods can use return exactly like functions
        return
    }
    
    /** Instance methods
     * @description  
     * A method that all instance objects will have access to.  
     * The lack of a static keyword is what defines it as an instance method.  
     * Other than that, instance methods behave the same as class methods.  
     * @example
     * ; Make an instance object
     * obj := example()
     * ; Use the message method
     * obj.message()
     * ; And pass in a string
     * obj.message('Hello, world!')
     * 
     * ; Define a class
     * class example {
     *     ; Define a method for creating message boxes
     *     ; Optional method message can be passed in
     *     message(msg:='No message provided') {
     *         MsgBox(msg)
     *     }
     * }
     */
    i_method(req, opt:=0, var*) {
        return
    }
    
    ; === Special Properties ===
    
    /** Base property
     * @description
     * All classes and instances of classes have a base.  
     * (EVERYTHING in AHK has a base property. Everything.)  
     * Base always references the object or class this item came from.  
     * It determines what properties and methods are inherited.  
     * @example  
     * my_instance := example()
     * if (my_instance.base = example.Prototype)
     *     MsgBox('Yes, this object came from the class Example.')
     * 
     * class example extends object {
     *     
     * }
     */
    base := my_cool_class.Prototype
    ; The my_cool_class class extends from the Object class
    ; So base is Object.
    static base := Object
    
    /** __Class property
     * @description
     * Contains the string name of the class this object came from.
     * Everything in AHK has this property.  
     * @example
     * ; Create an instance of example
     * instance := example()
     * ; __Class is set to "Example"
     * ; Because instance came from the Example class.
     * MsgBox(instance.__class)
     * 
     * ; Define example class
     * class Example {
     * }
     */
    __Class := 'my_cool_class'
    
    ; === Special Method Names ===
    ; There are a handful of reserved method names.  
    ; These methods have specific uses and purposes.  
    ; 
    ; __New()
    ; This method runs when the object is created.
    ; Use this for first-time-run/initialization stuff at object creation.  
    ; Think of this as a constructor.
    ; 
    ; __Delete()
    ; This method runs when the object is released (destroyed).  
    ; It's a destructor and is used to do "cleanup" stuff.  
    ; Not a regularly used method as AHK handles cleanup for most things.
    ; 
    ; Call()
    ; An object with a call method makes the class callable.  
    ; Meaning the object can be called like a function.  
    ; If my_class has a Call method, all instances of my_class can be called.
    ; If it has a static Call method, that's the method that runs when the class is called.  
    ; The class will no longer construct and return objects.
    ; 
    ; __Enum()
    ; An enumerator method.  
    ; This method should always return an enumerator object.  
    ; Enumerator objects provide for-loops with a list of "things" to loop through.
    ; When an object is passed to a for-loop, it looks for 2 things:
    ; Is the object is an enumerator object?
    ; If no, is there an __Enum() method?
    ; If no, error.
    ; Examples:  
    ; Array object enumerators provide the index and value of each array element.
    ; Gui object enumerators provide the handle and control object of each control.  
    ; 
    ; 
    ; __Init()
    ; The initialization method.  
    ; Won't be discussing this because it really shouldn't be messed with.  
    ; But for the sake of education:  
    ; __Init setups up everything for the object and runs before ANYTHING else.  
    ; Including the __New method.  
    ; 99.99% of you will never have a need to mess with this.  
    ; I've written TONS of code and I've never had a scenario where I needed to mess with this.  
    ; __New() is what should be used want stuff should happen at object creation.
    
    /** __New() method
     * @description
     * A method that runs when a new object is created.  
     * When a new instance is created, this method runs automatically.  
     * A static New() method runs the first time the class is referenced.
     * It does not run at script creation.  
     * @param [params] - One or more parameters.  
     * Parameter use is done at the user's discretion.  
     * @returns 
     * @example

MsgBox('This first msgbox runs without the static __New running.')

; Make our first reference to example
; Just including the name causes the static __New method to activate.
; We don't  accessing any properties or methods.
; Just the act of mentioning it counts as a reference to it.
example

; Now let's make a new instance of the example class
instance1 := example()
; And the instance __New()
instance2 := example()

class example {
}













; Examples 

; Let's make a Rect struct using a class.  
; A struct is a chunk of memory thats stores multiple values.  
; And each value is saved to a certain "part" of that chunk of memory.  
; This class lets us turn the concept of a struct into an object in AutoHotkey
; Rect struct information can be found in the MSDN docs:
; https://learn.microsoft.com/en-us/windows/win32/api/windef/ns-windef-rect

; They work kind of like objects in that multiple values can be stored in one thing.
class rect extends Buffer {
    
}

/*
"C" Word Theme:
    "Class Capabilities, Concepts, and Construction"
    "Classes, Concepts, and Crafting Code"
    "Class Creation: Capabilities, Concepts, and Coding"
    "Class Components, Concepts, and Construction"
    "Class Capabilities, Concepts, and Configuration"
    "Class Crafting, Concepts, and Capabilities"
    "Class Code: Capabilities, Concepts, and Clarity"
    "Class Capabilities, Concepts, and Challenges"

Alternative Non-C "Themes":
    "Mastering Classes: Concepts, Creation, and Code"
    "Unpacking Classes: Building Blocks of Object-Oriented Programming"
    "Class Dynamics: A Guide to Objects, Structure, and Syntax"
    "From Concept to Code: Building with Classes"
    "Class Construction: A Deep Dive into Programming Foundations"
    "The Class Blueprint: Concepts, Creation, and Code"
    "Class Crafting: Unlocking the Power of Objects"
    "Building Blocks of Classes: A Comprehensive Guide"
*/




/*
INCLUDE LINKS HERE

VS Code  
AHK v2 add-on
add-on Enhancement Update

Advanced example of class usage
JSONGO 
Peep




    ; Advanced object example of car
    ; How much detail do you need?
    car := {
        top_speed: 155,
        fuel_type: 'Gasoline',
        oil_type: 'Synthetic',
        make: 'Nissan',
        model: 'WRX',
        year: 2025,
        color: 'World Rally Blue',
        engine: {
            engine_type: 'Turbocharged Inline-4',
            horsepower: 271,
            torque: 350,
            fuel_efficiency: 22,
            cylinder_count: 4,
            cooling_system: 'Liquid-Cooled',
            turbocharger: {
                type: 'Twin-scroll',
                boost_pressure: '1.2 bar',
                cooling: {
                    type: 'Intercooler',
                    material: 'Aluminum',
                    size: 'Large'
                }
            }
        },
        transmission: {
            type: 'Manual',
            gears: 6,
            shift_mechanism: 'Hydraulic',
            differential: {
                type: 'Limited-slip',
                ratio: '3.9',
                location: 'Front and Rear'
            }
        },
        wheels: [
            {
                size: 18,
                material: 'Aluminum Alloy',
                type: 'All-Season',
                brake_type: {
                    front: 'Disc',
                    rear: 'Disc',
                    material: 'Carbon-ceramic'
                }
            },
            {
                size: 18,
                material: 'Aluminum Alloy',
                type: 'All-Season',
                brake_type: {
                    front: 'Disc',
                    rear: 'Disc',
                    material: 'Carbon-ceramic'
                }
            },
            {
                size: 18,
                material: 'Aluminum Alloy',
                type: 'All-Season',
                brake_type: {
                    front: 'Disc',
                    rear: 'Disc',
                    material: 'Carbon-ceramic'
                }
            },
            {
                size: 18,
                material: 'Aluminum Alloy',
                type: 'All-Season',
                brake_type: {
                    front: 'Disc',
                    rear: 'Disc',
                    material: 'Carbon-ceramic'
                }
            }
        ],
        interior: {
            seats: {
                seat_material: 'Alcantara',
                seat_adjustment: 'Electric',
                number_of_seats: 5,
                seat_heating: {
                    front: 'Yes',
                    rear: 'No'
                },
                seat_cooling: {
                    front: 'No',
                    rear: 'No'
                }
            },
            dashboard: {
                screen_size: 8,
                infotainment_system: 'Apple CarPlay, Android Auto',
                climate_control: 'Dual Zone',
                steering_wheel: {
                    material: 'Leather',
                    adjustable: 'Yes',
                    heated: 'Yes'
                }
            }
        },
        safety_features: [
            'ABS',
            'Airbags (Front, Side, Curtain)',
            'Lane Assist',
            'Backup Camera',
            'Adaptive Cruise Control',
            'Blind Spot Detection',
            'Rear Cross-Traffic Alert'
        ],
        dimensions: {
            length: 4.6,
            width: 1.8,
            height: 1.4,
            wheelbase: 2.7,
            weight: 1500,
            ground_clearance: 0.14
        },
        tires: [
            {
                tire_brand: 'Michelin',
                tire_type: 'All-Season',
                tire_pressure: 34,
                size: '225/45R18'
            },
            {
                tire_brand: 'Michelin',
                tire_type: 'All-Season',
                tire_pressure: 34,
                size: '225/45R18'
            },
            {
                tire_brand: 'Michelin',
                tire_type: 'All-Season',
                tire_pressure: 34,
                size: '225/45R18'
            },
            {
                tire_brand: 'Michelin',
                tire_type: 'All-Season',
                tire_pressure: 34,
                size: '225/45R18'
            }
        ],
        performance: {
            0_60_time: 5.4,
            quarter_mile_time: 13.5,
            braking_distance: {
                60_to_0: 35,
                meters: 35
            },
            handling: {
                g_force: 0.92,
                suspension: {
                    front: 'MacPherson Strut',
                    rear: 'Multi-Link'
                }
            }
        },
        lighting: {
            headlights: {
                type: 'LED',
                adaptive: 'Yes',
                auto_leveling: 'Yes'
            },
            taillights: {
                type: 'LED',
                dynamic_turn_signal: 'Yes'
            },
            fog_lights: {
                type: 'Halogen',
                activated: 'Automatic'
            }
        }
    }
    
## Classes in other languages
I think it's worth adding that in some other languages, you don't directly access properties. 
Instead, you would use "setters" and "getters" which are methods designed to set and get property values.  
AHK does not require the use of getters and setters, though they DO provide them in the form of dynamic properties.  
This gives the coder the option to use them.  
It's up to the coder to deicde how to implement things and how to design their code.  
Just make sure you document it so others know how to use it correctly.  

Another thing other languages do is require that you declare class items as "private" and "public".  
AHK does not have a concept of privatizing code so this does not exist.  
All code in AHK is considered public code.  



## Class Cheat Sheet  

And now for the giant example class:

    ; Description: Define a class.  
    ; A class name is required. We'll name ours "my_new_class".  
    ; All classes must extend from another class.  
    ; This determines what methods and properties your class inherits.  
    ; If no extension is provided, "Extends Object" is used by default.  
    ; This makes sense as most things in AHK are objects.  
    Class my_new_class extends some_other_class {
        
        ; === METHODS AND PROPERTIES ===
        
        ; PROPERTY
        ; Description: Properties tend to store data like numbers, strings, and objects.  
        ; These act as variables for objects.  
        ; Static properties belong to the class.  
        ; Non-static properties belong to the Prototype and are what each instance object receives.  
        static class_property := 'This property belongs to my_new_class'
        instance_property := 'This is a property all instances of my_new_class will get.'
        
        ; METHOD
        ; Description: Methods are used to run code. To "do stuff".  
        ; Static methods belong to the class.  
        ; Non-static methods belong to the Prototype and are what each instance object receives.  
        ; Methods work identically to functions.  
        static class_method(params*) {
            ; This method is called using: 
            ; my_new_class.class_method()
            MsgBox(A_ThisFunc)
        }
        
        instance_method(params*) {
            ; This method is called using: 
            ; instance := my_new_class()
            ; instance.instance_method()
            MsgBox(A_ThisFunc)
        }
        
        ; DYNAMIC PROPERTIES
        ; Description: These are properties that work like setter/getter functions.  
        ; A setter is code that runs when you assign (set) a property value.  
        ; A getter is code that runs when you access (get) a property value.  
        ; Only include square brackets if parameters are expected.  
        ; Static dynamic properties belong the class.  
        ; Non-static dynamic properties belong to the Prototype and are what each instance object receives.  
        dynamic_prop[parameters] {
            ; Get runs when the dynamic_prop is accessed.
            get {
                MsgBox('You tried to get dynamic_prop from an instance of my_new_class.')
            }
            
            ; Set runs when a value is assigned to the dynamic property.  
            ; A hidden "Value" parameter is provided containing the assigned data.  
            set {
                MsgBox('You set the value of dynamic_prop to: ' value)
            }
        }
        
        
        ; === SPECIAL PROPERTIES ===
        ; These are properties that all classes and instance objects have.
        
        ; __Class
        ; Description: A string containing the name of the class of origin.  
        ; All classes are based on the Class object. Or it wouldn't be a class.  
        ; Instance objects return the class they originated from.  
        __Class => 'my_new_class'
        static __Class => 'Class'
        
        ; Base
        ; Description: A reference to the origin of the current object.  
        ; It is the object upon which the current object is "based" upon.  
        ; This is an object reference, not a string.  
        ; Static base belongs to the class and is always a reference to the object it extends from.  
        ; Non-statc Base belongs to the instance objects and will always be a refrence to the Prototype that made them.  
        Base => my_new_class.Prototype
        static Base => Object
        
        ; __Item
        ; Description: A special dynamic property.  
        ; Including this in the class allows the class/instance to use item syntax. 
        ; obj[some_value]
        ; The __Item property is what Array and Map objects use.  
        ; Item syntax is also called array syntax.  
        ; Static __Item: The class can use item syntax.
        ; __Item: The instance objects can use item syntax.
        __Item[param] {
            get {
                MsgBox('Tried to get a property')
            }
            set {
                something := Value
            }
        }
        
        
        ; === SPECIAL METHODS ===
        ; These all have special meaning when used in a class:  
        ; __New(), __Delete(), __Enum(), __Item[], Call()
        
        ; __New()
        ; Description: Runs when the object is created. Initializes stuff.  
        ; my_new_class() is the same as calling my_new_class.__New()
        ; Static __New(): Runs the first time the class is referenced.  
        ; __New(): Runs when an instance object is created.  
        ; Instance __New is  also known as a "constructor" because it constructs an object.  
        __New(params*) {
            MsgBox('Intialize stuff.')
        }
        
        ; __Delete()
        ; Description: Runs when an object is destroyed/released.  
        ; Static __Delete(): Will never work because classes are read-only. Can't be destroyed.  
        ; __Delete(): Runs when an instance object is destroyed/released.  
        ; Instance __Delete is  also known as a "destructor" because it runs when the object is destroyed.
        __Delete(params*) {
            MsgBox('Clean up stuff.')
        }
        
        ; __Enum()
        ; Description: Used by for-loops. Provides a list of "things" to loop through.  
        ; This method is expected to return an enumerator-like object.  
        ; Static __Enum(): The class can be passed to a for-loop.  
        ; __Enum(): The instance object can be passed to a for-loop
        __Enum(params*) {
            return Enumerator
        }
        
        ; Call()
        ; Description: Makes an object callable.  
        ; Static Call(): The class can be called/run code. Also prevents the class from creating instance objects.  
        ; Call(): The instance objects can be called/run code.  
        Call(params*) {
            MsgBox('Do this stuff when called')
        }
        
        ; Description: The initialization method.  
        ; Only including for completeness and to educate.  
        ; This initializes and sets up stuff for the object.  
        ; Unless you know exactly what you're doing, don't mess with this method.  
        ; There is a 99.9% chance what you want to do should be done with the __New() method.
        __Init() {
            MsgBox("Seriously, you don't need to create __Init methods.")
        }
        
        ; === META-FUNCTIONS ===
        ; Meta-functions are used to handle "undefined" methods and properties.  
        ; These special functions can be used to run code instead of throwing an error.  
        
        ; __Call()
        ; Description: Called when an undefined method is called.  
        ; This applies to both static and instance versions.  
        __Call(method_name, param_arr) {
            MsgBox('This object does not have a ' method_name ' method.')
        }
        
        ; __Get()
        ; Description: Called when an undefined property is accessed (gotten).
        ; This applies to both static and instance versions.
        __Get(prop_name, param_arr) {
            MsgBox('This object does not have a ' prop_name ' property.')
        }
        
        ; __Set()
        ; Description: Called when an undefined property has a value set to it.
        ; This applies to both static and instance versions.
        __Set(prop_name, param_arr, value) {
            MsgBox('The value of ' value ' could not be set to ' prop_name '.')
        }
        
        ; === Nested Class ===
        ; Classes can be defined inside of classes.  
        ; Remember, it's just another type of object.  
        ; A nested class belongs to the class it's defined in and doesn't use the "static" keyword.
        ; Also, nesting a class inside another has nothing to do with inheritance or extends.  
        ; This nested class extends Array even though it is located inside the class my_new_class.
        class nested_class extends Array{
            static prop := 'belongs to: my_new_class.nested_class'
            prop := 'instance of: my_new_class.nested_class'
        }
    }

#Useful links


If you want to better understand AHK's class structure, check out my guide:  
[GroggyGuide: Everything in v2 is an object, descriptors described, the secret Any class, methods are just callable properties, and more.](https://www.reddit.com/r/AutoHotkey/comments/1hvwd64/groggyguide_everything_in_v2_is_an_object/).

vscode
add-on
add-on enhancement

#Examples
hotkey toggle class
autoclicker class  
make a struct from a buffer

# Provide all the types of polymorphic examples in the class section?
method overloading with different parameter types
method overloading with different parameter amounts  
method overriding





## Bonus: You are learning more than AHK

<update> There is SO MUCH stuff we've covered in this guide that is not unique to AHK.  
From the concepts of OOP to how arrays work, operator precedence to scope to how funcitons work...this is all stuff that applies to many programming languages.  
You're not just learning AHK. You're learning programming.  

EVERY language deals with variables, if-statements, and loops.  
They're core parts of programming.

By learning AutoHotkey v2, you're setting yourself up to learn other stuff.  
AutoHotkey IS a programming language by all definitions.  
And a lot of AHK is based on other languages, especially JavaScript and C#.  

Meaning as you continue to learn AHK v2 and learn more about object-oriented programming, you're actually learning about programming in general.  
What you learn here applies to other languages. 
The concept of objects, OOP (in general), properties and methods, setters and getters, class structuring, and more are commong concepts found in many other languages.  

If you understand AHK objects are made like this `{name:value, name:value, ...}`, then you're already on your way to understanding JavaScript objects.  

If you include AHK's array syntax `[value1, value2, value3]` and couple that with objects, you understand like 90% of JSON data structures. Without every studying the topic.  

One day you might decide you want to do something web related and that JavaScript is way better at that.  
You decide to take the dive into JavaScript.  
I guarantee that your learning curve will be substantially lower compared to what it would be without your AHK background.  
Understanding basic concepts, object structure, methods and properties, object-oriented programming, class structure, and all that will give you a hell of a leg up on learning.  
Couple that with the fact that a lot of AHK's structure and syntax is based on JS, and you'll be writing code in a fraction of the time it would take someone else to learn the language.  

Keep that in mind as you continue learning.  
You're developing skills that apply beyond AHK. And even beyond programming.  


# Examples 

## Class timer vs instance timers
Good example would be making a timer with a gui.  
Show a class timer vs instance timers. Plural.

## Rock, paper, scissors using a table.  



# Donations
"Human knowledge belongs to the world. Like Shakespeare or aspirin."  
Teddy Chin said that in Antitrust.  
It wasn't the *best* movie ever made, but it was a **good** movie.  
And that quote has always stuck with me because I believe it.  

My guides have always been free.  
My help has always been free.  
My video series will be free.  

However, there are bills to pay.  
I've decided to open a Ko-fi account.  
This is a place for people to make donations toward future content.  
If you can afford to and you *want* to, it's welcome.  
If you can't afford to or just plain don't want to, the content is still free an I want you read it and learn from it.  

The only way money comes into this is if someone can afford it and wants to help the cause.  
I've done donations in the past to people because I believed in what they were doing and wanted to see more of it.  
I'm hoping the same happens.  
If I can get enough people dontating or subscribing, I'll be making content more regularly.  

I have ***tons*** of different ideas relating to AHK v2.  
I want to make more educational stuff, maybe even getting lower level than AHK.  
I already have things like a binary series and a Gui series in the works.  
And a text file full of ideas ranging from YouTube videos to Reddit posts to interactive encounters to helping out random people on random subs.  

The more support and traction I'm able to get, the more content I intend to create and release.  

More guides.  
More videos.  
More examples.  
More assignments.  
More content.  

Regardless of how things turn out, I'm sure I'll still be posting guides and scripts when I can.  

Thanks for taking time to read the post and especially for reading to the end.  
Most importantly, thanks for being part of the AutoHotkey community.  

# Cheat sheets

## Operator Precedence List

All operators have a precedence level.  
This list includes each operator, a brief usage example, description, and a precedence number.  
The higher the number, the higher the precedence.  
Meaning dereferencing is always the first operator evaluated and the multi-statement operator is always the last.

As covered in the expression section, sub-expressions must be fully evaluated, left-to-right, before an expression can be evaluated.  

Precedence  | Usage         | Description
:---        | :---          | :---
Max         | `(expr)`      | SubExp: Evaluate inside the parentheses
Max         | `fn(param*)`  | SubExp: Evaluate function call and return value
Max         | `obj[item]`   | SubExp: Access an objects item
Max         | `{key:value}` | SubExp: Create and evaluate the object literal
24          | `%x%`         | Dereferencing
23          | `x.y`         | Memeber access
22          | `x?`          | Maybe
21          | `x++`         | Post-increment
21          | `++x`         | Pre-increment
21          | `x--`         | Post-decrement
21          | `--x`         | Pre-decrement
20          | `x ** y`      | Exponent
19          | `-x`          | Unary minus
19          | `+x`          | Unary plus
19          | `!x`          | Logical NOT
19          | `~x`          | Bit-wise NOT
19          | `&x`          | Reference
18          | `x * y`       | Multiply/variadic
18          | `x / y`       | Divide/true divide
18          | `x // y`      | Integer divide
17          | `x + y`       | Add
17          | `x - y`       | Subtract
16          | `x << y`      | Bit shift left
16          | `x >> y`      | Arithmetic bit shift right
16          | `x >>> y`     | Logical bit shift right
15          | `x & y`       | Bit-wise AND
14          | `x ^ y`       | Bit-wise XOR
13          | `x \| y`      | Bit-wise OR
12          | `x . y`       | Concatenate
11          | `x ~= Rgx`    | RegEx match
10          | `x > y`       | Greater than
10          | `x < y`       | Less than
10          | `x >= y`      | Greater than or equal to
10          | `x <= y`      | Less than or equal to
9           | `x = y`       | Equal
9           | `x == y`      | Case-sensitive equal
9           | `x != y`      | Not equal
9           | `x !== y`     | Case-sensitive not equal
8           | `x IS y`      | Is of type
8           | `IN`          | Reserved
8           | `CONTAINS`    | Reserved
7           | `x NOT y`     | Logical NOT
6           | `x AND y`     | Logical AND
6           | `x && y`      | Logical AND
6           | `x OR y`      | Logical OR
6           | `x \|\| y`    | Logical OR
5           | `x ?? y`      | Or-Maybe/Coalescing
4           | `x ? y : z`   | Ternary/conditional/if-else shorthand
3           | `x := y`      | Assignment
3           | `x += y`      | Add and assign
3           | `x -= y`      | Subtract and assign
3           | `x *= y`      | Multiply and assign
3           | `x /= y`      | Divide and assign
3           | `x //= y`     | Integer divide and assign
3           | `x .= y`      | Concatenate and assign (append)
3           | `x \|= y`     | OR and assign
3           | `x &= y`      | AND and assign
3           | `x ^= y`      | NOT and assign
3           | `x >>= y`     | Bit shift left and assign
3           | `x <<= y`     | Arithmetic bit shift right and assign
3           | `x >>>= y`    | Logical bit shift right and assign
2           | `x (*) => y`  | Fat arrow
1           | `x, y`        | Multi-statement


