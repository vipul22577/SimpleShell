SimpleShell is a basic command-line interface developed in C that allows users to interact with the operating system by executing standard shell commands. It also maintains a command execution history including process IDs and execution times. This project demonstrates core concepts of process handling, system calls, and file operations in Linux.

Major Components: 

1. Header Files

The following headers are used for accessing standard libraries and system-level functions:
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <sys/time.h>
#include <errno.h>

2. History Management:
A file named history.txt stores a log of executed commands. Each entry includes the command, its PID, and the time it took to execute. A struct is used to hold command information in memory.

3.Functional Modules: 
main(): Initializes variables and starts an infinite loop. Continuously accepts and executes user input. Maintains the execution history using a history array.

promptdisplay(): Displays the current working directory as a shell prompt.

user_input(): Reads, trims, and allocates memory for the user's input.

launch(): Handles internal commands:

exit: Saves history and exits the shell.

history: Displays the history of executed commands.

For all other inputs, it delegates to run_command().

run_command(): Forks a child process and executes the command using execvp().

Tracks execution time and stores command info in memory.

writeHistory(): Writes the in-memory history to history.txt.

printHistory() and temphistory(): Read and display contents of history.txt or in-memory command history.


Limitations

cd Command: Directory changes only affect the child process, not the shell itself.

jobs Command: Not supported, as it requires built-in shell management for background jobs.

Background Processes: The shell currently waits for each command to complete (waitpid()), so it cannot handle concurrent background tasks.

