sudo apt update
sudo apt install -y nasm gcc gcc-multilib libc6-dev-i386
nasm -v
gcc -m32 --version

section .data
    msg db "Hello, NASM32!", 10
    len equ $ - msg
section .text
    global _start
_start:
    mov eax, 4
    mov ebx, 1
    mov ecx, msg
    mov edx, len
    int 0x80
    mov eax, 1
    xor ebx, ebx
    int 0x80

nasm -f elf32 hello.asm -o hello.o
ld -m elf_i386 hello.o -o hello
./hello
 