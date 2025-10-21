Refers to an exploit module.
	- Singles: Self-contained 
	- Stagers: Setup a network connectin between the attacker and the victim. Are designed to be small and reliable. 
	- Stages: Are download by Stagers modules

Wheter a payload is staged is represented by '/' in the payload name.

## types

- Inline: contain the exploit and full shell code for the selected task. More stable than their counterparts.
- Stager: establishes a channel between the attack and victim, then execute a stage payload.
- Meterpeter (meta interpreter): operates via dll (dynamic link library) injection; resides in the memory of the remote host and leaves no traces on the hard drive; scripts and plugins can be loaded and unloaded dynamically.
- PassiveX: can help in circumventing restrictive outbound firewalls.
- NoNx: The NX (No eXecute) bit is a feature built into some CPUs to prevent code from executing in certain areas of memory. This payloads is designed to circumvent that.
- Ord: Ordinal payloads.
- IPv6: to function over those networks.
- Reflective DLL injection: Is a technique whereby a stage payload is injected into a compromised host process running in memory, never touching the host hard drive.
#### dll
A Dynamic Link Library (DLL) is a type of file used in Windows (and OS/2) that contains code and data which can be used by multiple programs simultaneously.

## Generating
Each payload has a generate, pry and reload command. 

```plaintext
msf payload(shell_bind_tcp) > generate -h
Usage: generate [options]

Generates a payload.

OPTIONS:

    -E        Force encoding.
    -b   The list of characters to avoid: '\x00\xff'
    -e   The name of the encoder module to use.
    -f   The output file name (otherwise stdout)
    -h   Help banner.
    -i   the number of encoding iterations.
    -k   Keep the template executable functional
    -o   A comma separated list of options in VAR=VAL format.
    -p   The Platform for output.
    -s   NOP sled length.
    -t   The output format: raw,ruby,rb,perl,pl,c,js_be,js_le,java,dll,exe,exe-small,elf,macho,vba,vbs,loop-vbs,asp,war
    -x   The executable template to use
```

To generate shellcode without any options, simply execute the generate command.
**shellcode**: a sequence of machine code instructions.


```plaintext
msf  payload(shell_bind_tcp) > generate -b '\x00'
```

Framework will use the best encoder for the job, when you specifying bad characters with -b.

## Payloads Generation Failed
If you restrict too many bytes and there no a encoder to accomplish the job, return the failed message.

## Using an encoder during payload generating
```plaintext
msf > show encoders
	to show a list with those
msf > generate -e encoder
	to use an specific encoder
msf  payload(shell_bind_tcp) > generate -b '\x00' -e x86/shikata_ga_nai -f /root/msfu/filename.txt
```


AEF 1 - Grammar, vocabulary, listening and speaking.

Criptography, read until next lecture
Logaritmos read information theory chapter, reduction and secondary memory
Data Mining read PPT and/or book
SOS aux 2

Try to read 60 pages of biology book
