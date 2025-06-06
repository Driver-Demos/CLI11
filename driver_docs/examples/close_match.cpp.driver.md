# Purpose
This C++ source code file is designed to demonstrate the implementation of close match detection for command-line subcommands using the CLI11 library. The primary functionality of this code is to enhance user experience by providing suggestions for mistyped subcommands based on their Levenshtein distance, a metric for measuring the difference between two sequences. The code defines a function [`levenshteinDistance`](#levenshteinDistance) to calculate this distance between two strings, and another function [`findClosestMatch`](#findClosestMatch) to identify the closest matching string from a list of candidates. These functions are utilized in the [`addSubcommandCloseMatchDetection`](#addSubcommandCloseMatchDetection) function, which integrates this logic into a CLI11 application by setting up a callback that checks for unmatched commands and suggests the closest valid subcommand.

The file includes a [`main`](#main) function that sets up a simple command-line application using CLI11, with options and subcommands such as "install," "upgrade," "remove," and "test." The application is configured to allow prefix matching and to detect close matches for subcommands, providing feedback to the user when an invalid command is entered. This code is a practical example of how to implement user-friendly command-line interfaces by leveraging string matching techniques to guide users towards correct command usage, thus reducing errors and improving usability.
# Imports and Dependencies

---
- `algorithm`
- `iostream`
- `numeric`
- `string`
- `utility`
- `vector`
- `CLI/CLI.hpp`


# Functions

---
### levenshteinDistance<!-- {{#callable:levenshteinDistance}} -->
The `levenshteinDistance` function calculates the Levenshtein distance between two strings, which is a measure of the minimum number of single-character edits required to change one string into the other.
- **Inputs**:
    - `s1`: The first input string for which the Levenshtein distance is to be calculated.
    - `s2`: The second input string for which the Levenshtein distance is to be calculated.
- **Control Flow**:
    - Initialize the lengths of the input strings `s1` and `s2` as `len1` and `len2`, respectively.
    - Check if either string is empty; if so, return the length of the other string as the distance.
    - Initialize two vectors, `prev` and `curr`, to store the distances for the previous and current rows of the dynamic programming table, respectively.
    - Fill the `prev` vector with values from 0 to `len2`, representing the initial state of the distance calculation.
    - Iterate over each character in `s1` (outer loop) and `s2` (inner loop) to compute the cost of substitution, insertion, and deletion.
    - For each pair of characters, calculate the minimum cost of transforming the substring of `s1` to the substring of `s2` using the dynamic programming approach.
    - Swap the `prev` and `curr` vectors efficiently using `std::exchange` after processing each character of `s1`.
- **Output**: The function returns the Levenshtein distance as a `std::size_t`, representing the minimum number of single-character edits needed to transform `s1` into `s2`.


---
### findClosestMatch<!-- {{#callable:findClosestMatch}} -->
The `findClosestMatch` function identifies the string from a list of candidates that has the smallest Levenshtein distance to a given input string.
- **Inputs**:
    - `input`: A reference to a constant string representing the input string for which the closest match is to be found.
    - `candidates`: A reference to a constant vector of strings representing the list of candidate strings to compare against the input string.
- **Control Flow**:
    - Initialize an empty string `closest` and set `minDistance` to the maximum possible size of a string (`std::string::npos`).
    - Iterate over each string `candidate` in the `candidates` vector.
    - For each `candidate`, calculate the Levenshtein distance to the `input` string using the [`levenshteinDistance`](#levenshteinDistance) function.
    - If the calculated distance is less than `minDistance`, update `minDistance` with this distance and set `closest` to the current `candidate`.
    - After iterating through all candidates, return a pair containing the `closest` string and the `minDistance`.
- **Output**: A `std::pair` consisting of the closest matching string from the candidates and the corresponding Levenshtein distance to the input string.
- **Functions called**:
    - [`levenshteinDistance`](#levenshteinDistance)


---
### addSubcommandCloseMatchDetection<!-- {{#callable:addSubcommandCloseMatchDetection}} -->
The function `addSubcommandCloseMatchDetection` adds a callback to a CLI application to detect and suggest corrections for unmatched subcommands based on a specified minimum Levenshtein distance.
- **Inputs**:
    - `app`: A pointer to a `CLI::App` object representing the command-line application to which the close match detection will be added.
    - `minDistance`: An optional size_t parameter specifying the maximum Levenshtein distance for suggesting a close match, defaulting to 3.
- **Control Flow**:
    - The function enables the allowance of extra arguments in the CLI application by calling `app->allow_extras(true);`.
    - It retrieves all subcommands of the application using `app->get_subcommands(nullptr);` and stores their names and aliases in a list called `list`.
    - A callback is added to the application using `app->parse_complete_callback`, which iterates over any remaining arguments after parsing.
    - For each remaining argument, if it is not empty and does not start with a '-', the function finds the closest match from the list of subcommands using [`findClosestMatch`](#findClosestMatch).
    - If the closest match's distance is less than or equal to `minDistance`, a message is printed to the console suggesting the closest match for the unmatched command.
- **Output**: The function does not return a value; it modifies the behavior of the `CLI::App` object by adding a callback for unmatched subcommand detection.
- **Functions called**:
    - [`findClosestMatch`](#findClosestMatch)


---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application with prefix and close string matching capabilities for subcommands, parses the input arguments, and outputs the names of the matched subcommands.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize an integer variable `value` to 0.
    - Create a `CLI::App` object named `app` with a description for testing prefix and close string matching.
    - Enable prefix matching for subcommands using `app.allow_subcommand_prefix_matching()`.
    - Add an option `-v` to the app to set the `value` variable.
    - Add subcommands 'install', 'upgrade', 'remove', and 'test' to the app.
    - Enable close matching for subcommands by calling [`addSubcommandCloseMatchDetection`](#addSubcommandCloseMatchDetection) with a minimum distance of 5.
    - Parse the command-line arguments using `CLI11_PARSE(app, argc, argv)`.
    - Retrieve the list of matched subcommands using `app.get_subcommands()`.
    - Iterate over the matched subcommands and print their names to the standard output.
- **Output**: The function returns an integer value of 0, indicating successful execution.
- **Functions called**:
    - [`addSubcommandCloseMatchDetection`](#addSubcommandCloseMatchDetection)


