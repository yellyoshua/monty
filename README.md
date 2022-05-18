# 0x19. C - Stacks, Queues - LIFO, FIFO
## Resources
Read or watch :
* [Google](https://intranet.hbtn.io/rltoken/56-bDz7IrFgcH02EkGkB3w) 

* [How do I use extern to share variables between source files in C?](https://intranet.hbtn.io/rltoken/9neX6gaN6DoA-ow1INgZqw) 

## Learning Objectives
At the end of this project, you are expected to be able to  [explain to anyone](https://intranet.hbtn.io/rltoken/S9hXXmjvT8hvNyFQLnSGug) 
 ,  without the help of Google :
### General
* What do LIFO and FIFO mean
* What is a stack, and when to use it
* What is a queue, and when to use it
* What are the common implementations of stacks and queues
* What are the most common use cases of stacks and queues
* What is the proper way to use global variables
## Requirements
### General
* Allowed editors:  ` vi ` ,  ` vim ` ,  ` emacs ` 
* All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options -Wall -Werror -Wextra -pedantic -std=gnu89
* All your files should end with a new line
* A  ` README.md `  file, at the root of the folder of the project is mandatory
* Your code should use the  ` Betty `  style. It will be checked using [betty-style.pl](https://github.com/holbertonschool/Betty/blob/master/betty-style.pl) 
 and [betty-doc.pl](https://github.com/holbertonschool/Betty/blob/master/betty-doc.pl) 

* You allowed to use a maximum of one global variable
* No more than 5 functions per file
* You are allowed to use the C standard library
* The prototypes of all your functions should be included in your header file called  ` monty.h ` 
* Don’t forget to push your header file
* All your header files should be include guarded
* You are expected to do the tasks in the order shown in the project
### GitHub
There should be one project repository per group. If you clone/fork/whatever a project repository with the same name before the second deadline, you risk a 0% score.
## More Info
### Data structures
Please use the following data structures for this project. Don’t forget to include them in your header file.
```bash
/**
 * struct stack_s - doubly linked list representation of a stack (or queue)
 * @n: integer
 * @prev: points to the previous element of the stack (or queue)
 * @next: points to the next element of the stack (or queue)
 *
 * Description: doubly linked list node structure
 * for stack, queues, LIFO, FIFO
 */
typedef struct stack_s
{
        int n;
        struct stack_s *prev;
        struct stack_s *next;
} stack_t;

```
```bash
/**
 * struct instruction_s - opcode and its function
 * @opcode: the opcode
 * @f: function to handle the opcode
 *
 * Description: opcode and its function
 * for stack, queues, LIFO, FIFO
 */
typedef struct instruction_s
{
        char *opcode;
        void (*f)(stack_t **stack, unsigned int line_number);
} instruction_t;

```
### Compilation & Output
* Your code will be compiled this way:
 ` $ gcc -Wall -Werror -Wextra -pedantic -std=gnu89 *.c -o monty
 ` * Any output must be printed on  ` stdout ` 
* Any error message must be printed on  ` stderr ` * [Here is a link to a GitHub repository](https://intranet.hbtn.io/rltoken/9RfVU4j7qVbFgGdMkpX2qA) 
 that could help you making sure your errors are printed on  ` stderr ` 

### Tests
We strongly encourage you to work all together on a set of tests
### The Monty language
Monty 0.98 is a scripting language that is first compiled into Monty byte codes (Just like Python). It relies on a unique stack, with specific instructions to manipulate it. The goal of this project is to create an interpreter for Monty ByteCodes files.
Monty byte code files
Files containing Monty byte codes usually have the   ` .m `   extension. Most of the industry uses this standard but it is not required by the specification of the language.There is not more than one instruction per line. There can be any number of spaces before or after the opcode and its argument:
```bash
julien@ubuntu:~/monty$ cat -e bytecodes/000.m
push 0$
push 1$
push 2$
  push 3$
                   pall    $
push 4$
    push 5    $
      push    6        $
pall$
julien@ubuntu:~/monty$

```
Monty byte code files can contain blank lines (empty or made of spaces only, and any additional text after the opcode or its required argument is not taken into account:
```bash
julien@ubuntu:~/monty$ cat -e bytecodes/001.m
push 0 Push 0 onto the stack$
push 1 Push 1 onto the stack$
$
push 2$
  push 3$
                   pall    $
$
$
                           $
push 4$
$
    push 5    $
      push    6        $
$
pall This is the end of our program. Monty is awesome!$
julien@ubuntu:~/monty$

```
The monty program
* Usage:  ` monty file ` * where  ` file `  is the path to the file containing Monty byte code

* If the user does not give any file or more than one argument to your program, print the error message  ` USAGE: monty file ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` 
* If, for any reason, it’s not possible to open the file, print the error message  ` Error: Can't open file <file> ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` * where  ` <file> `  is the name of the file

* If the file contains an invalid instruction, print the error message  ` L<line_number>: unknown instruction <opcode> ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` * where  is the line number where the instruction appears.
* Line numbers always start at 1

* The monty program runs the bytecodes line by line and stop if either:* it executed properly every line of the file
* it finds an error in the file
* an error occured

* If you can’t malloc anymore, print the error message  ` Error: malloc failed ` , followed by a new line, and exit with status  ` EXIT_FAILURE ` .
* You have to use  ` malloc `  and  ` free `  and are not allowed to use any other function from  ` man malloc `  (realloc, calloc, …)
### Quiz questions
Great!          You've completed the quiz successfully! Keep going!          (Show quiz)#### 
        
        Question #0
    
 Quiz question Body Which of these methods are keeping the order of insertion? (select all possible answers)
 Quiz question Answers * FIFO

* FILO

* LIFO

* LILO

### 0. push, pall
          mandatory         Progress vs Score  Task Body Implement the   ` push `   and   ` pall `   opcodes.
The push opcode
The opcode   ` push `   pushes an element to the stack.
* Usage:  ` push <int> ` * where  ` <int> `  is an integer

* if  ` <int> `  is not an integer or if there is no argument given to  ` push ` , print the error message  ` L<line_number>: usage: push integer ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` * where  is the line number in the file

* You won’t have to deal with overflows. Use the  ` atoi `  function
The pall opcode
The opcode   ` pall `   prints all the values on the stack, starting from the top of the stack.
* Usage  ` pall ` 
* Format: see example
* If the stack is empty, don’t print anything
```bash
julien@ubuntu:~/monty$ cat -e bytecodes/00.m
push 1$
push 2$
push 3$
pall$
julien@ubuntu:~/monty$ ./monty bytecodes/00.m
3
2
1
julien@ubuntu:~/monty$

```
 Task URLs  Github information Repo:
* GitHub repository:  ` monty ` 
 Self-paced manual review  Panel footer - Controls 
### 1. pint
          mandatory         Progress vs Score  Task Body Implement the   ` pint `   opcode.
The pint opcode
The opcode   ` pint `   prints the value at the top of the stack, followed by a new line.
* Usage:  ` pint ` 
* If the stack is empty, print the error message  ` L<line_number>: can't pint, stack empty ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` 
```bash
julien@ubuntu:~/monty$ cat bytecodes/06.m 
push 1
pint
push 2
pint
push 3
pint
julien@ubuntu:~/monty$ ./monty bytecodes/06.m 
1
2
3
julien@ubuntu:~/monty$ 

```
 Task URLs  Github information Repo:
* GitHub repository:  ` monty ` 
 Self-paced manual review  Panel footer - Controls 
### 2. pop
          mandatory         Progress vs Score  Task Body Implement the   ` pop `   opcode.
The pop opcode
The opcode   ` pop `   removes the top element of the stack.
* Usage:  ` pop ` 
* If the stack is empty, print the error message  ` L<line_number>: can't pop an empty stack ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` 
```bash
julien@ubuntu:~/monty$ cat bytecodes/07.m 
push 1
push 2
push 3
pall
pop
pall
pop
pall
pop
pall
julien@ubuntu:~/monty$ ./monty bytecodes/07.m 
3
2
1
2
1
1
julien@ubuntu:~/monty$ 

```
 Task URLs  Github information Repo:
* GitHub repository:  ` monty ` 
 Self-paced manual review  Panel footer - Controls 
### 3. swap
          mandatory         Progress vs Score  Task Body Implement the   ` swap `   opcode.
The swap opcode
The opcode   ` swap `   swaps the top two elements of the stack.
* Usage:  ` swap ` 
* If the stack contains less than two elements, print the error message  ` L<line_number>: can't swap, stack too short ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` 
```bash
julien@ubuntu:~/monty$ cat bytecodes/09.m 
push 1
push 2
push 3
pall
swap
pall
julien@ubuntu:~/monty$ ./monty bytecodes/09.m 
3
2
1
2
3
1
julien@ubuntu:~/monty$ 

```
 Task URLs  Github information Repo:
* GitHub repository:  ` monty ` 
 Self-paced manual review  Panel footer - Controls 
### 4. add
          mandatory         Progress vs Score  Task Body Implement the   ` add `   opcode.
The add opcode
The opcode   ` add `   adds the top two elements of the stack.
* Usage:  ` add ` 
* If the stack contains less than two elements, print the error message  ` L<line_number>: can't add, stack too short ` , followed by a new line, and exit with the status  ` EXIT_FAILURE ` 
* The result is stored in the second top element of the stack, and the top element is removed, so that at the end:* The top element of the stack contains the result
* The stack is one element shorter

```bash
julien@ubuntu:~/monty$ cat bytecodes/12.m 
push 1
push 2
push 3
pall
add
pall

julien@ubuntu:~/monty$ ./monty bytecodes/12.m 
3
2
1
5
1
julien@ubuntu:~/monty$

```
 Task URLs  Github information Repo:
* GitHub repository:  ` monty ` 
 Self-paced manual review  Panel footer - Controls 
### 5. nop
          mandatory         Progress vs Score  Task Body Implement the   ` nop `   opcode.
The nop opcode
The opcode   ` nop `   doesn’t do anything.
* Usage:  ` nop ` 
 Task URLs  Github information Repo:
* GitHub repository:  ` monty ` 
 Self-paced manual review  Panel footer - Controls 
[Done with the mandatory tasks? Unlock 14 advanced tasks now!](https://intranet.hbtn.io/projects/249/unlock_optionals) 

×#### Recommended Sandbox
[Running only]() 
### 1 image(1/5 Sandboxes spawned)
### Ubuntu 20.04
Basic Ubuntu 20.04, with vim, emacs, curl, wget and all needed for Holberton Foundations
SSHSFTP[Webterm](https://intranet.hbtn.io/user_containers/20136/webterm) 
[Restart]() 
[Destroy]() 
#### Credentials
Hostd0e3df2a9605.382951ab.hbtn-cod.ioUsernamed0e3df2a9605Passwordbec8653482c2d48c9d21#### Web access
[HTTPS](https://d0e3df2a9605.382951ab.hbtn-cod.io/) 
[HTTP](http://d0e3df2a9605.382951ab.hbtn-cod.io/) 
[3000](http://d0e3df2a9605.382951ab.hbtn-cod.io:3000/) 
[4000](http://d0e3df2a9605.382951ab.hbtn-cod.io:4000/) 
[5000](http://d0e3df2a9605.382951ab.hbtn-cod.io:5000/) 
[5001](http://d0e3df2a9605.382951ab.hbtn-cod.io:5001/) 
[8000](http://d0e3df2a9605.382951ab.hbtn-cod.io:8000/) 
[8080](http://d0e3df2a9605.382951ab.hbtn-cod.io:8080/) 
#### Port mapping
SSH49162HTTP49161HTTPS49160300049159MySQL49158400049157500049156500149155800049154808049153