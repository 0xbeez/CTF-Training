# Introduction to scripting with python:  
A guide to help you get up and running with scripting. Python will be used here as it is broadly adapted among the InfoSec community all over the world.  
## Versioning:  
There exist two flavors of Python, 2.X and 3.X. And since [2.X is nearly retired](https://pythonclock.org/), we will only cover Python3. Don't worry, there are no huge gaps in the syntax and you can go on from here and read some of the existent code in py2. This diff in versions is only necessary to understand why sometimes code may seem right, but not working.  
  
## PEPs and The Zen of Python:  
Index of Python Enhancement Proposals, also known as PEPs is a reference to all python officially related topics such as deprecation of Standard Modules, Guidelines for Language Evolution and bug fixes ... all described in the 0'th PEP [here](https://www.python.org/dev/peps/).  

**The Zen of Python** : Python is more than a programming/scripting language. It has its own set of rules and philosophy. That can be found in [the 20'th pep](https://www.python.org/dev/peps/pep-0020/) or by importing this in the REPL.  
```python
import this
```  
This brings us to the operational modes of Python.  
## **REPL Vs. interpreted code**:  
There exist two operational modes of python; the first one is using the REPL(Read Evaluate Print Loop) and the second is running code using the interpreter.  
* REPL: 
```bash
python # or python3 if the returned version when typing python --version is 2.X
```  
* Interpreter:  
This is how you will be mostly using python, besides when testing just a simple idea. This can be leveraged by writing code in a X.py file then running 
```bash
python X.py 
```  
The interpreter will interpret the code line by line and prompt us with output if it has any side effects related to STDOUT.  


## What is Python?  
In the Homepage: Python is a programming language that lets you work quickly
and integrate systems more effectively.  
It is dynamically typed, meaning that specifying the type of objects is not necessary. It is also used for heavy scripting besides the plethora of other fields since its huge community is always shipping more useful packages(we will talk about packaging and modules later on the course).  
  
## What is Python good for?
*Python is a general-purpose language, which means it can be used to build just about anything, which will be made easy with the right tools/libraries. Professionally, Python is great for backend web development, data analysis, artificial intelligence, and scientific computing.*  
  
## Installation (live)  
## Environment setup: SETTING UP VSCODE  

Now we should be all set up, and we can start with our first codes.

