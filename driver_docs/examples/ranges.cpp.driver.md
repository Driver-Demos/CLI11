# Purpose
This C++ source code file is an executable program designed to demonstrate the use of exclusionary option groups using the CLI11 library. The primary functionality of the code is to parse command-line arguments to configure a range with minimum, maximum, and step values. The program utilizes the CLI11 library to define command-line options and option groups, allowing users to specify a range either through a single `--range` option or through individual `--min`, `--max`, and `--step` options. The code ensures that at least one option is provided by requiring a minimum of one option to be specified.

The main technical components include the use of the CLI11 library to handle command-line argument parsing and the use of option groups to logically group related options. The program defines a public interface for users to interact with via command-line options, making it a useful tool for scenarios where users need to specify numerical ranges with flexibility. The code is structured to handle different input scenarios, adjusting the range parameters based on the number of arguments provided. The output is a formatted string that displays the configured range, demonstrating the effective use of the CLI11 library for command-line parsing in C++.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `vector`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application to demonstrate exclusionary option groups, processes input arguments to set range parameters, and outputs the configured range.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of character pointers listing all the arguments.
- **Control Flow**:
    - Initialize a CLI application with a description.
    - Add an option `--range` or `-R` to accept a vector of integers, expecting up to two values.
    - Create an option group `min_max_step` to set `min`, `max`, and `step` values, marking `min` and `max` as required options.
    - Require at least one option to be specified by the user.
    - Parse the command-line arguments using `CLI11_PARSE`.
    - Check if the `range` vector is not empty and adjust `min`, `max`, and `step` based on the size of `range`.
    - Output the configured range in the format `[min:step:max]`.
- **Output**: The function outputs the configured range in the format `[min:step:max]` to the standard output.


