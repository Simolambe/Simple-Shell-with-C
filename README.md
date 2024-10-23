# Simple-Shell-with-C
Overview
This C program implements a basic shell that processes user commands, executes them, and supports background execution. The shell, called smallsh, mimics a minimal command-line interface where users can input commands and receive outputs as in traditional Unix-based shells.

Key Components
Variables and Definitions
prompt: A string that stores the command prompt message, which is displayed before the user input.
background: A flag used to determine whether the command should run in the background (background = 1) or in the foreground (background = 0).
MAXARG: A constant that limits the number of arguments that can be passed with a command (defined in the header file smallsh.h).
Functions
procline():

This function processes the input line entered by the user, breaks it into tokens (such as arguments or special symbols like ; or &), and determines how to handle the command.
It handles different types of tokens:
ARG: Represents a valid argument in the command.
EOL (End of Line) and SEMICOLON: Marks the end of a command, which triggers execution of the current command with the runcommand() function.
AMPERSAND (&): Indicates that the command should be executed in the background.
The command and its arguments are stored in an array arg[]. After detecting the end of a command, the function clears the arguments and waits for the next command.
**runcommand(char cline, int background):

This function is responsible for executing a command. It uses the system call fork() to create a new process.
fork() creates a child process to execute the command using execvp(), which replaces the child process image with the new program specified by the command (cline).
If the command is not intended for background execution (background == 0), the parent process waits for the child to complete using wait(). For background processes, the parent does not wait, allowing the shell to continue accepting new commands while the background process runs.
main():

The main function initializes the shell and sets up the prompt format, which includes the current user's name and home directory. This is done using environment variables USER and HOME.
It enters a loop that repeatedly prompts the user for input, processes the input with procline(), and continues until the user exits (EOF).
Features and Behavior
Command Execution: The shell can execute commands entered by the user, similar to a regular Unix shell.
Background Execution: The shell supports running commands in the background by appending & to the command (e.g., ls &).
Prompt Customization: The prompt displays the current user's name and home directory, making it more personalized.
Token Handling: The shell processes commands token by token, which allows for parsing complex commands and running multiple commands sequentially (e.g., using ; to separate commands).
