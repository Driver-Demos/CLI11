# Purpose
This C++ source code file is an executable program designed to demonstrate the handling of command-line arguments using the CLI11 library. The primary functionality of the program is to accept unlimited arguments for two options, `--foo` (or `-f`) and `--bar`, and to maintain the original order of these arguments as they were input. The program utilizes the CLI11 library to define and parse these command-line options, allowing users to input multiple integer values for each option. Additionally, the program includes a flag option `--z` (or `--x`) to showcase the handling of flags, although it does not store or process these flags further.

The technical components of the program include the use of vectors to store the integer arguments for each option and the use of the `std::reverse` function to reverse these vectors after parsing. This reversal is necessary to maintain the original input order when the arguments are later processed. The program iterates over the parsed options in the order they were provided, pairing each option with its corresponding integer value and storing these pairs in a vector of string-integer pairs. Finally, the program outputs these pairs to the console, demonstrating that the original order of arguments has been preserved. This code serves as a practical example of using CLI11 for command-line parsing and managing argument order in C++.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `algorithm`
- `iostream`
- `string`
- `tuple`
- `vector`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line application that accepts unlimited `--foo` and `--bar` arguments, processes them to maintain their original order, and outputs them in the order they were parsed.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI application with a description.
    - Add options `--foo` and `--bar` to the application, storing their values in `foos` and `bars` vectors respectively.
    - Add flags `--z` and `--x` to the application.
    - Parse the command-line arguments using the `app.parse` method, handling any `CLI::ParseError` exceptions by exiting the application with an error code.
    - Reverse the order of the `foos` and `bars` vectors to facilitate popping from the back while maintaining the original order of input.
    - Iterate over the parsed options in the order they were provided, adding each to a `keyval` vector as a pair of the option name and its last value, then removing that value from the vector.
    - Output each key-value pair in the `keyval` vector to the standard output.
- **Output**: The function outputs the parsed `--foo` and `--bar` arguments in the order they were provided, each prefixed by their respective option name.


