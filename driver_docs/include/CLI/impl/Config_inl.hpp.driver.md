# Purpose
This C++ source code file is part of the CLI11 library, which is a command-line interface parser for C++. The file primarily focuses on handling configuration files, specifically in the context of parsing and generating configuration data. It provides functionality to read configuration data from input streams and convert it into a structured format that can be used by the CLI11 library. The code includes functions for parsing configuration sections, handling multiline strings, and managing parent-child relationships within configuration sections. Additionally, it provides utilities for converting command-line arguments into a format suitable for inclusion in configuration files, supporting various data types and formats.

The file is structured around the `CLI` namespace and includes several inline functions within the `detail` namespace, which are used to perform specific tasks such as checking if a string is printable, converting arguments for INI files, and generating parent sections. The `ConfigBase` class provides methods for reading from and writing to configuration files, allowing for the serialization and deserialization of application settings. The code is designed to be included in other parts of the CLI11 library, as indicated by the use of `#pragma once` and the inclusion of necessary headers. Overall, this file is a crucial component of the CLI11 library, enabling the handling of configuration files in a flexible and efficient manner.
# Imports and Dependencies

---
- `../Config.hpp`
- `algorithm`
- `string`
- `utility`
- `vector`


# Functions

---
### is\_printable<!-- {{#callable:CLI::detail::is_printable}} -->
The `is_printable` function checks if all characters in a given string are printable or are newline or tab characters.
- **Inputs**:
    - `test_string`: A constant reference to a `std::string` that is to be checked for printable characters.
- **Control Flow**:
    - The function uses `std::all_of` to iterate over each character in `test_string`.
    - For each character, a lambda function checks if the character is printable using `isprint` after casting it to `unsigned char`, or if it is a newline (`\n`) or tab (`\t`) character.
    - If all characters satisfy the condition, `std::all_of` returns `true`; otherwise, it returns `false`.
- **Output**: A boolean value indicating whether all characters in the input string are printable or are newline or tab characters.


---
### convert\_arg\_for\_ini<!-- {{#callable:CLI::detail::std::string::convert_arg_for_ini}} -->
The `convert_arg_for_ini` function processes a string argument to prepare it for inclusion in an INI file, applying appropriate quoting and escaping based on the content of the argument.
- **Inputs**:
    - `arg`: A string representing the argument to be converted for INI file compatibility.
    - `stringQuote`: A character used to quote strings in the INI file.
    - `literalQuote`: A character used to quote literals in the INI file.
    - `disable_multi_line`: A boolean flag indicating whether multi-line strings should be disabled.
- **Control Flow**:
    - Check if the argument is empty and return a double quote using `stringQuote` if true.
    - Return the argument directly if it matches specific strings like 'true', 'false', 'nan', or 'inf'.
    - Attempt to convert the argument to a floating-point number and return it if it is a valid numeric string.
    - For single-character arguments, return a quoted version using `literalQuote` or handle special cases like non-printable characters and single quotes.
    - Check for hexadecimal, octal, or binary numeric formats and return the argument if valid.
    - If the argument contains non-printable characters, return a binary-escaped version of the string.
    - If the argument contains escapable characters and is long, handle it as a multi-line string if allowed, otherwise return an escaped version using `stringQuote`.
    - Finally, return the argument quoted with `stringQuote` if none of the above conditions are met.
- **Output**: A string that is the processed version of the input argument, ready for inclusion in an INI file.
- **Functions called**:
    - [`CLI::detail::is_printable`](#is_printable)


---
### ini\_join<!-- {{#callable:CLI::detail::std::string::ini_join}} -->
The `ini_join` function concatenates a vector of strings into a single string, formatted according to INI file conventions, with optional array delimiters and quotes.
- **Inputs**:
    - `args`: A vector of strings to be joined.
    - `sepChar`: A character used to separate the joined strings.
    - `arrayStart`: A character used to denote the start of an array, or '\0' if not used.
    - `arrayEnd`: A character used to denote the end of an array, or '\0' if not used.
    - `stringQuote`: A character used to quote strings.
    - `literalQuote`: A character used to quote literals.
- **Control Flow**:
    - Initialize `disable_multi_line` to false and `joined` as an empty string.
    - If `args` has more than one element and `arrayStart` is not '\0', append `arrayStart` to `joined` and set `disable_multi_line` to true.
    - Iterate over each string in `args`, appending `sepChar` and a space to `joined` if it's not the first element and `sepChar` is not a whitespace character.
    - Convert each argument using [`convert_arg_for_ini`](#stringconvert_arg_for_ini) and append the result to `joined`.
    - If `args` has more than one element and `arrayEnd` is not '\0', append `arrayEnd` to `joined`.
    - Return the `joined` string.
- **Output**: A single string that represents the joined and formatted INI-style representation of the input strings.
- **Functions called**:
    - [`CLI::detail::std::string::convert_arg_for_ini`](#stringconvert_arg_for_ini)


---
### generate\_parents<!-- {{#callable:CLI::detail::std::vector<std::string>::generate_parents}} -->
The `generate_parents` function generates a list of parent sections from a given section and name, using a specified separator, and removes any quotes from the resulting parent names.
- **Inputs**:
    - `section`: A constant reference to a string representing the section name, which may contain parent sections separated by the `parentSeparator`.
    - `name`: A reference to a string representing the name, which may also contain parent sections separated by the `parentSeparator`.
    - `parentSeparator`: A character used to separate parent sections within the `section` and `name` strings.
- **Control Flow**:
    - Initialize an empty vector `parents` to store the parent sections.
    - Check if the `section` is not equal to "default" (case-insensitive).
    - If the `section` contains the `parentSeparator`, split the `section` into parts using `parentSeparator` and store them in `parents`; otherwise, add the `section` as a single element to `parents`.
    - Check if the `name` contains the `parentSeparator`.
    - If it does, split the `name` into parts using `parentSeparator`, update `name` to the last part, and insert the other parts into `parents`.
    - Attempt to remove quotes from all elements in `parents` using `detail::remove_quotes`.
    - If an `std::invalid_argument` exception is thrown during quote removal, catch it and throw a `CLI::ParseError` with the exception message and an exit code of `CLI::ExitCodes::InvalidError`.
    - Return the `parents` vector.
- **Output**: A vector of strings representing the parent sections derived from the `section` and `name` inputs, with quotes removed.


---
### checkParentSegments<!-- {{#callable:CLI::detail::checkParentSegments}} -->
The `checkParentSegments` function processes and updates a vector of `ConfigItem` objects by managing parent segments based on a given section and separator.
- **Inputs**:
    - `output`: A reference to a vector of `ConfigItem` objects that will be modified to reflect the parent segments.
    - `currentSection`: A string representing the current section whose parent segments are to be generated and processed.
    - `parentSeparator`: A character used to separate parent segments in the section string.
- **Control Flow**:
    - Generate parent segments from the `currentSection` using the `generate_parents` function.
    - Check if the `output` vector is not empty and the last `ConfigItem` has a name of "--".
    - If the above condition is true, determine the minimum size (`msize`) for parent segments and adjust the `output` vector by popping back parent segments until the size is less than `msize`.
    - If there are more than one parent segment, find the common segments between the last `ConfigItem` in `output` and the generated parents, and adjust the `output` vector accordingly.
    - If the `output` vector is empty or the last `ConfigItem` does not have a name of "--", and there are more than one parent segment, add new `ConfigItem` objects to `output` for each parent segment.
    - Finally, add a new `ConfigItem` to `output` with the generated parents and a name of "++".
- **Output**: The function modifies the `output` vector by adding or adjusting `ConfigItem` objects to reflect the parent segments of the `currentSection`.


---
### hasMLString<!-- {{#callable:CLI::detail::hasMLString}} -->
The `hasMLString` function checks if the last three characters of a given string are the same as a specified character.
- **Inputs**:
    - `fullString`: A constant reference to a `std::string` that represents the string to be checked.
    - `check`: A `char` that represents the character to be checked against the last three characters of `fullString`.
- **Control Flow**:
    - Check if the length of `fullString` is less than 3; if so, return `false`.
    - Create a reverse iterator `it` pointing to the end of `fullString`.
    - Check if the last three characters of `fullString` (pointed by `it`, `it+1`, and `it+2`) are equal to `check`.
    - Return `true` if all three characters match `check`, otherwise return `false`.
- **Output**: A boolean value indicating whether the last three characters of `fullString` are equal to `check`.


---
### find\_matching\_config<!-- {{#callable:CLI::detail::find_matching_config}} -->
The `find_matching_config` function searches for a `ConfigItem` in a vector that matches specified parent strings and a name, with an option for a full search.
- **Inputs**:
    - `items`: A reference to a vector of `ConfigItem` objects to search through.
    - `parents`: A constant reference to a vector of strings representing the parent hierarchy to match.
    - `name`: A constant reference to a string representing the name of the `ConfigItem` to match.
    - `fullSearch`: A boolean indicating whether to perform a full search through the vector or stop at the first match.
- **Control Flow**:
    - Check if the `items` vector is empty; if so, return `items.end()`.
    - Initialize `search` to point to the last element in the `items` vector.
    - Enter a `do-while` loop that continues as long as `fullSearch` is true.
    - In each iteration, check if the current `ConfigItem`'s `parents` and `name` match the given `parents` and `name`.
    - If a match is found, return the current iterator `search`.
    - If `search` is at the beginning of the vector, break the loop.
    - Decrement `search` to move to the previous element.
    - If no match is found after the loop, return `items.end()`.
- **Output**: An iterator to the matching `ConfigItem` in the vector, or `items.end()` if no match is found.


---
### from\_config<!-- {{#callable:CLI::ConfigBase::from_config}} -->
The `from_config` function reads configuration data from an input stream and parses it into a vector of `ConfigItem` objects, handling sections, comments, and various data formats.
- **Inputs**:
    - `input`: An input stream (`std::istream`) from which configuration data is read.
- **Control Flow**:
    - Initialize variables for line processing, section tracking, and configuration item storage.
    - Determine array handling based on configuration settings.
    - Iterate over each line of the input stream, trimming and processing each line.
    - Skip lines that are too short to be meaningful or are comments.
    - Handle multiline comments and values by checking for specific quote patterns and reading until the end of the multiline content.
    - Detect section headers enclosed in brackets and update the current section, inserting section end markers as needed.
    - Parse key-value pairs by finding the delimiter and handling potential multiline values or arrays.
    - Generate parent sections for each configuration item and process quoted strings.
    - Check for duplicate configuration items and merge or append new data as necessary.
    - Insert section end markers for non-default sections at the end of processing.
    - Return the vector of parsed `ConfigItem` objects.
- **Output**: A vector of `ConfigItem` objects representing the parsed configuration data.


---
### clean\_name\_string<!-- {{#callable:CLI::clean_name_string}} -->
The `clean_name_string` function modifies a given string by adding quotes if it contains certain characters or patterns.
- **Inputs**:
    - `name`: A reference to a string that needs to be cleaned or modified.
    - `keyChars`: A string containing characters that, if found in the name, trigger the cleaning process.
- **Control Flow**:
    - Check if the name contains any characters from keyChars, or if it is enclosed in square brackets, or contains any of the characters '"`\.
    - If the name does not contain a single quote, enclose the name with single quotes.
    - If the name contains a single quote, check for escapable characters and add escaped characters if necessary, then enclose the name with double quotes.
- **Output**: Returns a reference to the modified input string.


---
### to\_config<!-- {{#callable:CLI::std::string::to_config}} -->
The `to_config` function generates a configuration string for a given application, including options and subcommands, with optional descriptions and default values.
- **Inputs**:
    - `app`: A pointer to the `App` object representing the application for which the configuration is being generated.
    - `default_also`: A boolean indicating whether default values should be included in the configuration output.
    - `write_description`: A boolean indicating whether descriptions should be included as comments in the configuration output.
    - `prefix`: A string prefix to prepend to each configuration entry name.
- **Control Flow**:
    - Initialize a stringstream `out` and set up comment and key character strings.
    - Retrieve groups from the `app` object and insert 'OPTIONS' at the beginning of the groups vector.
    - Iterate over each group, skipping if the group is 'OPTIONS' and defaults have already been used.
    - For each group, if `write_description` is true, write the group name as a comment.
    - Iterate over each option in the `app` object, processing only configurable options.
    - For each option, check if it belongs to the current group and retrieve its single name and results.
    - If results are empty and `default_also` is true, determine the default value and set `isDefault` flag.
    - If the option has a value, process flag values and write the option description if `write_description` is true.
    - Clean the option name and write the configuration entry to `out`, commenting it if it's a default value and `commentDefaultsBool` is true.
    - Iterate over subcommands of the `app` object, recursively calling `to_config` for each subcommand.
    - Return the configuration string, optionally prepending the application's description as a comment.
- **Output**: A string representing the configuration of the application, including options and subcommands, formatted with optional descriptions and default values.
- **Functions called**:
    - [`CLI::clean_name_string`](#clean_name_string)


