---
tags:
    - linux
    - unix
    - gdb
    - dev
---

# GDB

GDB, the GNU Project debugger, allows you to see what is going on `inside' another program while it executes.
Or what another program was doing at the moment it crashed.

## Useful commands

### Build

```bash title="Compile program with debug-symbols"
$ g++ -g main.cpp -o bin
```

### Debug

```bash title="run gnu debugger"
$ gdb bin
```

```bash title="check information about arch and sections"
(gdb) info file
```

```bash title="get list of functions"
@(gdb) i func
All defined functions:

File demo-one.c:
3:      int main();

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  puts@plt
0x0000000000001040  printf@plt
0x0000000000001050  __isoc99_scanf@plt
0x0000000000001060  _start
0x00000000000011b0  _fini
```

```bash title="set breakpoint on main function"
@(gdb) b main
Breakpoint 1 at 0x1141: file demo-two.c, line 4.
```

```bash title="check information about breakpoints"
@(gdb) i b
Num     Type           Disp Enb Address            What
2       breakpoint     keep y   0x0000000000001168 in main at demo-one.c:6
3       breakpoint     keep y   0x0000000000001177 in main at demo-one.c:7
```

```bash title="other useful breakpoints commands"
disable/enable breakpoint_number    // disable/enable
delete breakpoint_number            // delete
ignore breakpoint_number n          // stop on breakpoint after executing it n times
```

```bash title="run program"
@(gdb) r
Starting program: /home/dima/dev/c/gdb-demo/demo-two
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/usr/lib/libthread_db.so.1".

Breakpoint 1, main () at demo-two.c:4
4         int value1 = 5;
```

```bash title="step into"
@(gdb) s
5         int value2 = 10;
```

```bash title="step over line"
@(gdb) n
7         int result = value1 + value2;
```

```bash title="step over instruction(assembly instruction)"
@(gdb) ni
```

```bash title="print values"
@(gdb) p value1
$1 = 5
@(gdb) p value2
$2 = 10
```

```bash title="display value"
@(gdb) disp value1
1: value1 = 5
@(gdb) disp result
2: result = 32767
@(gdb) s
9         printf("Sum of %d and %d is %d\n", value1, value2, result);
1: value1 = 5
2: result = 15
```

```bash title="quit gdb"
@(gdb) q
```

```bash title="set breakpoint on particular string of particular file"
@(gdb) b demo-two.c:7
Breakpoint 1 at 0x114f: file demo-two.c, line 7.
@(gdb) r
Starting program: /home/dima/dev/c/gdb-demo/demo-two
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/usr/lib/libthread_db.so.1".

Breakpoint 1, main () at demo-two.c:7
7         int result = value1 + value2;
```

```bash title="continue programm running"
@(gdb) c
Continuing.
Sum of 5 and 10 is 15
[Inferior 1 (process 50807) exited normally]
```

```bash title="list 10 code lines of current location"
@(gdb) l
2
3       int main() {
4         int value1 = 5;
5         int value2 = 10;
6
7         int result = value1 + value2;
8
9         printf("Sum of %d and %d is %d\n", value1, value2, result);
10
11        return 0;
```

```bash title="more detail views(source code, assembler, registers)"
@(gdb) lay next
@(gdb) lay src
@(gdb) lay asm
@(gdb) lay regs
```

```bash title="refresh the screen"
@(gdb) ref
```

```bash title="print the back trace"
@(gdb) bt
#0  0x00007ffff7e16736 in __vfscanf_internal (s=<optimized out>, format=<optimized out>, argptr=argptr@entry=0x7fffffffd9c0, mode_flags=mode_flags@entry=2) at vfscanf-internal.c:1976
#1  0x00007ffff7e04986 in __isoc99_scanf (format=<optimized out>) at isoc99_scanf.c:30
#2  0x0000555555555190 in main () at demo-one.c:7
```

```bash title="examine memory"
@(gdb) x/i $pc
=> 0x7ffff7e16736 <__vfscanf_internal+22086>:   mov    %edx,(%rax)

x/i - instruction
x/x - hex
x/s - string
x/a - address

x/b - 8-bit
x/h - 16-bit
x/w - 32-bit
x/g - 64-bit
```

