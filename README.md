**How to Edit, Run and debug C# programs in Visual Studio Code on the Raspberry Pi**

Now that we have an official Visual Studio Code on the Raspberry Pi I wanted to program in C#.
However, I found that Visual Studio Code doesn't come with 'out of the box' configurations for C# so, as you do, I had to spend a while working out how to do it!

Here is a step-by-step process to install, configure, run and debug a C# program on the Raspberry Pi:

**1. Install VS Code**

From the browser, navigate to https://code/visualstudio.com/Download
and install '.deb' 'ARM' (for 32 bit) or 'ARM 64' (if you know you have a 64 bit OS)

**2. Install Mono**

Opena terminal window and enter:
~~~
sudo apt-get install mono-complete
~~~

**3. Install 'Mono Debug' extension in VS Code**

a. Open Visual Studio Code from the Main menu -> Programming dropdown ..
b. Select the 'Extensions' button on the left panel (4 squares button)
c. Enter 'mono debug' in the search bar
d. Install 'mono debug' (by Microsoft)

**4. Create a C# program to run**

a. Create a new file (CTRL+N keys)

b. Enter the following C# program as a test ..
~~~
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
~~~
... and save as '**HelloWorld.cs**' in a 'HelloWorld' folder

**5. Add the launch.json and task.json scripts**

a. When about to run/debug, select 'Create launch.json script', modify it (as below) and save the script

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

b. Create another script in the same '.vscode' folder and save as 'tasks.json' ..

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

**6. Run the program and/or add debug breakpoints to debug your program**

