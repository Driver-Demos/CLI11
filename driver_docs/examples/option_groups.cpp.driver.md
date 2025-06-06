# Purpose
This C++ source code file is an executable program designed to handle command-line arguments for specifying data output formats and targets. It utilizes the CLI11 library to facilitate command-line interface creation, allowing users to specify how and where data should be outputted. The program defines two main option groups: "output_format" and "output target." The "output_format" group allows users to choose between CSV, human-readable text, or binary formats, ensuring that exactly one format is selected. The "output target" group provides options to specify either a file location or a network address for the output, with the constraint that at most one target option can be selected. The program then processes these options and outputs the selected format and target to the console.

The code is structured to provide a clear and user-friendly command-line interface for data output specification, making it suitable for applications where flexible data output configurations are required. The use of CLI11 simplifies the parsing and validation of command-line arguments, ensuring that users provide valid input. The program's main function is to parse the command-line arguments, determine the desired output format and target, and then print the selected configuration to the console. This functionality is narrow in scope, focusing specifically on output configuration, and does not define any public APIs or external interfaces beyond the command-line options it provides.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `string`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function configures and parses command-line options to specify the output format and target location, then displays the selected options.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI application with a description and help flag using the CLI11 library.
    - Create option groups for output format and target location.
    - Add flags for CSV, human-readable, and binary output formats, requiring exactly one to be selected.
    - Add options for file location and network address as output targets, allowing at most one to be selected.
    - Parse the command-line arguments using CLI11's parsing function.
    - Determine the selected output format based on the flags set and print the selection.
    - Check if a file location or network address is specified and print the corresponding output target, defaulting to standard output if none is specified.
    - Return 0 to indicate successful execution.
- **Output**: The function outputs the selected format and target location for the data, either to a file, network address, or standard output.


