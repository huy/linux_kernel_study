﻿## How debugger works

The implementation of debugger uses of system call ptrace.
A process ask the kernel  allow its parent (the debugger) to trace it (PTRACE_TRACEME). The process being 
traced will be stopped by the kernel whenever it receives a signal except KILL. 

The debugger establishes parent/child relationship (in this case real_parent and parent are different) 
with a process being traced so can receive (by calling system call wait/waitpid) any signals (except KILL) sent 
to the process being traced.

The debugger ask the kernel to step (PTRACE_SINGLESTEP), continue execution (PTRACE_CONT) the process being traced.

**breakpoint**

The debugger can set a breakpoint by changing an instruction (PTRACE_POKETEXT) at desire location with INT 3 (raise SIGTRAP).
Then it can examine, modify content of memory & registries using PTRACE_PEEKTEXT, PTRACE_PEEKDATA, PTRACE_GETREGS.
Finally rewinds instruction pointer (regs.eip=-1, PTRACE_SETREGS), restores original instruction then continue 
execution (PTRACE_CONT) .

**References**

1. http://eli.thegreenplace.net/2011/01/23/how-debuggers-work-part-1/
2. http://www.linuxjournal.com/article/6100?page=0,2