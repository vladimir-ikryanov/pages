# Java Style Guide

The intention of this guide is to provide a set of conventions that encourage good code. It is the distillation of many combined man-years of software engineering and Java development experience. While some suggestions are more strict than others, you should always practice good judgement.

Much of our style and conventions mirror the [Google's Java Style Guide](https://google.github.io/styleguide/javaguide.html) and [Twitter's Java Style Guide](https://github.com/twitter/commons/blob/master/src/java/com/twitter/common/styleguide.md).

### Table of Contents

1. [Introduction](#1-introduction)  
1.1. [Terminology notes](#11-terminology-notes)  
1.2. [Guide notes](#12-guide-notes)  

2. [Source file basics](#2-source-file-basics)  
2.1. [File name](#21-file-name)  
2.2. [File encoding: UTF-8](#22-file-encoding-utf-8)  
2.3. [Special characters](#23-special-characters)  

3. [Source file structure](#3-source-file-structure)  
3.1. [License or copyright information, if present](#31-license-or-copyright-information-if-present)  
3.2. [Package statement](#32-package-statement)  
3.3. [Import statements](#33-import-statements)  
3.4. [Class declaration](#34-class-declaration)  

4. [Formatting](#4-formatting)  
4.1. [Braces](#41-braces)  
4.2. [Block indentation: +4 spaces](#42-block-indentation-4-spaces)  
4.3. [One statement per line](#43-one-statement-per-line)  
4.4. [Column limit: 100](#44-column-limit-100)  
4.5. [Line-wrapping](#45-line-wrapping)  
4.6. [Whitespace](#46-whitespace)  
4.7. [Grouping parentheses: recommended](#47-grouping-parentheses-recommended)  
4.8. [Specific constructs](#48-specific-constructs)  
4.9. [Chained method calls](#49-chained-method-calls)  

5. [Naming](#5-naming)  
5.1. [Rules common to all identifiers](#51-rules-common-to-all-identifiers)  
5.2. [Rules by identifier type](#52-rules-by-identifier-type)  
5.3. [Camel case: defined](#53-camel-case-defined)  

6. [Programming Practices](#6-programming-practices)  
6.1. [@Override: always used](#61-override-always-used)  
6.2. [Caught exceptions: not ignored](#62-caught-exceptions-not-ignored)  
6.3. [Static members: qualified using class](#63-static-members-qualified-using-class)  
6.4. [Finalizers: not used](#64-finalizers-not-used)  
6.5. [Let your callers construct support objects](#65-let-your-callers-construct-support-objects)  
6.6. [Testing antipatterns](#66-testing-antipatterns)  
6.7. [Defensive programming](#67-defensive-programming)  
6.8. [Remove dead code](#68-remove-dead-code)  
6.9. [Use general types](#69-use-general-types)  
6.10. [Use final fields](#610-use-final-fields)  
6.11. [When interrupted, reset thread interrupted state](#611-when-interrupted-reset-thread-interrupted-state)  
6.12. [Avoid unnecessary code](#612-avoid-unnecessary-code)  

7. [Javadoc](#7-javadoc)  
7.1. [Formatting](#71-formatting)  
7.2. [The summary fragment](#72-the-summary-fragment)  
7.3. [Where Javadoc is used](#73-where-javadoc-is-used)  
7.4. [No author tags](#74-no-author-tags)  

## 1. Introduction

This document serves as the complete definition of JxBrowser's coding standards for source code in the Java™ Programming Language. A Java source file is described as being in Java Code Style if and only if it adheres to the rules herein.

Like other programming style guides, the issues covered span not only aesthetic issues of formatting, but other types of conventions or coding standards as well. However, this document focuses primarily on the hard-and-fast rules that we follow universally, and avoids giving advice that isn't clearly enforceable (whether by human or tool).

### 1.1. Terminology notes

In this document, unless otherwise clarified:

1. The term _class_ is used inclusively to mean an "ordinary" class, enum class, interface or annotation type (`@interface`).
2. The term _member_ (of a class) is used inclusively to mean a nested class, field, method, or constructor; that is, all top-level contents of a class except initializers and comments.
3. The term _comment_ always refers to implementation comments. We do not use the phrase "documentation comments", instead using the common term "Javadoc."

Other "terminology notes" will appear occasionally throughout the document.

### 1.2. Guide notes

Example code in this document is non-normative. That is, while the examples are in Java Code Style, they may not illustrate the only stylish way to represent the code. Optional formatting choices made in examples should not be enforced as rules.

## 2. Source file basics

### 2.1. File name

The source file name consists of the case-sensitive name of the top-level class it contains (of which there is exactly one), plus the `.java` extension.

### 2.2. File encoding: UTF-8

Source files are encoded in **UTF-8**.

### 2.3. Special characters

#### 2.3.1. Whitespace characters

Aside from the line terminator sequence, the **ASCII horizontal space character (0x20)** is the only whitespace character that appears anywhere in a source file. This implies that:

1. All other whitespace characters in string and character literals are escaped.
2. Tab characters are **not** used for indentation.

#### 2.3.2. Special escape sequences

For any character that has a [special escape sequence](http://docs.oracle.com/javase/tutorial/java/data/characters.html) (`\b`, `\t`, `\n`, `\f`, `\r`, `\"`, `\'` and `\\`), that sequence is used rather than the corresponding octal (e.g. `\012`) or Unicode (e.g. `\u000a`) escape.

#### 2.3.3. Non-ASCII characters

For the remaining non-ASCII characters, either the actual Unicode character (e.g. `∞`) or the equivalent Unicode escape (e.g. `\u221e`) is used. The choice depends only on which makes the code **easier to read and understand**, although Unicode escapes outside string literals and comments are strongly discouraged.

> **Tip**: In the Unicode escape case, and occasionally even when actual Unicode characters are used, an explanatory comment can be very helpful.

**Examples:**
```
// Best: perfectly clear even without a comment.
String unitAbbrev = "μs";

// Allowed, but there's no reason to do this.
String unitAbbrev = "\u03bcs"; // "μs"

// Allowed, but awkward and prone to mistakes.
String unitAbbrev = "\u03bcs"; // Greek letter mu, "s"

// Poor: the reader has no idea what this is.
String unitAbbrev = "\u03bcs";

// Good: use escapes for non-printable characters, and comment if necessary.
return '\ufeff' + content; // byte order mark
```
