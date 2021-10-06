# OSCP-Buffer-Overflow-Cheatsheet

## Immunity Debugger & Mona 

Install Immunity Debugger this will be needed to perform the bugger overflow exploitation.
can be found on: `https://www.immunityinc.com/`

After installing Immunity debugger install Mona from: `https://github.com/corelan/mona`.
Put the .py file in the PyCommands folder (C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands. 
This module will be needed to determine the offset/ find the EIP.

## Fuzzing

After running the program on your Windows machine and have it attached to Immunity Debugger.
Run the fuzzer.py script to identify the point where the application will crash.

## Finding the Offset

To find the we will need to use the ruby script from metasploit. `/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l {bytes}`



## Badchars

## JMP ESP

## Exploitation
