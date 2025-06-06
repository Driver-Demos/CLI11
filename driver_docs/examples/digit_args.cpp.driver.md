# Purpose
This code is a C++ executable that utilizes the CLI11 library to parse command-line arguments, providing narrow functionality focused on setting a compression level through flags. The program defines a [`main`](#main) function, which is the entry point for execution, and uses the CLI11 library to create a command-line application (`CLI::App app`). It sets up a series of flags (`-1` through `-9`) that correspond to integer values (1 through 9) to represent different compression levels, storing the selected value in the `val` variable. The `CLI11_PARSE` macro processes the command-line arguments, and the program outputs the selected compression level to the standard output. This code is intended to be compiled and run as a standalone application, demonstrating basic command-line argument parsing with predefined flag options.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application to parse compression level flags and outputs the selected value.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI::App object named `app`.
    - Declare an integer variable `val` initialized to 0.
    - Add a set of flags to the `app` object, each flag corresponding to a compression level from 1 to 9, with `val` being updated to the respective level when a flag is set.
    - Parse the command-line arguments using `CLI11_PARSE`, which updates `val` based on the flags provided.
    - Output the value of `val` to the standard output.
    - Return 0 to indicate successful execution.
- **Output**: The function outputs the selected compression level value to the standard output.


