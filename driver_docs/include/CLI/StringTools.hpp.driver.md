# Purpose
This C++ header file is part of the CLI11 library, which is a command-line interface parser for C++. The file provides a collection of utility functions and tools primarily focused on string manipulation and processing, which are essential for parsing and handling command-line arguments. The file includes functions for trimming whitespace, joining and splitting strings, handling quoted strings, and verifying the validity of option names. It also includes functionality for converting enums to and from streams, which is useful for handling enumerated command-line options.

The file is structured into namespaces, with the primary namespace being `CLI`, which contains a sub-namespace `enums` for handling enum streaming. The `detail` namespace contains a variety of helper functions that perform specific string operations, such as trimming, joining, and escaping characters. These functions are designed to be used internally within the CLI11 library to facilitate the parsing and formatting of command-line inputs. The file also includes mechanisms for handling environmental variables and processing binary strings, which are crucial for robust command-line parsing. Overall, this header file provides a focused set of utilities that support the broader functionality of the CLI11 library.
# Imports and Dependencies

---
- `algorithm`
- `iomanip`
- `locale`
- `sstream`
- `stdexcept`
- `string`
- `type_traits`
- `vector`
- `Macros.hpp`
- `impl/StringTools_inl.hpp`


# Functions

---
### operator<<<!-- {{#callable:CLI::enums::operator<<}} -->
The `operator<<` function template provides a way to output enumeration values to an `std::ostream` by converting them to their underlying integer type.
- **Inputs**:
    - `in`: An `std::ostream` object where the enumeration value will be output.
    - `item`: A constant reference to an enumeration value of type `T` to be output.
- **Control Flow**:
    - The function checks if the type `T` is an enumeration using `std::enable_if` and `std::is_enum`.
    - It casts the enumeration value `item` to its underlying integer type using `std::underlying_type`.
    - The casted integer value is then output to the `std::ostream` object `in`.
- **Output**: The function returns a reference to the `std::ostream` object `in` after outputting the enumeration value.


---
### join<!-- {{#callable:CLI::detail::join}} -->
The `join` function concatenates elements of a container into a single string, applying a transformation function to each element and separating them with a specified delimiter.
- **Inputs**:
    - `T`: A container type that holds the elements to be joined.
    - `Callable`: A function or callable object that transforms each element of the container before joining.
    - `delim`: A string delimiter used to separate the transformed elements in the final output string, defaulting to a comma (",").
- **Control Flow**:
    - Initialize an output string stream `s` to build the final string.
    - Obtain iterators `beg` and `end` to the beginning and end of the container `v`.
    - Initialize `loc` to track the position in the stream `s`.
    - Iterate over the container from `beg` to `end`.
    - For each element, check if the current position `nloc` in the stream is greater than `loc`; if so, append the delimiter to the stream and update `loc`.
    - Apply the transformation function `func` to the current element and append the result to the stream.
    - Continue until all elements have been processed.
    - Return the concatenated string from the stream.
- **Output**: A single string containing the transformed elements of the container, separated by the specified delimiter.


---
### rjoin<!-- {{#callable:CLI::detail::rjoin}} -->
The `rjoin` function concatenates elements of a container in reverse order, separated by a specified delimiter, into a single string.
- **Inputs**:
    - `v`: A container (e.g., vector, list) whose elements will be joined into a string.
    - `delim`: A string delimiter used to separate elements in the resulting string; defaults to a comma (",").
- **Control Flow**:
    - Initialize an output string stream `s`.
    - Iterate over the container `v` from the last element to the first.
    - For each element, if it is not the first element being processed, append the delimiter to the stream.
    - Append the current element to the stream.
    - Continue until all elements have been processed in reverse order.
- **Output**: A string representing the concatenated elements of the container in reverse order, separated by the specified delimiter.


---
### trim<!-- {{#callable:CLI::detail::trim}} -->
The `trim` function removes specified characters from both ends of a given string.
- **Inputs**:
    - `str`: A reference to the string that needs to be trimmed.
    - `filter`: A string containing characters to be removed from both ends of the input string.
- **Control Flow**:
    - The function calls [`rtrim`](impl/StringTools_inl.hpp.driver.md#detailrtrim) on the input string `str` with the `filter` to remove specified characters from the right end.
    - The result of [`rtrim`](impl/StringTools_inl.hpp.driver.md#detailrtrim) is then passed to [`ltrim`](impl/StringTools_inl.hpp.driver.md#detailltrim) with the same `filter` to remove specified characters from the left end.
    - The final trimmed string is returned.
- **Output**: A reference to the modified input string `str` with specified characters removed from both ends.
- **Functions called**:
    - [`CLI::detail::ltrim`](impl/StringTools_inl.hpp.driver.md#detailltrim)
    - [`CLI::detail::rtrim`](impl/StringTools_inl.hpp.driver.md#detailrtrim)


---
### trim\_copy<!-- {{#callable:CLI::detail::trim_copy}} -->
The `trim_copy` function creates a trimmed copy of a given string by removing specified characters from both ends.
- **Inputs**:
    - `str`: The original string that needs to be trimmed.
    - `filter`: A string containing characters to be removed from both ends of the original string.
- **Control Flow**:
    - A copy of the input string `str` is created and stored in a local variable `s`.
    - The [`trim`](#detailtrim) function is called with `s` and `filter` as arguments to remove specified characters from both ends of `s`.
    - The trimmed string is returned as the output.
- **Output**: A new string that is a trimmed version of the input string, with specified characters removed from both ends.
- **Functions called**:
    - [`CLI::detail::trim`](#detailtrim)


---
### valid\_first\_char<!-- {{#callable:CLI::detail::valid_first_char}} -->
The `valid_first_char` function checks if a given character is a valid first character for an option by ensuring it is not a hyphen and is greater than the ASCII value of '!'.

- **Inputs**:
    - `c`: A character of any type `T` to be validated as a potential first character for an option.
- **Control Flow**:
    - The function checks if the character `c` is not equal to the hyphen ('-').
    - It then checks if the ASCII value of `c`, when cast to an unsigned char, is greater than 33, which excludes space and '!'.
    - The function returns true if both conditions are met, indicating `c` is a valid first character.
- **Output**: A boolean value indicating whether the character `c` is a valid first character for an option.


---
### valid\_later\_char<!-- {{#callable:CLI::detail::valid_later_char}} -->
The `valid_later_char` function checks if a character is valid for use in option names, excluding certain special characters and control codes.
- **Inputs**:
    - `T c`: A character of any type `T` to be validated.
- **Control Flow**:
    - The function checks if the character `c` is not equal to '=', ':', or '{'.
    - It then checks if the character `c` is either a tab character or has an ASCII value greater than 32, indicating it is not a control character other than a tab.
- **Output**: The function returns a boolean value indicating whether the character is valid (true) or not (false).


---
### valid\_alias\_name\_string<!-- {{#callable:CLI::detail::valid_alias_name_string}} -->
The function `valid_alias_name_string` checks if a given string is a valid alias name by ensuring it does not contain newline or null characters.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that represents the alias name to be validated.
- **Control Flow**:
    - Define a static string `badChars` containing newline and null characters.
    - Use `std::string::find_first_of` to check if any character in `badChars` is present in the input string `str`.
    - Return `true` if none of the characters in `badChars` are found in `str`, otherwise return `false`.
- **Output**: A boolean value indicating whether the input string is a valid alias name (true if valid, false otherwise).


---
### is\_separator<!-- {{#callable:CLI::detail::is_separator}} -->
The `is_separator` function checks if a given string is either empty or equal to the string '%%'.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that is to be checked if it is a separator.
- **Control Flow**:
    - The function defines a static constant string `sep` initialized to '%%'.
    - It returns `true` if the input string `str` is empty or if it is equal to `sep`.
    - Otherwise, it returns `false`.
- **Output**: A boolean value indicating whether the input string is a separator (either empty or '%%').


---
### isalpha<!-- {{#callable:CLI::detail::isalpha}} -->
The `isalpha` function checks if all characters in a given string are alphabetic.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that is to be checked for alphabetic characters.
- **Control Flow**:
    - The function uses `std::all_of` to iterate over each character in the string `str`.
    - For each character, it applies a lambda function that checks if the character is alphabetic using `std::isalpha` with the default locale.
- **Output**: A boolean value indicating whether all characters in the input string are alphabetic (true) or not (false).


---
### to\_lower<!-- {{#callable:CLI::detail::to_lower}} -->
The `to_lower` function converts all characters in a given string to lowercase using the current locale.
- **Inputs**:
    - `str`: A string that will be converted to lowercase.
- **Control Flow**:
    - The function uses `std::transform` to iterate over each character in the input string `str`.
    - For each character, a lambda function is applied that converts the character to lowercase using `std::tolower` with the current locale.
    - The transformation is done in-place, modifying the original string `str`.
- **Output**: A new string with all characters converted to lowercase.


---
### remove\_underscore<!-- {{#callable:CLI::detail::remove_underscore}} -->
The `remove_underscore` function removes all underscore characters from a given string.
- **Inputs**:
    - `str`: A string from which underscores are to be removed.
- **Control Flow**:
    - The function uses `std::remove` to shift all non-underscore characters to the front of the string, effectively removing underscores.
    - The `erase` method is then called to remove the trailing characters that are no longer needed after the `remove` operation.
    - Finally, the modified string is returned.
- **Output**: A string with all underscore characters removed.


---
### has\_default\_flag\_values<!-- {{#callable:CLI::detail::has_default_flag_values}} -->
The function `has_default_flag_values` checks if a given string contains specific characters that indicate default flag values.
- **Inputs**:
    - `flags`: A constant reference to a `std::string` that represents the flags to be checked for default values.
- **Control Flow**:
    - The function uses `std::string::find_first_of` to search for the first occurrence of either '{' or '!' in the input string `flags`.
    - If either character is found, the function returns `true`; otherwise, it returns `false`.
- **Output**: A boolean value indicating whether the input string contains the characters '{' or '!', which are used to denote default flag values.


---
### find\_and\_modify<!-- {{#callable:CLI::detail::find_and_modify}} -->
The `find_and_modify` function searches for occurrences of a trigger string within a given string and applies a modification function to each occurrence, returning the modified string.
- **Inputs**:
    - `str`: The input string in which to search for the trigger string.
    - `trigger`: The substring to search for within the input string.
    - `modify`: A callable function that takes the input string and the starting position of the trigger, modifies the string, and returns the new position to continue searching from.
- **Control Flow**:
    - Initialize `start_pos` to 0 to begin searching from the start of the string.
    - Enter a while loop that continues as long as the trigger string is found in the input string starting from `start_pos`.
    - Within the loop, call the `modify` function with the current string and the position of the trigger, updating `start_pos` with the return value of `modify`.
    - Exit the loop when no more occurrences of the trigger string are found.
- **Output**: The function returns the modified string after all occurrences of the trigger string have been processed by the `modify` function.


