# Purpose
This code is a C++ executable that demonstrates the use of the CLI11 library to handle command-line arguments. It provides narrow functionality, specifically focusing on parsing command-line inputs using a subcommand structure. The code defines a main function that sets up a command-line interface with a global command named "Demo app" and a subcommand called "sub," which requires an argument. The program checks if the subcommand is invoked and, if so, outputs the provided argument to the console. This example is useful for developers looking to implement structured command-line interfaces in their applications using the CLI11 library.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `string`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application with a subcommand that requires an argument and prints the argument if the subcommand is invoked.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI application named 'Demo app'.
    - Add a subcommand named 'sub' to the CLI application with a required argument 'sub_arg'.
    - Parse the command-line arguments using the CLI11 library.
    - Check if the subcommand 'sub' was invoked.
    - If the subcommand was invoked, print the value of 'sub_arg'.
    - Return 0 to indicate successful execution.
- **Output**: The function returns an integer value of 0, indicating successful execution of the program.


