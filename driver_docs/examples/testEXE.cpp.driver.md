# Purpose
This C++ source code file is an executable program that utilizes the CLI11 library to create a command-line interface application. The primary purpose of this code is to demonstrate how to set up a basic command-line application with options and subcommands using the CLI11 library. The code defines a main function, which is the entry point of the program, and it includes the necessary headers to use the CLI11 functionalities. The application is named "Test App" and includes an option `-v` to accept an integer value from the user. Additionally, it defines a subcommand "sub" that can accept additional arguments, showcasing the ability to handle complex command-line inputs.

The code is structured to parse command-line arguments using the `CLI11_PARSE` macro, which processes the input arguments and configures the application accordingly. The program then outputs the value of the `-v` option and any remaining arguments associated with the "sub" subcommand. This file is a standalone executable and does not define public APIs or external interfaces, as its primary focus is on demonstrating the use of CLI11 for command-line parsing. The code is a practical example of how to implement command-line options and subcommands, making it useful for developers looking to integrate similar functionality into their applications.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `string`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application, parses command-line arguments, and outputs the parsed value and remaining subcommand arguments.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize an integer variable `value` to 0.
    - Create a `CLI::App` object named `app` with the description 'Test App'.
    - Add an option '-v' to the `app` that modifies the `value` variable when specified.
    - Add a subcommand 'sub' to the `app` and enable prefix command mode for it.
    - Parse the command-line arguments using `CLI11_PARSE` macro with `app`, `argc`, and `argv`.
    - Output the parsed `value` to the console.
    - Iterate over the remaining arguments of the subcommand and output each to the console.
- **Output**: The function outputs the parsed value of the '-v' option and any remaining arguments of the 'sub' subcommand to the console.


