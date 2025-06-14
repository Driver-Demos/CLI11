# Purpose
This C++ source code file defines a command-line interface (CLI) application named "Geet," which is a mock version of the Git command-line tool. The code utilizes the CLI11 library to create a structured command-line application that mimics some basic Git commands, specifically "add" and "commit." The primary purpose of this file is to demonstrate how to set up a CLI application with subcommands and options using the CLI11 library. The application requires exactly one subcommand to be executed, either "add" or "commit," each with its own set of options and behaviors.

The "add" subcommand allows users to specify files to add, with an optional flag to add only updated files. The "commit" subcommand requires a commit message to be provided. Each subcommand is associated with a callback function that outputs a message to the console, simulating the action of adding or committing files. The code is structured to parse command-line arguments and execute the appropriate subcommand based on user input. This file is an executable C++ program, as indicated by the presence of the [`main`](#main) function, and it does not define public APIs or external interfaces beyond the command-line interface it provides.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line application that mimics git commands, specifically handling 'add' and 'commit' subcommands with options and callbacks.
- **Inputs**:
    - `argc`: An integer representing the number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the actual command-line arguments.
- **Control Flow**:
    - Initialize a CLI application named 'Geet' with a requirement for at least one subcommand.
    - Define an 'add' subcommand with options for updating files and specifying files to add.
    - Set a callback for the 'add' subcommand to print the files being added or a message indicating all files or updated files are being added.
    - Define a 'commit' subcommand with a required message option.
    - Set a callback for the 'commit' subcommand to print the commit message.
    - Parse the command-line arguments using the CLI11 library.
    - Print a thank you message and return 0 to indicate successful execution.
- **Output**: The function returns an integer 0, indicating successful execution of the program.


