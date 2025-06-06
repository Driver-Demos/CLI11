# Purpose
This C++ source code file is part of the CLI11 library, which is a command-line interface parser for C++. The file defines inline implementations for the `Option` class, which is a core component of the library responsible for handling command-line options. The `Option` class provides a variety of methods to configure and manipulate command-line options, including setting expected values, adding validators and transformers, managing dependencies and exclusions between options, and handling multi-option policies. The file includes detailed logic for validating and processing command-line arguments, ensuring that they meet specified criteria and transforming them as needed.

The code is structured to provide a comprehensive set of functionalities for managing command-line options, making it a critical part of the CLI11 library's public API. It includes methods for setting and retrieving option properties, such as whether an option is required, whether it should ignore case or underscores, and how it should handle multiple values. The file also includes mechanisms for validating and transforming option values using custom validators and transformers, which can be defined by the user. This file is intended to be included in other parts of the CLI11 library, as indicated by the `#pragma once` directive and the inclusion of other headers, and it plays a crucial role in enabling the library to parse and interpret command-line arguments effectively.
# Imports and Dependencies

---
- `../Option.hpp`
- `algorithm`
- `string`
- `utility`
- `vector`


# Functions

---
### copy\_to<!-- {{#callable:CLI::OptionBase<CRTP>::copy_to}} -->
The `copy_to` function copies configuration settings from an `OptionBase` object to another object of type `T`.
- **Inputs**:
    - `T *other`: A pointer to an object of type `T` where the configuration settings will be copied to.
- **Control Flow**:
    - The function sets the `group` of `other` to the `group_` of the current object.
    - The `required` status of `other` is set to the `required_` status of the current object.
    - The `ignore_case` setting of `other` is set to the `ignore_case_` setting of the current object.
    - The `ignore_underscore` setting of `other` is set to the `ignore_underscore_` setting of the current object.
    - The `configurable` status of `other` is set to the `configurable_` status of the current object.
    - The `disable_flag_override` setting of `other` is set to the `disable_flag_override_` setting of the current object.
    - The `delimiter` of `other` is set to the `delimiter_` of the current object.
    - The `always_capture_default` setting of `other` is set to the `always_capture_default_` setting of the current object.
    - The `multi_option_policy` of `other` is set to the `multi_option_policy_` of the current object.
- **Output**: The function does not return any value; it modifies the `other` object in place.


---
### expected<!-- {{#callable:CLI::Option::expected}} -->
The `expected` function sets the minimum and maximum expected values for an option, adjusting negative values and ensuring the minimum is not greater than the maximum.
- **Inputs**:
    - `value_min`: The minimum expected value for the option, which can be negative.
    - `value_max`: The maximum expected value for the option, which can also be negative.
- **Control Flow**:
    - If `value_min` is negative, it is converted to its positive equivalent.
    - If `value_max` is negative, it is set to a predefined maximum vector size from `detail::expected_max_vector_size`.
    - If `value_max` is less than `value_min`, the values of `expected_min_` and `expected_max_` are swapped to ensure `expected_min_` is less than or equal to `expected_max_`.
    - Otherwise, `expected_min_` is set to `value_min` and `expected_max_` is set to `value_max`.
- **Output**: Returns a pointer to the current `Option` object, allowing for method chaining.


---
### check<!-- {{#callable:CLI::Option::check}} -->
The `check` function adds a validator to the `Option` object, which is used to validate input strings based on a provided validation function, description, and name.
- **Inputs**:
    - `Validator`: A `std::function` that takes a `const std::string &` and returns a `std::string`, used to validate input strings.
    - `Validator_description`: A `std::string` providing a description of the validator.
    - `Validator_name`: A `std::string` representing the name of the validator.
- **Control Flow**:
    - The function adds a new validator to the `validators_` vector using `emplace_back`, which constructs the validator in place with the provided function, description, and name.
    - The `non_modifying` method is called on the newly added validator to ensure it does not modify the input string.
    - The function returns a pointer to the current `Option` object (`this`).
- **Output**: A pointer to the current `Option` object, allowing for method chaining.


---
### transform<!-- {{#callable:CLI::Option::transform}} -->
The `transform` method adds a transformation function to the list of validators for an `Option` object, allowing the transformation of option values before validation.
- **Inputs**:
    - `func`: A `std::function` that takes a `std::string` and returns a `std::string`, representing the transformation function to be applied to the option value.
    - `transform_description`: A `std::string` providing a description of the transformation, used for documentation or error messages.
    - `transform_name`: A `std::string` representing the name of the transformation, used for identification purposes.
- **Control Flow**:
    - A `Validator` object is created with a lambda function that applies the `func` transformation to the input string `val` and returns an empty string.
    - The `Validator` object is initialized with the provided `transform_description` and `transform_name`.
    - The `Validator` is inserted at the beginning of the `validators_` list, ensuring it is applied before other validators.
    - The method returns a pointer to the current `Option` object (`this`).
- **Output**: A pointer to the current `Option` object, allowing for method chaining.


---
### each<!-- {{#callable:CLI::Option::each}} -->
The `each` method adds a validator to the `Option` object that applies a given function to each input string without modifying it.
- **Inputs**:
    - `func`: A `std::function<void(std::string)>` that takes a string as input and performs an operation on it.
- **Control Flow**:
    - The method takes a function `func` as an argument.
    - It adds a lambda function to the `validators_` vector, which applies `func` to a string reference `inout`.
    - The lambda function returns an empty string after applying `func`.
    - The method returns a pointer to the current `Option` object (`this`).
- **Output**: A pointer to the current `Option` object, allowing for method chaining.


---
### get\_validator<!-- {{#callable:CLI::Option::get_validator}} -->
The `get_validator` function retrieves a validator from the `validators_` vector at a specified index.
- **Inputs**:
    - `index`: An integer representing the position of the validator in the `validators_` vector to be retrieved.
- **Control Flow**:
    - Check if the provided index is within the valid range (0 to size of `validators_` - 1).
    - If the index is valid, return a pointer to the validator at the specified index in the `validators_` vector.
    - If the index is invalid, throw an `OptionNotFound` exception with a message indicating the validator index is not valid.
- **Output**: A pointer to the `Validator` object at the specified index in the `validators_` vector.


---
### remove\_needs<!-- {{#callable:CLI::Option::remove_needs}} -->
The `remove_needs` function removes a specified `Option` pointer from the `needs_` list of an `Option` object if it exists.
- **Inputs**:
    - `opt`: A pointer to an `Option` object that is to be removed from the `needs_` list.
- **Control Flow**:
    - The function uses `std::find` to search for the `opt` pointer in the `needs_` list.
    - If the `opt` pointer is not found, the function returns `false`.
    - If the `opt` pointer is found, it is removed from the `needs_` list using `erase`, and the function returns `true`.
- **Output**: A boolean value indicating whether the `opt` pointer was successfully removed (`true`) or not found (`false`).


---
### excludes<!-- {{#callable:CLI::Option::excludes}} -->
The `excludes` function adds a mutual exclusion relationship between two `Option` objects, ensuring that if one is selected, the other cannot be.
- **Inputs**:
    - `opt`: A pointer to an `Option` object that is to be mutually excluded with the current `Option` object.
- **Control Flow**:
    - Check if the input `Option` pointer `opt` is the same as the current object (`this`); if so, throw an `IncorrectConstruction` exception because an option cannot exclude itself.
    - Insert the input `Option` pointer `opt` into the `excludes_` set of the current `Option` object to establish the exclusion relationship.
    - Insert the current `Option` object (`this`) into the `excludes_` set of the input `Option` object `opt` to ensure the exclusion is symmetric.
    - Return the current `Option` object (`this`) to allow method chaining.
- **Output**: Returns a pointer to the current `Option` object (`this`) after establishing the exclusion relationship.


---
### remove\_excludes<!-- {{#callable:CLI::Option::remove_excludes}} -->
The `remove_excludes` function removes a specified `Option` from the `excludes_` set of the current `Option` object if it exists.
- **Inputs**:
    - `opt`: A pointer to an `Option` object that is to be removed from the `excludes_` set of the current `Option` object.
- **Control Flow**:
    - The function uses `std::find` to search for the `opt` in the `excludes_` set of the current `Option` object.
    - If `opt` is not found, the function returns `false`.
    - If `opt` is found, it is removed from the `excludes_` set using `erase`, and the function returns `true`.
- **Output**: A boolean value indicating whether the `opt` was successfully removed from the `excludes_` set (`true` if removed, `false` if not found).


---
### ignore\_case<!-- {{#callable:CLI::Option::ignore_case}} -->
The `ignore_case` function sets the `ignore_case_` flag for an `Option` object and checks for name conflicts with other options in the same parent if the flag is enabled.
- **Inputs**:
    - `value`: A boolean value indicating whether to enable or disable case insensitivity for the option.
- **Control Flow**:
    - Check if `ignore_case_` is currently false and `value` is true.
    - If true, set `ignore_case_` to true and retrieve the parent object cast to type `T`.
    - Iterate over each option in the parent's options list.
    - Skip the current option in the iteration.
    - For each other option, check if there is a matching name with the current option using `matching_name`.
    - If a matching name is found, set `ignore_case_` back to false and throw an `OptionAlreadyAdded` exception with a conflict message.
    - If `ignore_case_` is already true or `value` is false, simply set `ignore_case_` to `value`.
- **Output**: Returns a pointer to the current `Option` object (`this`).


---
### ignore\_underscore<!-- {{#callable:CLI::Option::ignore_underscore}} -->
The `ignore_underscore` function sets the `ignore_underscore_` flag for an `Option` object and checks for name conflicts with other options in the same parent context.
- **Inputs**:
    - `value`: A boolean value indicating whether underscores should be ignored in option names.
- **Control Flow**:
    - Check if `ignore_underscore_` is currently false and `value` is true.
    - If true, set `ignore_underscore_` to true and retrieve the parent object cast to type `T`.
    - Iterate over each option in the parent's options list.
    - Skip the current option if it matches `this`.
    - For each other option, check if there is a matching name with the current option using `matching_name`.
    - If a matching name is found, set `ignore_underscore_` back to false and throw an `OptionAlreadyAdded` exception with a conflict message.
    - If `ignore_underscore_` is already true or `value` is false, simply set `ignore_underscore_` to `value`.
- **Output**: Returns a pointer to the current `Option` object (`this`).


---
### multi\_option\_policy<!-- {{#callable:CLI::Option::multi_option_policy}} -->
The `multi_option_policy` method sets the policy for handling multiple options and adjusts the expected maximum number of options if necessary.
- **Inputs**:
    - `value`: A `MultiOptionPolicy` enum value that specifies the new policy for handling multiple options.
- **Control Flow**:
    - Check if the new policy value is different from the current `multi_option_policy_` value.
    - If the current policy is `MultiOptionPolicy::Throw`, `expected_max_` is set to `expected_min_` if `expected_max_` equals `detail::expected_max_vector_size` and `expected_min_` is greater than 1, to maintain backward compatibility.
    - Update `multi_option_policy_` to the new value.
    - Set `current_option_state_` to `option_state::parsing`.
- **Output**: Returns a pointer to the current `Option` object (`this`).


---
### get\_name<!-- {{#callable:CLI::CLI11_INLINE::string::get_name}} -->
The `get_name` function retrieves the name of an option based on its positional status and whether all options should be considered.
- **Inputs**:
    - `positional`: A boolean indicating whether the option is positional.
    - `all_options`: A boolean indicating whether to consider all options when retrieving the name.
- **Control Flow**:
    - Check if the option's group is empty and return an empty string if true, indicating the option is hidden.
    - If `all_options` is true, construct a list of option names based on the presence of positional, short, and long names, and return the joined list.
    - If `positional` is true, return the positional name `pname_`.
    - If there are long names available, return the first long name prefixed with '--'.
    - If there are no long names but short names are available, return the first short name prefixed with '-'.
    - If none of the above conditions are met, return the positional name `pname_`.
- **Output**: A string representing the name of the option, which could be a positional name, a short name, or a long name, depending on the input parameters and the option's configuration.
- **Functions called**:
    - [`CLI::CLI11_INLINE::string::get_flag_value`](#stringget_flag_value)


---
### run\_callback<!-- {{#callable:CLI::Option::run_callback}} -->
The `run_callback` function executes a callback function for an option, handling default values and validating results.
- **Inputs**: None
- **Control Flow**:
    - Initialize `used_default_str` to false.
    - If `force_callback_` is true and `results_` is empty, set `used_default_str` to true and add `default_str_` to `results_`.
    - If `current_option_state_` is `parsing`, validate `results_` and set `current_option_state_` to `validated`.
    - If `current_option_state_` is less than `reduced`, reduce `results_` into `proc_results_`.
    - Set `current_option_state_` to `callback_run`.
    - If `callback_` is not null, determine `send_results` based on whether `proc_results_` is empty, then execute `callback_` with `send_results`.
    - If `used_default_str` is true and the callback was used, clear `results_` and `proc_results_`.
    - If the callback returns false, throw a `ConversionError` with the option name and `results_`.
- **Output**: The function does not return a value but may throw a `ConversionError` if the callback fails.
- **Functions called**:
    - [`CLI::Option::add_result`](#Optionadd_result)
    - [`CLI::Option::_validate_results`](#Option_validate_results)
    - [`CLI::Option::_reduce_results`](#Option_reduce_results)
    - [`CLI::CLI11_INLINE::string::get_name`](#stringget_name)


---
### matching\_name<!-- {{#callable:CLI::Option::matching_name}} -->
The `matching_name` function checks for a matching short or long name between two `Option` objects, considering configurability and case/underscore ignoring settings, and returns the first match found.
- **Inputs**:
    - `other`: An `Option` object to compare against the current `Option` object for matching names.
- **Control Flow**:
    - Initialize a static empty string `estring` to return if no match is found.
    - Check if both `Option` objects are configurable.
    - Iterate over short names (`snames_`) of the current `Option` and check if any match with the short or long names of `other`; return the first match found.
    - Iterate over long names (`lnames_`) of the current `Option` and check if any match with the long or short names of `other`; return the first match found.
    - Check if both `Option` objects are configurable and have empty short and long names but non-empty positional names (`pname_`); return the positional name if it matches.
    - Check if the current `Option` has case or underscore ignoring enabled, and if so, iterate over `other`'s short and long names to find a match; return the first match found.
    - Return `estring` if no matches are found.
- **Output**: A reference to the first matching name found between the two `Option` objects, or an empty string if no match is found.


---
### check\_name<!-- {{#callable:CLI::CLI11_INLINE::check_name}} -->
The `check_name` function verifies if a given option name matches the expected format or predefined names, considering case and underscore sensitivity.
- **Inputs**:
    - `name`: A constant reference to a `std::string` representing the option name to be checked.
- **Control Flow**:
    - Check if the name starts with '--' and has more than two characters; if so, call `check_lname` with the substring after '--'.
    - Check if the name starts with '-' and has more than one character; if so, call `check_sname` with the substring after '-'.
    - If `pname_` is not empty, create local copies of `pname_` and `name`, and modify them based on `ignore_underscore_` and `ignore_case_` flags.
    - Compare the modified `local_name` with `local_pname`; return true if they match.
    - If `envname_` is not empty, compare `name` with `envname_` and return true if they match.
    - Return false if none of the conditions are met.
- **Output**: A boolean value indicating whether the name matches the expected format or predefined names.


---
### get\_flag\_value<!-- {{#callable:CLI::CLI11_INLINE::string::get_flag_value}} -->
The `get_flag_value` function determines the appropriate flag value for a given option name and input value, considering various conditions and defaults.
- **Inputs**:
    - `name`: A string representing the name of the option for which the flag value is being retrieved.
    - `input_value`: A string representing the input value provided for the option, which may be empty or a specific value.
- **Control Flow**:
    - Check if `disable_flag_override_` is true; if so, verify that `input_value` is empty or matches the default flag value, otherwise throw an `ArgumentMismatch::FlagOverride` exception.
    - Find the index of the option name in `fnames_` using `detail::find_member`, considering case and underscore settings.
    - If `input_value` is empty or equals `emptyString`, return the default flag value or `trueString` if `flag_like_` is true.
    - If the index is negative, return `input_value` as it is.
    - If the default flag value at the found index is `falseString`, convert `input_value` to a flag value using `detail::to_flag_value` and handle conversion errors by returning `input_value`.
    - Return the appropriate flag value based on the conditions and conversions applied.
- **Output**: A string representing the determined flag value for the given option name and input value, which may be a default value, `true`, `false`, or the input value itself.


---
### add\_result<!-- {{#callable:CLI::Option::add_result}} -->
The `add_result` function adds a list of string results to an option's results vector and updates the option's state to parsing.
- **Inputs**:
    - `s`: A vector of strings representing the results to be added to the option's results vector.
- **Control Flow**:
    - Set the current option state to `parsing`.
    - Iterate over each string in the input vector `s`.
    - For each string, call the [`_add_result`](#Option_add_result) function to add it to the `results_` vector.
    - Return the current instance of the `Option` class.
- **Output**: Returns a pointer to the current `Option` object, allowing for method chaining.
- **Functions called**:
    - [`CLI::Option::_add_result`](#Option_add_result)


---
### reduced\_results<!-- {{#callable:CLI::CLI11_INLINE::reduced_results}} -->
The `reduced_results` function returns a processed version of the option's results, potentially reducing them based on the current state and policies.
- **Inputs**: None
- **Control Flow**:
    - Initialize `res` with `proc_results_` if not empty, otherwise use `results_`.
    - Check if `current_option_state_` is less than `option_state::reduced`.
    - If `current_option_state_` is `option_state::parsing`, set `res` to `results_` and validate it using [`_validate_results`](#Option_validate_results).
    - If `res` is not empty, create an `extra` results container and reduce `res` into `extra` using [`_reduce_results`](#Option_reduce_results).
    - If `extra` is not empty, move `extra` into `res`.
    - Return `res`.
- **Output**: A `results_t` object containing the reduced results of the option.
- **Functions called**:
    - [`CLI::Option::_validate_results`](#Option_validate_results)
    - [`CLI::Option::_reduce_results`](#Option_reduce_results)


---
### type\_size<!-- {{#callable:CLI::Option::type_size}} -->
The `type_size` function sets the minimum and maximum type size for an option, adjusting for backwards compatibility and certain conditions.
- **Inputs**:
    - `option_type_size_min`: The minimum type size for the option, which can be negative for backwards compatibility.
    - `option_type_size_max`: The maximum type size for the option, which can also be negative for backwards compatibility.
- **Control Flow**:
    - Check if either `option_type_size_min` or `option_type_size_max` is negative, and if so, set `expected_max_` to `detail::expected_max_vector_size` and take the absolute values of the inputs.
    - Compare `option_type_size_min` and `option_type_size_max`; if the minimum is greater than the maximum, swap their values.
    - Set `type_size_min_` and `type_size_max_` to the adjusted minimum and maximum values.
    - If `type_size_max_` is zero, set `required_` to false.
    - If `type_size_max_` is greater than or equal to `detail::expected_max_vector_size`, set `inject_separator_` to true.
    - Return the current object (`this`).
- **Output**: Returns a pointer to the current `Option` object, allowing for method chaining.


---
### get\_type\_name<!-- {{#callable:CLI::CLI11_INLINE::string::get_type_name}} -->
The `get_type_name` function constructs and returns a string representing the type name of an option, appending descriptions of any associated validators.
- **Inputs**: None
- **Control Flow**:
    - Initialize `full_type_name` with the result of `type_name_()`.
    - Check if the `validators_` vector is not empty.
    - Iterate over each `Validator` in `validators_`.
    - For each `Validator`, retrieve its description using `get_description()`.
    - If the description is not empty, append it to `full_type_name` with a colon separator.
    - Return the constructed `full_type_name`.
- **Output**: A `std::string` representing the type name of the option, potentially including descriptions of validators.


---
### \_validate\_results<!-- {{#callable:CLI::Option::_validate_results}} -->
The `_validate_results` function validates a list of results using predefined validators and throws an error if any validation fails.
- **Inputs**:
    - `res`: A reference to a vector of strings (`results_t`) that contains the results to be validated.
- **Control Flow**:
    - Check if there are any validators to apply; if not, exit the function.
    - Determine if the maximum type size is greater than 1 to decide the validation strategy.
    - Initialize an index to track the position of each result in the context of the type size.
    - Adjust the index if the number of results exceeds the expected maximum and the multi-option policy is either `TakeLast` or `Reverse`.
    - Iterate over each result in the `res` vector.
    - If a result is a separator and the type size is variable, reset the index and continue to the next result.
    - Validate each result using the [`_validate`](#string_validate) method, passing the result and the current index.
    - If validation returns an error message, throw a `ValidationError` with the option's name and the error message.
    - Increment the index after each validation.
- **Output**: The function does not return a value but may throw a `ValidationError` if any result fails validation.
- **Functions called**:
    - [`CLI::std::string::_validate`](#string_validate)
    - [`CLI::CLI11_INLINE::string::get_name`](#stringget_name)


---
### \_reduce\_results<!-- {{#callable:CLI::Option::_reduce_results}} -->
The `_reduce_results` function processes and reduces a list of results based on a specified multi-option policy.
- **Inputs**:
    - `out`: A reference to a `results_t` vector where the reduced results will be stored.
    - `original`: A constant reference to a `results_t` vector containing the original results to be processed.
- **Control Flow**:
    - The function starts by clearing the `out` vector to prepare it for storing reduced results.
    - A switch statement is used to determine the action based on the `multi_option_policy_`.
    - For `TakeAll`, no action is taken, and the original results are left unchanged.
    - For `TakeLast`, the function calculates a `trim_size` and assigns the last `trim_size` elements from `original` to `out`.
    - For `Reverse`, similar to `TakeLast`, but the results in `out` are reversed after assignment.
    - For `TakeFirst`, the first `trim_size` elements from `original` are assigned to `out`.
    - For `Join`, if there are multiple results, they are joined into a single string using a delimiter and added to `out`.
    - For `Sum`, the results are summed and the result is added to `out`.
    - For `Throw` and default, the function checks if the number of results is within expected bounds and throws exceptions if not.
    - After processing, the function checks if `out` is empty and handles special cases for empty indicators.
- **Output**: The function outputs the reduced results in the `out` vector, which is modified in place.
- **Functions called**:
    - [`CLI::CLI11_INLINE::string::get_name`](#stringget_name)


---
### \_validate<!-- {{#callable:CLI::std::string::_validate}} -->
The `_validate` function checks a given string against a set of validators and returns an error message if validation fails.
- **Inputs**:
    - `result`: A reference to a string that needs to be validated.
    - `index`: An integer representing the index of the current validation context.
- **Control Flow**:
    - Initialize an empty error message string `err_msg`.
    - Check if `result` is empty and `expected_min_` is 0; if true, return the empty `err_msg`.
    - Iterate over each validator in `validators_`.
    - For each validator, check if its application index is -1 or matches the provided `index`.
    - Attempt to validate `result` using the current validator, catching any `ValidationError` exceptions.
    - If an error message is returned from the validator, break the loop.
- **Output**: A string containing an error message if validation fails, or an empty string if validation is successful.


---
### \_add\_result<!-- {{#callable:CLI::Option::_add_result}} -->
The `_add_result` function processes a string result, potentially splitting it into multiple parts based on specific conditions, and appends these parts to a vector, returning the count of parts added.
- **Inputs**:
    - `result`: A string to be processed and potentially split into multiple parts.
    - `res`: A reference to a vector of strings where the processed parts of the result will be stored.
- **Control Flow**:
    - Initialize `result_count` to 0 to keep track of the number of results added.
    - Check if the result is a vector escape sequence (starts with `[[` and ends with `]]` with all characters duplicated).
    - If it is a vector escape sequence, process it to remove duplicates and add the processed string to `res`, then return the count.
    - Check if the result is a vector string (enclosed in `[]`) and if extra arguments are allowed or expected max/type size is greater than 1.
    - If it is a vector string, remove the enclosing brackets, split the string by commas, and recursively call `_add_result` for each part, accumulating the count.
    - If the delimiter is `\0`, add the result directly to `res` and increment the count.
    - Otherwise, split the result by the delimiter and add each non-empty part to `res`, incrementing the count for each part added.
    - Return the total count of results added to `res`.
- **Output**: The function returns an integer representing the number of parts added to the `res` vector.


