# Purpose
This C++ source code file is part of the CLI11 library, which is a command-line interface parser for C++. The file provides a collection of utility functions within the `CLI::detail` namespace, focusing on string manipulation and processing. These functions include operations such as splitting strings, trimming whitespace, removing quotes, handling escape sequences, and formatting output. The file is structured to support the broader functionality of the CLI11 library by offering detailed string handling capabilities, which are essential for parsing and interpreting command-line arguments effectively.

The code is not intended to be an executable on its own but rather serves as a utility component within the CLI11 library. It includes a variety of inline functions that are likely used internally by other parts of the library to ensure efficient and accurate processing of command-line inputs. The functions handle complex string operations, such as managing escape sequences and binary strings, which are crucial for robust command-line parsing. The file does not define public APIs or external interfaces directly but provides foundational support for the library's public-facing components.
# Imports and Dependencies

---
- `../StringTools.hpp`
- `cstdint`
- `string`
- `utility`
- `vector`


# Functions

---
### split<!-- {{#callable:CLI::detail::std::vector<std::string>::split}} -->
The `split` function divides a given string into a vector of substrings based on a specified delimiter character.
- **Inputs**:
    - `s`: A constant reference to the input string that needs to be split.
    - `delim`: A character that serves as the delimiter to split the string.
- **Control Flow**:
    - Initialize an empty vector of strings named `elems` to store the resulting substrings.
    - Check if the input string `s` is empty; if so, add an empty string to `elems` and return it.
    - If the string is not empty, create a stringstream `ss` and set its content to the input string `s`.
    - Use a while loop to read substrings from the stringstream `ss` using the specified delimiter `delim`.
    - For each substring extracted, add it to the `elems` vector.
    - Return the `elems` vector containing the split substrings.
- **Output**: A vector of strings containing the substrings obtained by splitting the input string `s` using the delimiter `delim`.


---
### ltrim<!-- {{#callable:CLI::detail::ltrim}} -->
The `ltrim` function removes leading characters from a string that are present in a specified filter string.
- **Inputs**:
    - `str`: A reference to the string from which leading characters will be removed.
    - `filter`: A string containing characters to be removed from the beginning of the input string.
- **Control Flow**:
    - The function uses `std::find_if` to locate the first character in `str` that is not present in `filter`.
    - It then erases all characters from the beginning of `str` up to the found character.
    - Finally, it returns the modified `str`.
- **Output**: A reference to the modified input string `str` with leading characters removed.


---
### rtrim<!-- {{#callable:CLI::detail::rtrim}} -->
The `rtrim` function removes trailing characters from a string that are present in a specified filter string.
- **Inputs**:
    - `str`: A reference to the string from which trailing characters will be removed.
    - `filter`: A string containing characters to be removed from the end of the input string.
- **Control Flow**:
    - The function uses `std::find_if` with a reverse iterator to locate the first character from the end of the string that is not in the filter string.
    - The lambda function checks if a character is not found in the filter string using `filter.find(ch) == std::string::npos`.
    - The `erase` method is called on the string to remove all characters from the found position to the end of the string.
- **Output**: A reference to the modified input string with trailing characters removed.


---
### remove\_quotes<!-- {{#callable:CLI::detail::remove_quotes}} -->
The [`remove_quotes`](#remove_quotes) function iterates over a vector of strings, removing surrounding quotes and escaped characters from each string.
- **Inputs**:
    - `args`: A reference to a vector of strings, where each string may have surrounding quotes and escaped characters to be removed.
- **Control Flow**:
    - Iterate over each string in the vector `args`.
    - For each string, check if it starts and ends with a double quote ('"').
    - If it does, call [`remove_quotes`](#remove_quotes) on the string to remove the quotes, then call [`remove_escaped_characters`](#stringremove_escaped_characters) to remove any escaped characters.
    - If it does not start and end with a double quote, simply call [`remove_quotes`](#remove_quotes) on the string.
- **Output**: The function modifies the input vector `args` in place, removing quotes and escaped characters from each string.
- **Functions called**:
    - [`CLI::detail::remove_quotes`](#remove_quotes)
    - [`CLI::detail::std::string::remove_escaped_characters`](#stringremove_escaped_characters)


---
### remove\_outer<!-- {{#callable:CLI::detail::remove_outer}} -->
The `remove_outer` function removes matching outer characters from a string if they are equal to a specified key character.
- **Inputs**:
    - `str`: A reference to a string from which the outer characters will be removed.
    - `key`: A character that specifies the outer character to be removed if it matches both the first and last character of the string.
- **Control Flow**:
    - Check if the string length is greater than 1 and the first character matches the key.
    - If the first and last characters of the string are the same, remove the last character using `pop_back()`.
    - Erase the first character of the string using `erase()`.
- **Output**: Returns a reference to the modified string with the outer characters removed if they matched the key.


---
### fix\_newlines<!-- {{#callable:CLI::detail::std::string::fix_newlines}} -->
The `fix_newlines` function inserts a specified leader string after every newline character in the input string.
- **Inputs**:
    - `leader`: A constant reference to a string that will be inserted after each newline character in the input string.
    - `input`: A string in which newline characters will be identified and followed by the leader string.
- **Control Flow**:
    - Initialize a size_type variable `n` to 0 to track the position in the input string.
    - Enter a while loop that continues as long as `n` is not `npos` and is less than the size of the input string.
    - Within the loop, use `find_first_of` to locate the first occurrence of either '\r' or '\n' starting from position `n`.
    - If a newline character is found, modify the input string by inserting the leader string immediately after the newline character.
    - Update `n` to the position after the inserted leader string to continue searching for further newline characters.
- **Output**: Returns the modified input string with the leader string inserted after each newline character.


---
### format\_aliases<!-- {{#callable:CLI::detail::format_aliases}} -->
The `format_aliases` function formats and outputs a list of alias strings to a given output stream with a specified width for alignment.
- **Inputs**:
    - `out`: An output stream (std::ostream) where the formatted aliases will be written.
    - `aliases`: A vector of strings containing the aliases to be formatted and output.
    - `wid`: A size_t value representing the width for alignment of the alias output.
- **Control Flow**:
    - Check if the aliases vector is not empty.
    - If not empty, write 'aliases: ' to the output stream, aligned to the specified width.
    - Iterate over each alias in the aliases vector.
    - For each alias, if it is not the first, prepend a comma and space before writing it to the output stream.
    - Use the `fix_newlines` function to handle newlines in each alias, ensuring proper alignment.
    - After processing all aliases, write a newline character to the output stream.
- **Output**: Returns the modified output stream (std::ostream) with the formatted aliases.


---
### valid\_name\_string<!-- {{#callable:CLI::detail::valid_name_string}} -->
The `valid_name_string` function checks if a given string is a valid name by ensuring it starts with a valid character and all subsequent characters are also valid.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that represents the name to be validated.
- **Control Flow**:
    - Check if the input string `str` is empty or if the first character is not valid using `valid_first_char`; if either condition is true, return `false`.
    - Iterate over each character in the string starting from the second character to the end.
    - For each character, check if it is valid using `valid_later_char`; if any character is invalid, return `false`.
    - If all characters are valid, return `true`.
- **Output**: A boolean value indicating whether the input string is a valid name (`true` if valid, `false` otherwise).


---
### get\_group\_separators<!-- {{#callable:CLI::detail::std::string::get_group_separators}} -->
The `get_group_separators` function returns a string containing default group separators and optionally includes the locale-specific thousands separator if RTTI is enabled.
- **Inputs**: None
- **Control Flow**:
    - Initialize a string `separators` with default group separators "_'".
    - Check if RTTI (Run-Time Type Information) is enabled using the preprocessor directive `#if CLI11_HAS_RTTI != 0`.
    - If RTTI is enabled, retrieve the locale-specific thousands separator using `std::use_facet<std::numpunct<char>>(std::locale()).thousands_sep()` and append it to the `separators` string.
    - Return the `separators` string.
- **Output**: A string containing the default group separators and possibly the locale-specific thousands separator.


---
### find\_and\_replace<!-- {{#callable:CLI::detail::std::string::find_and_replace}} -->
The `find_and_replace` function searches for all occurrences of a substring within a string and replaces them with another substring.
- **Inputs**:
    - `str`: The original string in which the search and replace operation will be performed.
    - `from`: The substring to search for within the original string.
    - `to`: The substring to replace each occurrence of the 'from' substring with.
- **Control Flow**:
    - Initialize `start_pos` to 0 to track the position in the string where the search begins.
    - Enter a while loop that continues as long as `str.find(from, start_pos)` does not return `std::string::npos`, indicating that the substring 'from' is found.
    - Within the loop, replace the substring 'from' at the found position with the substring 'to'.
    - Update `start_pos` to the position immediately after the newly replaced substring to continue searching for further occurrences.
    - Exit the loop when no more occurrences of 'from' are found.
- **Output**: Returns a new string with all occurrences of the 'from' substring replaced by the 'to' substring.


---
### remove\_default\_flag\_values<!-- {{#callable:CLI::detail::remove_default_flag_values}} -->
The `remove_default_flag_values` function removes default flag values enclosed in curly braces and exclamation marks from a given string of flags.
- **Inputs**:
    - `flags`: A reference to a string containing flag definitions, potentially with default values enclosed in curly braces and exclamation marks.
- **Control Flow**:
    - Find the first occurrence of '{' in the string starting from the third character.
    - While a '{' is found, locate the next '}' or ',' after the '{'.
    - If a '}' is found, erase the substring from '{' to '}' inclusive.
    - Continue searching for the next '{' after the current position.
    - After processing all curly braces, remove all '!' characters from the string.
- **Output**: The function modifies the input string in place, removing specified default flag values and exclamation marks.


---
### find\_member<!-- {{#callable:CLI::detail::std::ptrdiff_t::find_member}} -->
The `find_member` function searches for a string in a vector of strings, with optional case and underscore insensitivity, and returns the index of the found string or -1 if not found.
- **Inputs**:
    - `name`: A string representing the name to search for in the vector.
    - `names`: A vector of strings in which to search for the name.
    - `ignore_case`: A boolean flag indicating whether to ignore case when comparing strings.
    - `ignore_underscore`: A boolean flag indicating whether to ignore underscores when comparing strings.
- **Control Flow**:
    - Initialize an iterator `it` to the end of the `names` vector.
    - Check if `ignore_case` is true; if so, further check if `ignore_underscore` is true.
    - If both `ignore_case` and `ignore_underscore` are true, convert `name` to lowercase and remove underscores, then search for a matching string in `names` using the same transformations.
    - If only `ignore_case` is true, convert `name` to lowercase and search for a matching string in `names` using the same transformation.
    - If only `ignore_underscore` is true, remove underscores from `name` and search for a matching string in `names` using the same transformation.
    - If neither `ignore_case` nor `ignore_underscore` is true, search for `name` directly in `names`.
    - Return the index of the found string if `it` is not at the end of `names`, otherwise return -1.
- **Output**: The function returns a `std::ptrdiff_t` which is the index of the found string in the vector, or -1 if the string is not found.


---
### has\_escapable\_character<!-- {{#callable:CLI::detail::has_escapable_character}} -->
The function `has_escapable_character` checks if a given string contains any characters that are considered escapable.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that is to be checked for escapable characters.
- **Control Flow**:
    - The function uses `std::string::find_first_of` to search for any character in the input string `str` that matches any character in the predefined string `escapedChars`.
    - If such a character is found, `std::string::find_first_of` returns the position of the first occurrence, otherwise it returns `std::string::npos`.
    - The function returns `true` if the result is not `std::string::npos`, indicating that an escapable character was found, otherwise it returns `false`.
- **Output**: A boolean value indicating whether the input string contains any escapable characters.


---
### add\_escaped\_characters<!-- {{#callable:CLI::detail::std::string::add_escaped_characters}} -->
The `add_escaped_characters` function processes a string to add escape sequences for certain special characters.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that needs to be processed for escape sequences.
- **Control Flow**:
    - Initialize an empty string `out` and reserve space for it based on the input string size plus 4 additional characters.
    - Iterate over each character `s` in the input string `str`.
    - For each character, check if it is a special character by finding its position in the `escapedChars` string.
    - If the character is found in `escapedChars`, append a backslash '\' and the corresponding escape code from `escapedCharsCode` to `out`.
    - If the character is not a special character, append it directly to `out`.
    - Return the processed string `out` with escape sequences added.
- **Output**: A `std::string` with escape sequences added for special characters found in the input string.


---
### hexConvert<!-- {{#callable:CLI::detail::std::uint32_t::hexConvert}} -->
The `hexConvert` function converts a single hexadecimal character to its corresponding integer value.
- **Inputs**:
    - `hc`: A single character representing a hexadecimal digit, which can be '0'-'9', 'A'-'F', or 'a'-'f'.
- **Control Flow**:
    - Initialize an integer variable `hcode` to 0.
    - Check if the input character `hc` is between '0' and '9'; if true, set `hcode` to the integer value of `hc` minus '0'.
    - Check if the input character `hc` is between 'A' and 'F'; if true, set `hcode` to the integer value of `hc` minus 'A' plus 10.
    - Check if the input character `hc` is between 'a' and 'f'; if true, set `hcode` to the integer value of `hc` minus 'a' plus 10.
    - If none of the above conditions are met, set `hcode` to -1.
    - Return `hcode` cast to a `uint32_t`.
- **Output**: A `uint32_t` representing the integer value of the hexadecimal character, or -1 if the character is not a valid hexadecimal digit.


---
### make\_char<!-- {{#callable:CLI::detail::make_char}} -->
The `make_char` function converts a 32-bit unsigned integer to a character by casting it to an unsigned char and then to a char.
- **Inputs**:
    - `code`: A 32-bit unsigned integer representing a character code.
- **Control Flow**:
    - The function takes a 32-bit unsigned integer as input.
    - It casts the integer to an unsigned char, which is then cast to a char.
    - The resulting char is returned.
- **Output**: A char that represents the input code as a character.


---
### append\_codepoint<!-- {{#callable:CLI::detail::append_codepoint}} -->
The `append_codepoint` function appends a UTF-8 encoded representation of a Unicode code point to a given string.
- **Inputs**:
    - `str`: A reference to a `std::string` where the UTF-8 encoded code point will be appended.
    - `code`: A `std::uint32_t` representing the Unicode code point to be encoded and appended.
- **Control Flow**:
    - Check if the code point is less than 0x80, and if so, append it directly as an ASCII character.
    - If the code point is between 0x80 and 0x800, encode it as a two-byte UTF-8 sequence and append both bytes.
    - If the code point is between 0x800 and 0x10000, check for invalid UTF-8 range (0xD800 to 0xDFFF) and encode it as a three-byte UTF-8 sequence, appending all three bytes.
    - If the code point is between 0x10000 and 0x110000, encode it as a four-byte UTF-8 sequence and append all four bytes.
- **Output**: The function modifies the input string `str` by appending the UTF-8 encoded representation of the input code point.
- **Functions called**:
    - [`CLI::detail::make_char`](#make_char)


---
### remove\_escaped\_characters<!-- {{#callable:CLI::detail::std::string::remove_escaped_characters}} -->
The `remove_escaped_characters` function processes a string to remove escape sequences, converting them into their corresponding characters or throwing exceptions for invalid sequences.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that contains the input string with potential escape sequences.
- **Control Flow**:
    - Initialize an empty string `out` and reserve space equal to the input string's size.
    - Iterate over each character in the input string `str`.
    - If a backslash '\' is encountered, check if there is at least one more character following it; otherwise, throw an invalid_argument exception.
    - Determine if the character following the backslash is a recognized escape character (e.g., 'b', 't', 'n', etc.) and append the corresponding character to `out`.
    - If the character following the backslash is 'u', ensure there are four subsequent hexadecimal characters, convert them to a Unicode code point, and append the corresponding character to `out`.
    - If the character following the backslash is 'U', ensure there are eight subsequent hexadecimal characters, convert them to a Unicode code point, and append the corresponding character to `out`.
    - If the character following the backslash is '0', append a null character '\0' to `out`.
    - If the escape sequence is unrecognized, throw an invalid_argument exception.
    - If the current character is not a backslash, append it directly to `out`.
    - Return the processed string `out`.
- **Output**: A `std::string` that is the input string with escape sequences replaced by their corresponding characters.
- **Functions called**:
    - [`CLI::detail::std::uint32_t::hexConvert`](#uint32_thexConvert)
    - [`CLI::detail::append_codepoint`](#append_codepoint)


---
### close\_string\_quote<!-- {{#callable:CLI::detail::std::size_t::close_string_quote}} -->
The `close_string_quote` function finds the position of the closing quote character in a string, accounting for escaped characters.
- **Inputs**:
    - `str`: A constant reference to the input string in which the closing quote is to be found.
    - `start`: The starting index in the string from which to begin searching for the closing quote.
    - `closure_char`: The character that represents the closing quote to be found.
- **Control Flow**:
    - Initialize a variable `loc` to zero.
    - Iterate over the string starting from `start + 1` to the end of the string.
    - Check if the current character is the `closure_char`; if so, break the loop.
    - If the current character is a backslash '\', increment `loc` to skip the next character, as it is part of an escape sequence.
    - Return the position `loc` where the closing quote character is found or the end of the string if not found.
- **Output**: The function returns the index of the closing quote character in the string, or the size of the string if the closing quote is not found.


---
### close\_literal\_quote<!-- {{#callable:CLI::detail::std::size_t::close_literal_quote}} -->
The `close_literal_quote` function finds the position of the first occurrence of a specified closure character in a string, starting from a given index, and returns its position or the string's size if not found.
- **Inputs**:
    - `str`: A constant reference to a `std::string` in which the function searches for the closure character.
    - `start`: A `std::size_t` index indicating the position in the string from which to start the search.
    - `closure_char`: A `char` representing the closure character to search for in the string.
- **Control Flow**:
    - The function uses `std::string::find_first_of` to search for the first occurrence of `closure_char` in `str`, starting from `start + 1`.
    - If the closure character is found, the function returns its position.
    - If the closure character is not found, the function returns the size of the string.
- **Output**: The function returns a `std::size_t` representing the position of the closure character in the string, or the size of the string if the character is not found.


---
### close\_sequence<!-- {{#callable:CLI::detail::std::size_t::close_sequence}} -->
The `close_sequence` function finds the position in a string where a sequence of characters, starting from a given position and enclosed by a specified closure character, is properly closed.
- **Inputs**:
    - `str`: A constant reference to a string in which the sequence is to be closed.
    - `start`: A size_t value indicating the starting position in the string from which to begin searching for the closure.
    - `closure_char`: A character that represents the closure character to match in the sequence.
- **Control Flow**:
    - Find the position of the closure character in the `matchBracketChars` string.
    - Use a switch statement to determine the type of closure based on the position found.
    - If the closure character is a string quote, call [`close_string_quote`](#size_tclose_string_quote) to find the closing quote position.
    - If the closure character is a literal quote, call [`close_literal_quote`](#size_tclose_literal_quote) to find the closing quote position.
    - If the closure character is not a quote, initialize a string with the closure character and start searching from the next position.
    - Iterate through the string starting from the next position, checking for matching closure characters and nested brackets.
    - If a matching closure character is found, remove it from the stack of closures and check if the stack is empty to determine closure completion.
    - If a new bracket character is found, push its matching closure character onto the stack.
    - Continue iterating until the end of the string or until the closure is completed.
    - Return the position of the closure or the end of the string if not found.
- **Output**: Returns a size_t value representing the position in the string where the sequence is properly closed, or the end of the string if no closure is found.
- **Functions called**:
    - [`CLI::detail::std::size_t::close_string_quote`](#size_tclose_string_quote)
    - [`CLI::detail::std::size_t::close_literal_quote`](#size_tclose_literal_quote)


---
### split\_up<!-- {{#callable:CLI::detail::std::vector<std::string>::split_up}} -->
The `split_up` function splits a given string into a vector of substrings based on a specified delimiter, handling bracketed sequences as single units.
- **Inputs**:
    - `str`: A string to be split into substrings.
    - `delimiter`: A character used to determine where to split the string; if '\0', whitespace is used as the delimiter.
- **Control Flow**:
    - Define a lambda function `find_ws` to identify delimiter or whitespace based on the input `delimiter`.
    - Trim the input string `str` to remove leading and trailing whitespace.
    - Initialize an empty vector `output` to store the resulting substrings.
    - Enter a loop that continues until `str` is empty.
    - Check if the first character of `str` is a bracket character; if so, find the matching closing bracket using [`close_sequence`](#size_tclose_sequence).
    - If a matching closing bracket is found, extract the bracketed sequence and add it to `output`, then update `str` to exclude the processed part.
    - If no bracket is found, find the next delimiter or whitespace using `find_ws`, extract the substring up to that point, add it to `output`, and update `str`.
    - Trim `str` again to remove any leading whitespace.
    - Return the `output` vector containing the split substrings.
- **Output**: A vector of strings, each representing a substring of the input `str` split by the specified `delimiter`.
- **Functions called**:
    - [`CLI::detail::std::size_t::close_sequence`](#size_tclose_sequence)


---
### escape\_detect<!-- {{#callable:CLI::detail::std::size_t::escape_detect}} -->
The `escape_detect` function checks for specific characters following an offset in a string and modifies the string if certain conditions are met.
- **Inputs**:
    - `str`: A reference to a string that will be checked and potentially modified.
    - `offset`: A size_t value indicating the position in the string from which to start checking.
- **Control Flow**:
    - Retrieve the character immediately following the given offset in the string.
    - Check if this character is a double quote ('"'), single quote (''), or backtick ('`').
    - If it is, find the last occurrence of any of the characters '-', '/', ' ', '"', '', or '`' before the offset.
    - If such a character is found and it matches a specific condition (either '-' if the character at the offset is '=', or '/' otherwise), replace the character at the offset with a space (' ').
    - Return the offset incremented by one.
- **Output**: Returns the offset incremented by one, as a size_t.


---
### binary\_escape\_string<!-- {{#callable:CLI::detail::std::string::binary_escape_string}} -->
The `binary_escape_string` function converts non-printable characters in a string to their hexadecimal escape sequences and formats the string for binary representation, optionally forcing this transformation.
- **Inputs**:
    - `string_to_escape`: A constant reference to the input string that needs to be escaped.
    - `force`: A boolean flag indicating whether to force the transformation even if no changes are necessary.
- **Control Flow**:
    - Initialize an empty string `escaped_string` to store the result.
    - Iterate over each character `c` in `string_to_escape`.
    - Check if `c` is a non-printable character using `isprint`; if not, convert it to a hexadecimal escape sequence and append to `escaped_string`.
    - If `c` is 'x' or 'X', check if it follows a backslash and append the appropriate escape sequence to avoid binary sequences.
    - Otherwise, append `c` directly to `escaped_string`.
    - If `escaped_string` differs from `string_to_escape` or `force` is true, replace all single quotes in `escaped_string` with their escape sequence and wrap the string with a specific binary format prefix and suffix.
    - Return the `escaped_string`.
- **Output**: A string that represents the escaped version of the input, formatted for binary representation if necessary.


---
### is\_binary\_escaped\_string<!-- {{#callable:CLI::detail::is_binary_escaped_string}} -->
The function `is_binary_escaped_string` checks if a given string is formatted as a binary escaped string.
- **Inputs**:
    - `escaped_string`: A constant reference to a `std::string` that is potentially a binary escaped string.
- **Control Flow**:
    - Calculate the size of the input string `escaped_string`.
    - Check if the string starts with "B"(" and ends with ")"; if true, return `true`.
    - If the first condition is false, check if the string starts with "'B"(" and ends with ")"'"; if true, return `true`.
    - If neither condition is met, return `false`.
- **Output**: A boolean value indicating whether the input string is a binary escaped string.


---
### extract\_binary\_string<!-- {{#callable:CLI::detail::std::string::extract_binary_string}} -->
The `extract_binary_string` function extracts and decodes a binary string from an escaped string format, handling hexadecimal escape sequences.
- **Inputs**:
    - `escaped_string`: A string that potentially contains a binary string in an escaped format, starting with 'B"(' or ''B"(' and ending with ')"' or ')"''.
- **Control Flow**:
    - Initialize `start` and `tail` to 0, and determine the size of `escaped_string`.
    - Check if `escaped_string` starts with 'B"(' and ends with ')"', or starts with ''B"(' and ends with ')"''; set `start` and `tail` accordingly.
    - If `start` is still 0, return `escaped_string` as it is not in the expected format.
    - Reserve space in `outstring` for the decoded content.
    - Iterate over `escaped_string` from `start` to `ssize - tail`, checking for hexadecimal escape sequences.
    - If a valid hexadecimal escape sequence is found, convert it to a character and append to `outstring`.
    - If no escape sequence is found, append the current character to `outstring`.
    - Return the decoded `outstring`.
- **Output**: A string containing the decoded binary content from the input `escaped_string`, with hexadecimal escape sequences converted to their respective characters.
- **Functions called**:
    - [`CLI::detail::std::uint32_t::hexConvert`](#uint32_thexConvert)


---
### handle\_secondary\_array<!-- {{#callable:CLI::detail::handle_secondary_array}} -->
The `handle_secondary_array` function processes a string that represents a secondary array by duplicating each character within the brackets and wrapping it with double brackets.
- **Inputs**:
    - `str`: A reference to a string that is potentially formatted as a secondary array, enclosed in square brackets.
- **Control Flow**:
    - Check if the string has at least two characters and is enclosed in square brackets.
    - If true, initialize a new string `tstr` with double opening brackets.
    - Iterate over each character in the input string, starting from the second character to the second-to-last character.
    - For each character, append it twice to `tstr`.
    - Replace the original string with the newly constructed `tstr`.
- **Output**: The function modifies the input string in place, transforming it into a format with duplicated characters enclosed in double brackets if it initially represented a secondary array.


---
### process\_quoted\_string<!-- {{#callable:CLI::detail::process_quoted_string}} -->
The `process_quoted_string` function processes a string to handle quoted or binary-escaped strings, removing outer quotes or escape sequences and potentially modifying the string for secondary array handling.
- **Inputs**:
    - `str`: A reference to a string that is to be processed for quotes or escape sequences.
    - `string_char`: A character representing the quote character to check for at the start and end of the string.
    - `literal_char`: A character representing an alternative quote character to check for at the start and end of the string.
- **Control Flow**:
    - Check if the string length is less than or equal to 1, returning false if true.
    - Check if the string is a binary-escaped string using `detail::is_binary_escaped_string`; if true, extract the binary string, handle it as a secondary array, and return true.
    - Check if the string starts and ends with `string_char`; if true, remove the outer quotes, remove escaped characters if any, handle it as a secondary array, and return true.
    - Check if the string starts and ends with `literal_char` or '`'; if true, remove the outer quotes, handle it as a secondary array, and return true.
    - Return false if none of the conditions are met.
- **Output**: Returns a boolean indicating whether the string was successfully processed as a quoted or binary-escaped string.
- **Functions called**:
    - [`CLI::detail::handle_secondary_array`](#handle_secondary_array)


---
### get\_environment\_value<!-- {{#callable:CLI::detail::get_environment_value}} -->
The `get_environment_value` function retrieves the value of an environment variable given its name.
- **Inputs**:
    - `env_name`: A constant reference to a string representing the name of the environment variable to retrieve.
- **Control Flow**:
    - Initialize a null pointer `buffer` and an empty string `ename_string`.
    - Check if the code is being compiled with Microsoft Visual C++ (`_MSC_VER` is defined).
    - If on Windows, use `_dupenv_s` to get the environment variable value into `buffer` and check if successful and `buffer` is not null.
    - If successful, assign the value in `buffer` to `ename_string` and free the allocated memory for `buffer`.
    - If not on Windows, use `std::getenv` to get the environment variable value into `buffer` and check if `buffer` is not null.
    - If `buffer` is not null, assign its value to `ename_string`.
    - Return the `ename_string` which contains the environment variable value or is empty if not found.
- **Output**: A string containing the value of the specified environment variable, or an empty string if the variable is not found.


---
### streamOutAsParagraph<!-- {{#callable:CLI::detail::streamOutAsParagraph}} -->
The `streamOutAsParagraph` function formats a given text into a paragraph with specified width and line prefix, and outputs it to a stream.
- **Inputs**:
    - `out`: An output stream where the formatted paragraph will be written.
    - `text`: The input text to be formatted into a paragraph.
    - `paragraphWidth`: The maximum width of each line in the paragraph.
    - `linePrefix`: A string to be prefixed to each line of the paragraph.
    - `skipPrefixOnFirstLine`: A boolean flag indicating whether to skip the prefix on the first line of the paragraph.
- **Control Flow**:
    - If `skipPrefixOnFirstLine` is false, the function writes the `linePrefix` to the output stream.
    - The input text is split into lines using a string stream.
    - For each line, the function reads words and checks if adding the next word would exceed `paragraphWidth`.
    - If adding a word exceeds `paragraphWidth`, a newline and `linePrefix` are written to the output stream, and the word is added to the new line.
    - Each word is written to the output stream followed by a space, and the character count is updated.
    - If the end of the line is reached and it's not the last line, a newline and `linePrefix` are written to the output stream.
- **Output**: The function returns the output stream after writing the formatted paragraph.


