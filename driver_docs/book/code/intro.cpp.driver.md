# Purpose
This code is a simple C++ executable that utilizes the CLI11 library to parse command-line arguments. It provides narrow functionality, specifically designed to handle a single integer parameter passed with the `-p` option. The code defines a [`main`](#main) function, which is the entry point of the program, and sets up a command-line interface application with a brief description. It then adds an option for a parameter `p`, which is parsed from the command line using the `CLI11_PARSE` macro. Finally, it outputs the value of the parameter to the standard output, demonstrating basic command-line argument handling.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application, parses command-line arguments to set a parameter, and outputs the parameter value.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI::App object with a description.
    - Define an integer option '-p' with a default value of 0 and associate it with the variable 'p'.
    - Parse the command-line arguments using CLI11_PARSE macro, which updates 'p' if '-p' is provided.
    - Output the value of 'p' to the standard output.
    - Return 0 to indicate successful execution.
- **Output**: The function returns an integer value of 0, indicating successful execution.


