# Purpose
This C++ source code file is an executable program that utilizes the CLI11 library to handle command-line arguments. The primary purpose of this code is to demonstrate a mechanism for passing through command-line arguments to a sub-application within the same program. The code defines a main function that sets up a CLI application named "callback_passthrough" and allows for additional, unspecified arguments. It introduces two string variables, `argName` and `val`, where `argName` is used to specify a custom command-line argument name, and `val` is intended to store the value associated with this custom argument.

The code's most significant technical component is the use of a callback function, which is triggered if `argName` is not empty. This callback creates a sub-application that adds an option based on the custom argument name provided by the user. The sub-application then parses any remaining arguments that were not initially processed by the main application. This design allows for dynamic handling of command-line arguments, where users can specify custom argument names at runtime. The program concludes by outputting the value associated with the custom argument, demonstrating the successful parsing and handling of command-line inputs.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `string`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function sets up a command-line interface application that allows for a custom argument name and value to be parsed and displayed.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI::App object named 'app' with the description 'callback_passthrough'.
    - Enable the application to accept extra arguments beyond those explicitly defined.
    - Declare two strings, 'argName' and 'val', to store the custom argument name and its value respectively.
    - Add an option '--argname' to the app to capture the custom command line argument name into 'argName'.
    - Define a callback function that checks if 'argName' is not empty, then creates a sub-application 'subApp'.
    - Add an option to 'subApp' using the custom argument name stored in 'argName' and parse the remaining arguments for passthrough.
    - Parse the command-line arguments using CLI11_PARSE macro, which processes the arguments according to the defined options and callback.
    - Output the value of 'val' to the console.
- **Output**: The function outputs a string to the console indicating the value of the custom argument, if provided.


