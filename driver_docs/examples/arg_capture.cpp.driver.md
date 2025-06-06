# Purpose
This C++ source code file is an example program demonstrating the use of the CLI11 library, specifically focusing on the `prefix_command` feature for subcommands. The code is structured as an executable application, as indicated by the presence of the [`main`](#main) function. The primary functionality of this program is to parse command-line arguments using the CLI11 library, which is a powerful and flexible library for handling command-line interfaces in C++. The program sets up a main application with a single option `-v` to capture an integer value and a subcommand `sub` (with an alias `--sub`) that captures all subsequent arguments using the `prefix_command` method. This allows the subcommand to behave like a regular option, capturing all arguments that follow it.

The technical components of this code include the use of the CLI11 library to define command-line options and subcommands. The `CLI::App` object is used to define the main application, and the `add_option` and `add_subcommand` methods are used to specify the options and subcommands, respectively. The `CLI11_PARSE` macro is employed to parse the command-line arguments. The program outputs the value of the `-v` option and lists all arguments captured by the subcommand, demonstrating how the `remaining()` method can be used to access these arguments. This example serves as a practical illustration of how to implement and utilize subcommands with prefixed arguments in a command-line application using CLI11.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `string`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application that parses command-line arguments, including a subcommand with a prefix, and outputs the parsed values and remaining arguments.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize an integer variable `value` to 0.
    - Create a `CLI::App` object named `app` with the description 'Test App'.
    - Add an option '-v' to the app that modifies the `value` variable and has a description 'value'.
    - Add a subcommand 'sub' to the app, enabling it to capture all subsequent arguments using `prefix_command()`.
    - Set an alias '--sub' for the subcommand.
    - Parse the command-line arguments using `CLI11_PARSE(app, argc, argv);`.
    - Output the value of `value` to the console.
    - Iterate over the remaining arguments captured by the subcommand and output them to the console.
- **Output**: The function outputs the value of the `-v` option and any remaining arguments after the 'sub' or '--sub' subcommand to the console.


