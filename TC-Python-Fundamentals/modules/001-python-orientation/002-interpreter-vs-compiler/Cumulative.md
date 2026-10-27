# Cumulative

<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Explain from a high-level perspective how a compiler works
- Explain from a high-level perspective how an interpreter works
- Explain the benefits and drawbacks that come with a compiled language
- Explain the benefits and drawbacks that come with an interpreted language
</details>

<details><summary>Description</summary>
<br>

# What is a Compiler

- A compiler is software that takes the entirety of your source code and converts it into a form that can be executed by your operating system, usually called a "binary" or "executable."
- Passing the entirety of your source code through the compiler has multiple benefits.
- Your entire program is pre-converted into whatever format your system needs to execute.
- Optimizations can be applied during the compilation process.
- The compiler can detect issues with your code before you try to run it.
- There are some drawbacks to compiled languages.
- Your application has to be compiled for each system you want your app to work on.
- If you want your app to work on both Windows and Mac computers, you will need two versions of your application: one for Windows and one for Mac.
- Debugging can be more difficult since errors can happen anywhere between the start of the compilation process and the end of the execution of your application.

Some compiled languages are:

- C++
- Java
- Go

# What is an Interpreter

- An interpreter is similar to a compiler in that it converts source code into machine code, but it does so line by line instead of all at once.
- Using an interpreter brings multiple advantages.
- Interpreters are specific to their operating system, so as long as you have access to the software, you can run your applications. This makes applications created via interpreted languages much more portable than applications created in compiled languages.
- Interpreted languages are typically easier to debug due to the interpreter going line by line in the compilation/execution process. It is easier to track where things are happening.
- Interpreters have some drawbacks regarding their flexibility.
- Interpreted languages tend to be less optimized than their compiled counterparts and are typically not used when high levels of application performance are necessary.
- Since compilation and execution happen at the same time, you are required to have an interpreter anywhere you want to run your application.

Some interpreted languages are:

- Python
- JavaScript
- Ruby

</details>
<details><summary>Real World Application</summary>
<br>

Some companies that use compiled languages for their services:
- **Google**: Many of Google's services are written with Go.
- **Microsoft**: Many of Windows' core components are written in C++ (compiled), and C# is used across .NET applications, compiled to Intermediate Language and then JIT-compiled at runtime.
- **AWS**: Rust is being integrated into some of AWS's cloud offerings.

Some companies that use interpreted languages for their services:
- **Instagram**: Instagram's backend is primarily built in Python, enabling fast development.
- **YouTube**: While YouTube's core systems are written in C++, Python is used extensively for internal tools and APIs.
- **Reddit**: Reddit's backend is built with Python, especially using frameworks like Pylons and now moving toward newer Python stacks.

</details>
<details><summary>Implementation</summary>
<br>

- Most interpreted and compiled languages are interchangeable when it comes to creating functionality, but they differ in their built-in efficiency for different tasks. For instance, if all you need is a simple script or snippet of code that will be slightly adjusted every now and then, an interpreted language is probably going to be more efficient in the long run than a compiled language. The interpreter is going to compile and execute the code line by line, allowing for ease of deployment. You could use a compiled language to perform the same action, but that would require compiling the code, creating your executable, and then executing it, which could become very tedious if there are minor changes that need to be made occasionally.

- On the flip side, if you are building a monolithic enterprise application for your company's flagship product, a compiled language's built-in quality gates are crucial for catching bugs and errors that could turn consumers away from your product. With an interpreted language, it can be very easy to miss errors in lightly used areas of your system since the interpreter won't load them for compilation and execution until they are used. With a compiled language, you are able to catch those mistakes right away.

- Ultimately, while both interpreted and compiled languages are incredibly flexible in how they work, they are inherently suitable for different kinds of tasks if you need to optimize your systems. Use interpreted languages when you need flexibility and ease of deployment, and use compiled languages when you need reliability and process optimization.

</details>
<details><summary>Summary</summary>
<br>

- "Compiler vs Interpreter" describes two different approaches to how programming languages go from source code to executable code.
- Compiled languages tend to be better when execution speed is essential, but they can be a pain to deploy in multiple environments because they require separate "binaries" for each one.
- Interpreted languages tend to be more flexible in their deployment options, but due to compilation happening line by line at runtime, their execution tends to be slower than compiled language applications.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
