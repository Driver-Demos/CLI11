# Purpose
This C++ header file is part of the CLI11 library, which is designed to facilitate command-line interface (CLI) parsing. The file primarily focuses on the internal implementation details of parsing and handling command-line arguments. It defines several inline functions within the `CLI::detail` namespace, which are used to split and validate command-line argument strings. These functions include [`split_short`](#detailsplit_short), [`split_long`](#detailsplit_long), and [`split_windows_style`](#detailsplit_windows_style), which handle different styles of command-line options (e.g., Unix-style short and long options, and Windows-style options). Additionally, the file provides utility functions like [`split_names`](#string>split_names) and [`get_default_flag_values`](#string>>get_default_flag_values) to process and extract flag names and their default values from input strings.

The file is structured to be included in other parts of the CLI11 library, as indicated by the use of `#pragma once` for include guards and the `IWYU pragma` for managing include dependencies. It does not define a public API directly but rather supports the internal workings of the library by providing essential parsing logic. The functions are marked as `CLI11_INLINE`, suggesting they are intended for efficient, inline execution. The file also includes error handling through custom exceptions like `BadNameString`, which are thrown when invalid argument names are encountered. Overall, this file is a specialized component of the CLI11 library, focusing on the parsing and validation of command-line argument names and values.
# Imports and Dependencies

---
- `../Split.hpp`
- `string`
- `tuple`
- `utility`
- `vector`
- `../Error.hpp`
- `../StringTools.hpp`


# Functions

---
### split\_short<!-- {{#callable:CLI::detail::split_short}} -->
The `split_short` function parses a short command-line option from a string, extracting the option name and any remaining characters.
- **Inputs**:
    - `current`: A reference to a constant string representing the command-line argument to be parsed.
    - `name`: A reference to a string where the extracted option name will be stored.
    - `rest`: A reference to a string where the remaining characters after the option name will be stored.
- **Control Flow**:
    - Check if the input string `current` has more than one character, starts with a '-', and the second character is a valid first character for an option.
    - If the above condition is true, extract the second character as the option name and store it in `name`.
    - Store the remaining characters after the option name in `rest`.
    - Return true if the parsing was successful, otherwise return false.
- **Output**: A boolean value indicating whether the parsing was successful (true) or not (false).


---
### split\_long<!-- {{#callable:CLI::detail::split_long}} -->
The `split_long` function parses a string representing a long command-line option, extracting the option name and its associated value if present.
- **Inputs**:
    - `current`: A string representing the current command-line argument, expected to be a long option starting with '--'.
    - `name`: A reference to a string where the extracted option name will be stored.
    - `value`: A reference to a string where the extracted option value will be stored, if present.
- **Control Flow**:
    - Check if the input string `current` is longer than 2 characters, starts with '--', and has a valid character following '--'.
    - Find the position of the first '=' character in `current`.
    - If '=' is found, extract the substring before '=' as the option name and the substring after '=' as the option value.
    - If '=' is not found, extract the substring after '--' as the option name and set the option value to an empty string.
    - Return true if the input string is a valid long option, otherwise return false.
- **Output**: A boolean value indicating whether the input string was successfully parsed as a long option.


---
### split\_windows\_style<!-- {{#callable:CLI::detail::split_windows_style}} -->
The `split_windows_style` function parses a Windows-style command-line argument, extracting the option name and its associated value if present.
- **Inputs**:
    - `current`: A string representing the current command-line argument to be parsed, expected to be in Windows-style format (e.g., '/option:value').
    - `name`: A reference to a string where the extracted option name will be stored.
    - `value`: A reference to a string where the extracted option value will be stored, if present.
- **Control Flow**:
    - Check if the input string `current` is longer than one character, starts with a '/', and the second character is a valid first character for an option name.
    - Find the position of the first ':' character in `current`.
    - If a ':' is found, extract the substring between the '/' and ':' as the option name and the substring after ':' as the option value.
    - If no ':' is found, extract the substring after '/' as the option name and set the option value to an empty string.
    - Return true if the input string is successfully parsed as a Windows-style option, otherwise return false.
- **Output**: A boolean value indicating whether the input string was successfully parsed as a Windows-style option.


---
### split\_names<!-- {{#callable:CLI::detail::std::vector<std::string>::split_names}} -->
The `split_names` function splits a comma-separated string into a vector of trimmed strings.
- **Inputs**:
    - `current`: A string containing names separated by commas.
- **Control Flow**:
    - Initialize an empty vector `output` to store the split names.
    - Initialize a size_t variable `val` to 0 for tracking the position of commas.
    - Enter a while loop that continues as long as a comma is found in `current`.
    - In each iteration, find the position of the first comma in `current` and store it in `val`.
    - Extract the substring from the start to the position of the comma, trim it, and add it to `output`.
    - Update `current` to the substring starting just after the comma.
    - After the loop, add the last remaining trimmed substring of `current` to `output`.
- **Output**: A vector of strings, each representing a trimmed name from the input string.


---
### get\_default\_flag\_values<!-- {{#callable:CLI::detail::std::vector<std::pair<std::string, std::string>>::get_default_flag_values}} -->
The function `get_default_flag_values` parses a string of flag definitions and extracts flag names with their default values.
- **Inputs**:
    - `str`: A string containing flag definitions, where each flag may have a default value enclosed in curly braces or be prefixed with an exclamation mark.
- **Control Flow**:
    - The input string is split into individual flag definitions using the [`split_names`](#string>split_names) function.
    - Flags that are empty or do not have a default value enclosed in curly braces or prefixed with an exclamation mark are removed.
    - For each remaining flag, the default value is extracted if it is enclosed in curly braces; otherwise, it defaults to 'false'.
    - The flag name is cleaned by removing leading dashes or exclamation marks.
    - Each flag name and its default value are stored as a pair in the output vector.
- **Output**: A vector of pairs, where each pair consists of a flag name and its corresponding default value.
- **Functions called**:
    - [`CLI::detail::std::vector<std::string>::split_names`](#string>split_names)


---
### get\_names<!-- {{#callable:CLI::detail::std::tuple<std::vector<std::string>, std::vector<std::string>, std::string>::get_names}} -->
The `get_names` function processes a list of input strings to categorize them into short names, long names, and a positional name, while handling various naming conventions and errors.
- **Inputs**:
    - `input`: A vector of strings representing the names to be processed.
    - `allow_non_standard`: A boolean flag indicating whether non-standard naming conventions are allowed.
- **Control Flow**:
    - Initialize empty vectors for short names and long names, and an empty string for the positional name.
    - Iterate over each name in the input vector.
    - Skip empty names.
    - For names starting with a single dash ('-'), check if they are valid short names or handle them based on the `allow_non_standard` flag, throwing exceptions for invalid cases.
    - For names starting with double dashes ('--'), validate and add them to the long names vector or throw an exception if invalid.
    - Throw exceptions for reserved names like '-', '--', or '++'.
    - For other names, ensure only one positional name is set and validate it, throwing exceptions for invalid or multiple positional names.
    - Return a tuple containing the vectors of short names, long names, and the positional name.
- **Output**: A tuple containing a vector of short names, a vector of long names, and a string for the positional name.


