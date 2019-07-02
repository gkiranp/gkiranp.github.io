---
layout: post
excerpt_separator: <!--more-->
title: "Why does C++ Compilation takes a long"
date: 2017-05-23
tags: C++ compilation
---

C++ is one of the strong programming language. But people complain saying it takes long time to compile even a small piece of code compare to other competitors like C# or Java. The answer is Yes.<!--more--> 
Straight away we can think of one basic reason for this is the `pre-processor directives`, which gives instructions to compiler to pre-process the information before the actual compilation starts, and I should not miss, `#include` is also one among that pre-processor directives. But in reality, this is not only the reason. I was going through the whole compilation process and did surfing through Google and found below points,

**1. Load and Compile Header: 
In C++ every single unit of compilation needs, may be hundreds of headers to be Loaded and Compiled each time. Everyone of them typically has to be re-compiled for every single compilation unit. This is because, compiler thinks the result of compiling header may vary for every other unit, such like, a macro defined in one of the compilation unit may cause change in contents of header included for another compilation unit. So, the process has to be re-carried out for each and every single unit. This, probably could be main reason for C++ compiler to consume more time on compilation.
On the other hand, languages like Java or C# if you compare, they don't have to include headers, they can depend on binaries from the compilation of the used classes. This means, if object X is used in abc.java file, to get it compiled, it is enough for compiler to check binaries of X.class, it doesn't require to go deeper check looking for dependencies of X.class.

**2. - Templates: 
In C# like languages, `List<T>` is the only type that is compiled, irrespective of type 'T' and irrespective of how many instantiation of List you have in program. On the other hand, C++ compiler behaves differently. For C++, `vector<int>` and `vector<float>` are entirely different entities to handle and each one needs to be re-compiled on each time.
Add to this, templates makes a full Turing-Complete "sub-language" that the compiler has to interpret with, and this can become ridiculously complicated. Even relatively simple template meta programming code can define recursive templates that create dozens and dozens of templates of instantiations. However, it is likely that templates may result in extremely complex types, with ridiculously long names, adding a lot of extra work to the linker. (It has to compare a lot of symbol names, and if these names can grow into many thousand characters, that can become fairly expensive).

**3. - Linking: 
Once all units are compiled, all the object files need to be linked together. This is the process of monolithic linking and cannot be parallelized. So compiler has to process whole project.

**4. - Optimization: 
C++ really allows very peculiar way of optimization. This whole optimazation process is a compiler dependent and may vary with different techniques. If you compare other programming languages like C# or Java, they don't allow complete optimization to happen on program, they don't allow complete elimination of class to happen, because of their feature 'reflection' [Reflection is used to describe a code which is able to inspect another piece of code]. But, even a simple C++ template metaprogram can easily generate dozens or hundreds of classes, all of which are inlined and eliminated again in the optimization phase. And again, for C++, it doesn't get second chance and compiler has to do optimization on compilation time only, compared with C# program which can rely on the JIT compiler to perform additional optimizations at load-time.

**5. - Parsing: 
The C++ syntax is extremely complicated to parse, as it depends heavily on context, and is very hard to disambiguate. This takes a lot of time in compilation.

However, most of the above factors are shared by C program also, which compiles fairly and efficiently. Only offender I can see is `Templates` in C++. Templates are useful, and make C++ a far more powerful language, but they also take their toll in terms of compilation speed.