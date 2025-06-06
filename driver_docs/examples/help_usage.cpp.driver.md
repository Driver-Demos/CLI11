# Purpose
This C++ source code file is an executable program that utilizes the CLI11 library to create a command-line interface (CLI) application. The primary purpose of this application is to provide encoding and decoding functionalities through subcommands. The code defines two main subcommands: "encode" and "decode," each requiring an input and output file, with the "encode" subcommand offering additional options such as specifying an encoding level, removing the input file after processing, and a suboption flag. The application enforces the existence of the input file and allows for case-insensitive subcommand recognition, enhancing user convenience.

The code is structured to ensure that at least one subcommand is required, and it customizes the usage message to guide users on how to execute the program correctly. The CLI11 library is leveraged to handle command-line argument parsing, option validation, and help message generation. The application sets a custom help flag to display comprehensive help information, ensuring users can easily access guidance on using the program. This file is a standalone executable, not intended to be imported as a library, and it does not define public APIs or external interfaces beyond the command-line interface it provides.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `string`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function sets up a command-line interface using the CLI11 library to handle encoding and decoding operations with specified options and flags.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize variables for input and output file names, encoding level, and suboption flag.
    - Create a CLI11 application object with a caption 'CLI11 help'.
    - Require exactly one subcommand to be specified by the user.
    - Add an 'encode' subcommand with options for input file, output file, encoding level, and flags for removing the input file and a suboption.
    - Add a 'decode' subcommand with options for input file and output file.
    - Customize the usage message to show the correct command format.
    - Set flags for displaying help messages, including a full help message flag.
    - Parse the command-line arguments using CLI11's parsing function.
- **Output**: The function returns an integer value of 0, indicating successful execution.


