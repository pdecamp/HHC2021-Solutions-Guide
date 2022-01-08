# Objective 6) Shellcode Primer

!!! summary "*Difficulty*: :fontawesome-solid-tree:{: style="color: red;"}:fontawesome-solid-tree:{: style="color: red;"}:fontawesome-solid-tree:{: style="color: red;"}:fontawesome-solid-tree:{: style="color: grey;"}:fontawesome-solid-tree:{: style="color: grey;"}"
    Complete the <a href="https://tracer.kringlecastle.com/">Shellcode Primer</a> in Jack's office. According to the last challenge, what is the secret to KringleCon success? "All of our speakers and organizers, providing the gift of ____, free to the community." Talk to Chimney Scissorsticks in the NetWars area for hints.


## Hints and Resources

??? hint "Hints provided after helping Chimney Scissorsticks and completing the <a href="../../challenges/T6_Holiday_Hero">Holiday Hero</a> Terminal Challenge"
    **Shellcode Primer Primer**<br>
    If you run into any shellcode primers at the North Pole, be sure to read the directions and the comments in the shellcode source!<br>
    <br>
    **Debugging Shellcode**<br>
    Also, troubleshooting shellcode can be difficult. Use the debugger step-by-step feature to watch values.<br>
    <br>
    **Register Stomping**<br>
    Lastly, be careful not to overwrite any register values you need to reference later on in your shellcode.<br>


## Troll Introduction

??? quote "Talk to Ruby Cyster in Jack's Office"
    Hey, I'm Ruby Cyster. Don't listen to anything my sister, Ingreta, says about me.<br>
    So I'm looking at this system, and it has me a little bit worried.<br>
    If I didn't know better, I'd say someone here is learning how to hack North Pole systems.<br>
    Who's got that kind of nerve!<br>
    Anyway, I hear some elf on the other roof knows a bit about this type of thing.

## Solution

Open the Shellcode Primer by clicking on the monitor next to Ruby or use the direct link <a href="https://tracer.kringlecastle.com">https://tracer.kringlecastle.com</a>.

The primer will walk you through eleven progressively more difficult shellcode exercises, solutions for which are provided below.

### 1 - Introduction

No code needs to be added to complete this level.

### 2 - Loops

No code needs to be added to complete this level


### 3 - Getting Started

``` nasm
; This is a comment! We'll use comments to help guide your journey.
; Right now, we just need to RETurn!
;
; Enter a return statement below and hit Execute to see what happens!
ret
```

### 4 - Returning a Value

``` nasm
; TODO: Set rax to 1337
mov rax, 1337
ret

; Return, just like we did last time
ret
```

### 5 - System Calls

```nasm
; TODO: Find the syscall number for sys_exit and put it in rax
mov rax, 60

; TODO: Put the exit_code we want (99) in rdi
mov rdi, 99

; Perform the actual syscall
syscall
```

### 6 - Calling Into the Void

No code needs to be added to complete this level


### 7 - Getting RIP

``` nasm
; Remember, this call pushes the return address to the stack
call place_below_the_nop

; This is where the function *thinks* it is supposed to return
nop

; This is a 'label' - as far as the call knows, this is the start of a function
place_below_the_nop:

; TODO: Pop the top of the stack into rax
pop rax

; Return from our code, as in previous levels
ret
```

### 8 - Hello, World!

``` nasm
; This would be a good place for a call
call foo

; This is the literal string 'Hello World', null terminated, as code. Except
; it'll crash if it actually tries to run, so we'd better jump over it!
db 'Hello World',0

; This would be a good place for a label and a pop
foo:
pop rax

; This would be a good place for a re... oh wait, it's already here. Hooray!
ret
```

### 9 - Hello, World!!

``` nasm
; TODO: Get a reference to this string into the correct register
call foo
db 'Hello World!',0
foo:

; Set up a call to sys_write
; TODO: Set rax to the correct syscall number for sys_write
mov rax, 1

; TODO: Set rdi to the first argument (the file descriptor, 1)
mov rdi, 1

; TODO: Set rsi to the second argument (buf - this is the "Hello World" string)
pop rsi

; TODO: Set rdx to the third argument (length of the string, in bytes)
mov rdx, 12

; Perform the syscall
syscall

; Return cleanly
ret
```

### 10 - Opening a File

``` nasm
; TODO: Get a reference to this string into the correct register
call foo
db '/etc/passwd',0
foo:

; Set up a call to sys_open
; TODO: Set rax to the correct syscall number
mov rax, 2

; TODO: Set rdi to the first argument (the filename)
pop rdi

; TODO: Set rsi to the second argument (flags - 0 is fine)
mov rsi, 0

; TODO: Set rdx to the third argument (mode - 0 is also fine)
mov rdx, 0

; Perform the syscall
syscall

; syscall sets rax to the file handle, so to return the file handle we don't
; need to do anything else!
ret
```

### 11 - Reading a File

``` nasm
; TODO: Get a reference to this
call foo
db '/var/northpolesecrets.txt',0
foo:

; TODO: Call sys_open
; rax = sys_open(2), rdi = filename, rsi and rdx = 0
mov rax, 2
pop rdi
mov rsi, 0
mov rdx, 0
syscall

; TODO: Call sys_read on the file handle and read it into rsp
; rax = sys_read(0), rdi = file handle, rsi = rsp (buffer), rdx = number of chars to read
; remember that the previous syscall set rax to the value of the file handle
mov rdi, rax
mov rax, 0
mov rsi , rsp
mov rdx, 255
syscall

; TODO: Call sys_write to write the contents from rsp to stdout (1)
; rax = sys_write(1), rdi = stdout(1), rsi = buffer to output, rdx = number of chars
mov rax, 1
mov rdi, 1
mov rsi, rsp
mov rdx, 255
syscall

; TODO: Call sys_exit
mov rax, 60
syscall
```




## Completion


Running the code for the last exercise sends the following text to Stdout<br>
`Secret to KringleCon success: all of our speakers and organizers, providing the gift of cyber security knowledge, free to the community.`

!!! success "Answer"
    cyber security knowledge

??? quote "Talk to Ruby Cyster to receive hints for <a href="../O7_Printer_Exploitation">Objective 7) Printer Exploitation</a>"
    Oh man - what is this all about? Great work though.<br>
    So first things first, you should definitely take a look at the firmware.<br>
    With that in-hand, you can pick it apart and see what's there.<br>
    Did you know that if you append multiple files of that type, the last one is processed?<br>
    Have you heard of <a href="https://blog.skullsecurity.org/2012/everything-you-need-to-know-about-hash-length-extension-attacks">Hash Extension Attacks</a>?<br>
    If something isn't working, be sure to check the output! The error messages are very verbose.<br>
    Everything else accomplished, you just might be able to get shell access to that dusty old thing!
