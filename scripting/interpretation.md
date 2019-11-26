# Interpretation & compilation process
![compilation and interpretation model](https://ruslanspivak.com/lsbasi-part1/lsbasi_part1_compiler_interpreter.png)
  
This document is a reference for major differences between compiled and interpreted languages.

## Compilation:
Actually compiled languages go through a build process rather than a compilation process. Actually, it represents nothing but a step of many.  
First, we start with a set of text files containing code that we want to spit the executable from the project.  
The build process consists of several steps:  
![Build process](https://he-s3.s3.amazonaws.com/media/uploads/8b8ef84.jpg)  
  
## Interpretation:  
The build process of interpreted language is often more complex than that of compiled ones. Actually, a lot of their features turn into a nightmare especially that dynamic tying for example means that the interpreter has to figure out types itself. Usually, interpreted languages have more or less the same process of running, with the gain of portability and syntax friendliness over performance. Thus, they are not recommended when dealing with complex tasks which require efficiency and heavy computation unless optimisation measures are taken.  
![Interpretation process](https://i.imgur.com/PJME67T.png)
