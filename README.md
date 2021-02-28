**How to run and debug C# programs in Visual Studio Code on the Raspberry Pi**

Now that we have an official Visual Studio Code on the Raspberry Pi I wanted to program in C#.
However, I found that Visual Studio Code doesn't come with 'out of the box' configurations for C# so, as you do, I had to spend several hours on the web finding out how to do it!

Here is a step-by-step process to install, configure, run and debug a C# program:

**1. Install VS Code**


**2. Install Mono**

~~~
sudo apt-get install mono-complete
~~~

**3. Create a C# program to run**

a. Open a terminal (shell) window
b. Create a project folder such as 'HelloWorld' with ..
~~~
mkdir HelloWorld
~~~
c. Enter the folder with ..
~~~
cd HelloWorld
~~~
d. Open Visual Studio Code from the terminal with ..
~~~
code .
~~~
e. Create a new file by selecting the 'New File' icon (on the 'HELLOWORLD' tab)

f. Now enter the following C# program as a test ..
~~~
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World on my Raspberry Pi!");
        }
    }
}
~~~
... and save it as '**HelloWorld.cs**' in a folder such as 'HelloWorld'

**4. Add .vscode folder with launch and task JSON scripts**

a. In your 'HelloWorld' folder create another folder '.vscode' next to your 'HelloWorld.cs' file
b. Inside the '.vscode' folder ad the following two scripts;

launch.json
~~~
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "2.0.0",
    "configurations": [

        {
            "name": "Mono Debug (console)",
            "type": "mono",
            "request": "launch",
            "preLaunchTask": "build",
            "program": "${workspaceFolder}/HelloWorld.exe",
            "args": [],
            "cwd": "${workspaceFolder}",
            "console": "internalConsole"
        }
    ]
}
~~~

tasks.json
~~~
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "command": "mcs",
            "type": "shell",
            "args": [
                "-debug",
                "${workspaceFolder}/HelloWorld.cs"
            ],
            "group": "build"
        }
    ]
}
~~~

5. 
