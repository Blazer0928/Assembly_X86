### Assembly_X86
# Me Learning Assembly Notes as Such.
1. [Introduction](#Introduction)
    Assembly language is same as machine language, except the command numbers have been replaced by letter sequence which are easier to memorize.
2. [Hello_World](#Hello_World)

## Hello World Program-Assembly-x86

<pre lang="markdown">
; code...
 section .data
   msg db "hello world", 0x0A ; new line character at the end
   len equ $ - msg            ; calculate the length of the string
 section .text
    global _start
 _start:
   mov eax, 4                 ; 4 is the system call number associated with the write operation
                               ; write (fd , string_address, offset) it is c-style syntax for write system call    
                              ; the input arguments will be passed on using "ebx" - fd, "ecx" - msg-starting address , "edx" as a offset (length)
   mov ebx, 1                 ; fd = stdout 
   mov ecx, msg
   mov edx, len               ; length of the message
   int 0x80                   ; Interrupt call the system call in eax

 ; to exit cleanly 
   mov eax, 1 
   mov ebx, 0                  ; for exit code 
   int 0x80  </pre>

## Compile and Link 

<pre lang="markdown">
nasm -f elf32 hello.asm -o hello.o 
#this compiles the binary to 32bit
ld -m elf_i386 hello.o -o hello 
#this linkes the object file to executable
./hello 
</pre>

## Computer Architecture

cpu - The instructions are read from memory one at a time and executes them. This is known as "fetch-execute cycle".
This is accomplished using,
1. program counter
2. instructions Decoder
3. Data Bus
4. General-purpose register
5. Arithmetic and logic unit

since the instructions are stored in memory program counter hold the address to the next instruction to be executed 
-> then passed to instruction Decoder it decodes the instruction(addition, sub, multi, data moving) etc... 
-> data Bus is used to fetch or send data to a specified location 
-> General-purpose registers are high speed registers used for calculations it also have special purpose registers that have so special use case 
-> Arithmetic and logic unit for Arithmetic and logical calculations.
