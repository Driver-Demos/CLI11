# Purpose
This C++ source code file is part of a library designed to provide validation functionality, specifically for command-line interface (CLI) applications. The file defines a set of validators within the `CLI` namespace, which are used to ensure that input data meets certain criteria. The primary class, `Validator`, is equipped with several operator overloads ([`operator()`](#stringoperator()), [`operator&`](#Validatoroperator&), [`operator|`](#Validatoroperator|), and [`operator!`](#Validatoroperator!)) to facilitate the combination and logical manipulation of validation rules. These validators can be used to check the existence of files and directories, validate IPv4 addresses, and transform escaped strings, among other tasks. The file also includes utility functions for path checking, which are conditionally compiled based on the availability of the C++17 filesystem library.

The code is structured to be part of a larger library, likely intended for inclusion in other projects via header files. It provides a public API for creating and using validators, which can be extended or customized as needed. The validators are implemented as inline functions, suggesting a focus on performance and ease of integration. The file also includes mechanisms for handling different operating systems and compiler environments, ensuring broad compatibility. Overall, this file is a specialized component of a CLI library, offering robust validation capabilities for command-line applications.
# Imports and Dependencies

---
- `../Validators.hpp`
- `../Encoding.hpp`
- `../Macros.hpp`
- `../StringTools.hpp`
- `../TypeTools.hpp`
- `map`
- `string`
- `utility`


# Global Variables

---
### func\_
- **Type**: `std::function<std::string(std::string &)>`
- **Description**: The `func_` variable is a lambda function that takes a reference to a `std::string` representing a filename and returns a `std::string`. It is used within the `FileOnDefaultPath` constructor to validate file paths and potentially modify the filename to include a default path if the file does not exist at the given location.
- **Use**: This variable is used to check if a file exists at a given path, and if not, it attempts to prepend a default path to the filename and recheck its existence.


# Data Structures

---
### Validator<!-- {{#data_structure:CLI::Validator}} -->
- **Description**: [See definition](../Validators.hpp.driver.md#Validator)
- **Member Functions**:
    - [`CLI::Validator::Validator`](../Validators.hpp.driver.md#ValidatorValidator)
    - [`CLI::Validator::Validator`](../Validators.hpp.driver.md#ValidatorValidator)
    - [`CLI::Validator::Validator`](../Validators.hpp.driver.md#ValidatorValidator)
    - [`CLI::Validator::Validator`](../Validators.hpp.driver.md#ValidatorValidator)
    - [`CLI::Validator::operation`](../Validators.hpp.driver.md#Validatoroperation)
    - [`CLI::Validator::operator()`](../Validators.hpp.driver.md#Validatoroperator())
    - [`CLI::Validator::description`](../Validators.hpp.driver.md#Validatordescription)
    - [`CLI::Validator::operator&`](#Validatoroperator&)
    - [`CLI::Validator::operator|`](#Validatoroperator|)
    - [`CLI::Validator::operator!`](#Validatoroperator!)
    - [`CLI::Validator::_merge_description`](#Validator_merge_description)

**Methods**

---
#### Validator::operator&<!-- {{#callable:CLI::Validator::operator&}} -->
The `operator&` function combines two `Validator` objects into a new `Validator` that requires both original validators to pass for validation to succeed.
- **Inputs**:
    - `other`: A reference to another `Validator` object to be combined with the current `Validator` using logical AND.
- **Control Flow**:
    - A new `Validator` object `newval` is created.
    - The `_merge_description` method is called to combine the descriptions of the two validators with ' AND '.
    - References to the `func_` members of both validators are stored in `f1` and `f2`.
    - A new lambda function is assigned to `newval.func_`, which calls both `f1` and `f2` on the input string and combines their results with ' AND ' if both are non-empty.
    - The `active_` member of `newval` is set to the logical AND of the `active_` members of the two validators.
    - The `application_index_` of `newval` is set to the `application_index_` of the current validator.
    - The new `Validator` object `newval` is returned.
- **Output**: A new `Validator` object that represents the logical AND combination of the two input validators.
- **See also**: [`CLI::Validator`](../Validators.hpp.driver.md#Validator)  (Data Structure)


---
#### Validator::operator|<!-- {{#callable:CLI::Validator::operator|}} -->
The `operator|` function combines two `Validator` objects using a logical OR operation, creating a new `Validator` that succeeds if either of the original validators succeed.
- **Inputs**:
    - `other`: A reference to another `Validator` object to be combined with the current one using a logical OR operation.
- **Control Flow**:
    - A new `Validator` object `newval` is created.
    - The `_merge_description` method is called to combine the descriptions of the two validators with ' OR ' as the separator.
    - References to the `func_` members of both validators are stored in `f1` and `f2`.
    - A lambda function is assigned to `newval.func_`, which applies both `f1` and `f2` to the input string and returns an empty string if either result is empty, or a combined string with ' OR ' if both are non-empty.
    - The `active_` member of `newval` is set to the logical AND of the `active_` members of the two validators.
    - The `application_index_` of `newval` is set to the `application_index_` of the current validator.
    - The new `Validator` object `newval` is returned.
- **Output**: A new `Validator` object that represents the logical OR combination of the two input validators.
- **See also**: [`CLI::Validator`](../Validators.hpp.driver.md#Validator)  (Data Structure)


---
#### Validator::operator\!<!-- {{#callable:CLI::Validator::operator!}} -->
The `operator!` function in the `Validator` class creates a new `Validator` object that negates the logic of the current validator, modifying its description and validation function accordingly.
- **Inputs**: None
- **Control Flow**:
    - A new `Validator` object `newval` is created.
    - The description function `desc_function_` of `newval` is set to prepend 'NOT ' to the current description if it is not empty.
    - The validation function `func_` of `newval` is set to return an error message if the current validation function returns an empty string, indicating a failed check.
    - The `active_` and `application_index_` properties of the current `Validator` are copied to `newval`.
    - The modified `newval` is returned.
- **Output**: A new `Validator` object with negated logic and modified description and validation function.
- **See also**: [`CLI::Validator`](../Validators.hpp.driver.md#Validator)  (Data Structure)


---
#### Validator::\_merge\_description<!-- {{#callable:CLI::Validator::_merge_description}} -->
The `_merge_description` function combines the description functions of two `Validator` objects into a single description function using a specified merger string.
- **Inputs**:
    - `val1`: The first `Validator` object whose description function is to be merged.
    - `val2`: The second `Validator` object whose description function is to be merged.
    - `merger`: A string used to join the descriptions of the two validators.
- **Control Flow**:
    - Retrieve the description function from `val1` and assign it to `dfunc1`.
    - Retrieve the description function from `val2` and assign it to `dfunc2`.
    - Define a new lambda function for `desc_function_` that calls `dfunc1` and `dfunc2` to get their descriptions.
    - Check if either description is empty; if so, concatenate them directly.
    - If both descriptions are non-empty, format them with parentheses and the merger string in between.
- **Output**: The function does not return a value; it modifies the `desc_function_` member of the current `Validator` object.
- **See also**: [`CLI::Validator`](../Validators.hpp.driver.md#Validator)  (Data Structure)



# Functions

---
### operator\(\)<!-- {{#callable:CLI::std::string::operator()}} -->
The `operator()` function in the `Validator` class applies a validation function to a given string if the validator is active.
- **Inputs**:
    - `str`: A reference to a string that is to be validated or transformed by the validator's function.
- **Control Flow**:
    - Initialize an empty string `retstring` to store the result.
    - Check if the validator is active (`active_` is true).
    - If `non_modifying_` is true, create a copy of `str` named `value` and apply the validation function `func_` to `value`, storing the result in `retstring`.
    - If `non_modifying_` is false, apply the validation function `func_` directly to `str`, storing the result in `retstring`.
    - Return `retstring`.
- **Output**: A string containing the result of the validation function, which may be an error message or an empty string if validation is successful.


---
### description<!-- {{#callable:CLI::CLI11_INLINE::description}} -->
The `description` method creates a new `Validator` object with a specified description function that returns a given string.
- **Inputs**:
    - `validator_desc`: A string representing the description to be associated with the new `Validator` object.
- **Control Flow**:
    - A new `Validator` object `newval` is created as a copy of the current object.
    - The `desc_function_` of `newval` is set to a lambda function that returns the `validator_desc` string.
    - The modified `newval` object is returned.
- **Output**: A new `Validator` object with the updated description function.


---
### check\_path<!-- {{#callable:CLI::detail::check_path}} -->
The `check_path` function determines the type of a given file path, returning whether it is a directory, a file, or nonexistent.
- **Inputs**:
    - `file`: A constant character pointer representing the file path to be checked.
- **Control Flow**:
    - The function first checks if the code is being compiled with Microsoft Visual C++ (MSVC) using `_MSC_VER` preprocessor directive.
    - If compiled with MSVC, it uses the `_stat64` function to get file status information into a `__stat64` structure.
    - If not compiled with MSVC, it uses the `stat` function to get file status information into a `stat` structure.
    - In both cases, if the status function returns 0 (indicating success), it checks if the path is a directory using the `st_mode` field and the `S_IFDIR` flag.
    - If the path is a directory, it returns `path_type::directory`; otherwise, it returns `path_type::file`.
    - If the status function does not return 0, it returns `path_type::nonexistent`.
- **Output**: The function returns a `path_type` enum value indicating whether the path is a directory, a file, or nonexistent.


---
### EscapedStringTransformer<!-- {{#callable:EscapedStringTransformer::EscapedStringTransformer}} -->
The `EscapedStringTransformer` function processes a string to handle quoted strings and escape sequences, transforming it accordingly.
- **Inputs**:
    - `str`: A reference to a string that will be transformed based on its content, such as quoted strings or escape sequences.
- **Control Flow**:
    - The function is defined as a lambda and assigned to `func_`.
    - It checks if the string is a quoted string by comparing the first and last characters and processes it using `process_quoted_string` if true.
    - If the string contains a backslash, it checks if it is a binary escaped string using `detail::is_binary_escaped_string`.
    - If it is a binary escaped string, it extracts the binary string using `detail::extract_binary_string`.
    - If it is not a binary escaped string, it removes escaped characters using `remove_escaped_characters`.
    - The function returns an empty string if no exceptions occur.
    - If an `std::invalid_argument` exception is caught, it returns the exception's message as a string.
- **Output**: The function returns an empty string if the transformation is successful, or an error message if an exception occurs.


---
### AsNumberWithUnit<!-- {{#callable:AsNumberWithUnit}} -->
The `AsSizeValue` constructor initializes an `AsNumberWithUnit` object with a size mapping based on whether kilobytes are considered as 1000 bytes or 1024 bytes, and sets a description accordingly.
- **Inputs**:
    - `kb_is_1000`: A boolean indicating whether kilobytes should be considered as 1000 bytes (true) or 1024 bytes (false).
- **Control Flow**:
    - The constructor calls `get_mapping` with `kb_is_1000` to obtain a size mapping.
    - It initializes the base class `AsNumberWithUnit` with the obtained mapping.
    - If `kb_is_1000` is true, it sets the description to "SIZE [b, kb(=1000b), kib(=1024b), ...]".
    - If `kb_is_1000` is false, it sets the description to "SIZE [b, kb(=1024b), ...]".
- **Output**: The function does not return a value; it initializes an object of the `AsSizeValue` class.
- **Functions called**:
    - [`CLI::CLI11_INLINE::description`](#11_INLINEdescription)


---
### init\_mapping<!-- {{#callable:std::map<std::string, AsSizeValue::result_t>::AsSizeValue::init_mapping}} -->
The `init_mapping` function initializes and returns a map that associates string representations of size units with their corresponding numerical values, based on whether kilobytes are defined as 1000 or 1024 bytes.
- **Inputs**:
    - `kb_is_1000`: A boolean flag indicating whether kilobytes should be considered as 1000 bytes (true) or 1024 bytes (false).
- **Control Flow**:
    - Initialize an empty map `m` to store the size unit mappings.
    - Determine the `k_factor` based on the `kb_is_1000` flag, setting it to 1000 if true, otherwise 1024.
    - Set `ki_factor` to 1024, and initialize `k` and `ki` to 1.
    - Map the string "b" to the value 1 in the map `m`.
    - Iterate over the list of size unit prefixes {"k", "m", "g", "t", "p", "e"}.
    - For each prefix, multiply `k` by `k_factor` and `ki` by `ki_factor`.
    - Map the prefix and its variations (e.g., "k", "kb", "ki", "kib") to their respective values in the map `m`.
    - Return the populated map `m`.
- **Output**: A map where keys are string representations of size units (e.g., "b", "kb", "kib") and values are their corresponding numerical values based on the specified kilobyte definition.


---
### get\_mapping<!-- {{#callable:std::map<std::string, AsSizeValue::result_t>::AsSizeValue::get_mapping}} -->
The `get_mapping` function returns a static map of string keys to size values, initialized based on whether kilobytes are considered as 1000 or 1024 bytes.
- **Inputs**:
    - `kb_is_1000`: A boolean flag indicating whether kilobytes should be considered as 1000 bytes (true) or 1024 bytes (false).
- **Control Flow**:
    - Check if `kb_is_1000` is true.
    - If true, initialize a static map `m` using `init_mapping(true)` and return it.
    - If false, initialize a static map `m` using `init_mapping(false)` and return it.
- **Output**: A `std::map<std::string, AsSizeValue::result_t>` that maps size unit strings to their corresponding size values.
- **Functions called**:
    - [`std::map<std::string, AsSizeValue::result_t>::AsSizeValue::init_mapping`](#AsSizeValueinit_mapping)


---
### split\_program\_name<!-- {{#callable:detail::std::pair<std::string, std::string>::split_program_name}} -->
The `split_program_name` function splits a command line string into a program name and its arguments.
- **Inputs**:
    - `commandline`: A string representing the command line input, which includes the program name and its arguments.
- **Control Flow**:
    - Trim the input command line string to remove leading and trailing whitespace.
    - Initialize a pair `vals` to store the program name and arguments separately.
    - Find the first space in the command line string starting from the second character to identify potential program name boundaries.
    - Iterate through the command line string, checking if the substring up to the first space is a valid file path using `detail::check_path`.
    - If no valid file path is found, assume the first argument is the program name, handling quoted strings and escaped quotes appropriately.
    - If a valid program name is not found, default to the substring up to the first space as the program name.
    - Trim any trailing spaces from the program name.
    - Assign the remaining part of the command line string after the program name to the second element of the pair, trimming leading spaces.
    - Return the pair containing the program name and the remaining arguments.
- **Output**: A `std::pair<std::string, std::string>` where the first element is the program name and the second element is the remaining command line arguments.


