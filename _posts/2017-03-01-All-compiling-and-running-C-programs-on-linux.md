Steps to Compile and Execute C Program in Linux Using GCC :--


--> Before talking of compiling and running C program in Linux let's see why C is so popular ever since it was created. He was the Dennis Ritchie who developed C language in 1969 to 1973. C was developed from the beginning as the system programming language for UNIX. Most of the UNIX kernel, and all of its supporting tools and libraries, were written in C. Initially, C was designed to implement the UNIX operating system. Later other folks found it useful for their programs without any hindrance, and they began using it. Even today, C is the first choice for system-level programming. This tutorial explains compilation and execution of C program is in detail.
Compile C Program in Linux - A Classic example Hello World! :--


#include <stdio.h>
int main()
{
printf("hello, world!\n");
}
/* helloworld.c */


---> To compile and run this C program every part of the system has to perform in concert. In order to compile above C program in Linux, we will start right from the creation of the program. The 'Hello World!' program starts its life as a source file which is created with help of a text editor and saved as helloworld.c. The helloworld.c program code is stored in a file as a sequence of bytes. Each byte has a value corresponding to some character. The first byte has the value 35 that corresponds to the character '#', for example. Likewise, the second byte has the integer value 105, which corresponds to the character 'i', and so on. The idea illustrates that all information in a system is represented as a bunch of bits.


---> To compile and run the C program helloworld.c, all C statements must be translated individually into a sequence of instructions that a machine can understand. These instructions are then packaged in a form called executable object program. There are other programs which perform this task to get the program running. On a UNIX/Linux system, the translation from source code to object code (executable) is performed by a compiler driver. Here we will compile C program by gcc.


---> The following command (provided that gcc is installed on your Linux box) compiles C program helloworld.c and creates an executable file called helloworld. Don't forget to set appropriate permissions to helloworld.c, so that you won't get execute permission errors.

[root@host ~]# gcc helloworld.c -o helloworld
While compiling helloworld.c the gcc compiler reads the source file helloworld.c and translates it into an executable helloworld. The compilation is performed in four sequential phases by the compilation system (a collection of four programs - preprocessor, compiler, assembler, and linker).
Now, let's perform all four steps to compile and run C program one by one.

1. Preprocessing :---
During compilation of a C program the compilation is started off with preprocessing the directives (e.g., #include and #define). The preprocessor (cpp - c preprocessor) is a separate program in reality, but it is invoked automatically by the compiler. For example, the #include <stdio.h> command in line 1 of helloworld.c tells the preprocessor to read the contents of the system header file stdio.h and insert it directly into the program text. The result is another file typically with the .i suffix. In practice, the preprocessed file is not saved to disk unless the -save-temps option is used.
This is the first stage of compilation process where preprocessor directives (macros and header files are most common) are expanded. To perform this step gcc executes the following command internally.
[root@host ~]# cpp helloworld.c > helloworld.i
The result is a file helloworld.i that contains the source code with all macros expanded. If you execute the above command in isolation then the file helloworld.i will be saved to disk and you can see its content by vi or any other editor you have on your Linux system.
2. Compilation :---
In this phase compilation proper takes place. The compiler (ccl) translates helloworld.i into helloworld.s. File helloworld.s contains assembly code. You can explicitly tell gcc to translate helloworld.i to helloworld.s by executing the following command.
[root@host ~]# gcc -S helloworld.i
The command line option -S tells the compiler to convert the preprocessed code to assembly language without creating an object file. After having created helloworld.s you can see the content of this file. While looking at assembly code you may note that the assembly code contains a call to the external function printf.
3. Assembly :---
Here, the assembler (as) translates helloworld.s into machine language instructions, and generates an object file helloworld.o. You can invoke the assembler at your own by executing the following command.
[root@host ~]# as helloworld.s -o helloworld.o
The above command will generate helloworld.o as it is specified with -o option. And, the resulting file contains the machine instructions for the classic "Hello World!" program, with an undefined reference to printf.
4. Linking :---
This is the final stage in compilation of "Hello World!" program. This phase links object files to produce final executable file. An executable file requires many external resources (system functions, C run-time libraries etc.). Regarding our "Hello World!" program you have noticed that it calls the printf function to print the 'Hello World!' message on console. This function is contained in a separate pre compiled object file printf.o, which must somehow be merged with our helloworld.o file. The linker (ld) performs this task for you. Eventually, the resulting file helloworld is produced, which is an executable. This is now ready to be loaded into memory and executed by the system.
[root@host ~]# ./helloworld
Output:
hello, world!
The entire linking process is handled transparently by gcc when invoked, as follows.
[root@host ~]# gcc helloworld.c -o helloworld
During the whole compilation process there are other files also in role along with the source code file. If you see the very first statement of helloworld.c it is #include <stdio.h> (includes header file). Likewise, while compiling a C program you have to work with following types of files.
Program Translation :---
Source code files :---
--> These files contain high level program code which can be read and understood by programmers. Such files carry .c extension by convention.
Header files :---
--> These types of files contain function declarations (also known as function prototypes) and various preprocessor statements. They are used to allow source code files to access externally-defined functions. As a convention header files have .h extension.
Object files :---
--> These files are produced as an intermediate output by the gcc compiler during program compilation. They consist of function definitions in binary form, but they are not executable by themselves. Object files end with .o extension by convention (on UNIX like operating systems), although on some operating systems e.g., Windows, and MS-DOS they often end in .obj.
Binary executables :---
--> These are produced as the output of a program called a linker. During the process of compiling and running C program the linker links together a number of object files to produce a binary file which can be directly executed. Binary executables have no special suffix on UNIX like operating systems, while they generally have .exe on Windows.
Along with above four types of files, while compiling a C program you can come across .a and .so, static and shared libraries respectively, but you would not normally deal with them directly.
Last Word :---
In this article I explained compilation and execution process steps and stages of C program in Linux using gcc . Various phases during compilation and execution process of a C program take place, such as, preprocessing, compilation, assembly, and linking. Hope you have enjoyed reading this article. Please write us if you have any suggestion/comment or come across any error on this page. Thanks for reading!
