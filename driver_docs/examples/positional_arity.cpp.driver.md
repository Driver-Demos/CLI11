# Purpose
This C++ source code file is an executable program designed to parse command-line arguments using the CLI11 library. The primary purpose of the code is to demonstrate the handling of positional arguments with varying arity, specifically focusing on two groups of options: numbers and files. The program defines a command-line application named "test for positional arity" and sets up two option groups. The "numbers" group includes two optional integer arguments, `num1` and `num2`, while the "files" group includes two string arguments, `file1` and `file2`, with `file1` being mandatory.

A notable feature of this code is the use of a pre-parse callback function that dynamically enables or disables the "numbers" group based on the number of arguments provided. If the number of arguments is two or fewer, the "numbers" group is disabled, otherwise, it is enabled. This functionality allows the program to adapt its behavior based on the input, showcasing the flexibility of the CLI11 library in managing command-line interfaces. The program outputs the values of the parsed arguments, demonstrating how the input is processed and utilized within the application.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `string`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function sets up a command-line interface to parse and handle options for numbers and files, with conditional logic to enable or disable the numbers group based on the number of arguments provided.
- **Inputs**:
    - `argc`: The count of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI application with a description 'test for positional arity'.
    - Create two option groups: 'numbers' for numerical inputs and 'files' for file inputs.
    - Add options 'num1' and 'num2' to the 'numbers' group, initializing them to -1.
    - Add options 'file1' and 'file2' to the 'files' group, with 'file1' being required.
    - Set a pre-parse callback to disable the 'numbers' group if the number of arguments is 2 or less, otherwise enable it.
    - Parse the command-line arguments using `CLI11_PARSE`.
    - If 'num1' is not -1, print its value.
    - If 'num2' is not -1, print its value.
    - Always print the value of 'file1'.
    - If 'file2' is not empty, print its value.
    - Return 0 to indicate successful execution.
- **Output**: The function returns an integer 0, indicating successful execution of the program.


