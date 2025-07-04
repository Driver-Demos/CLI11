# Purpose
This C++ header file is part of the CLI11 library, which is designed to facilitate command-line interface (CLI) parsing. The file primarily defines a set of classes and functions related to input validation, which are essential for ensuring that command-line arguments meet specific criteria before being processed by an application. The core component of this file is the [`Validator`](#ValidatorValidator) class, which provides a flexible mechanism for defining custom validation logic. This class allows users to specify validation functions, descriptions, and other properties to tailor the validation process to their needs. Additionally, the file includes several pre-defined validators, such as `ExistingFileValidator`, `ExistingDirectoryValidator`, `IPV4Validator`, and [`Range`](#RangeRange), which check for common conditions like file existence, directory existence, valid IP addresses, and numerical ranges.

The file also introduces more specialized validators like [`Transformer`](#TransformerTransformer) and [`CheckedTransformer`](#CheckedTransformerCheckedTransformer), which not only validate input but also transform it into a desired format. These components are crucial for applications that require input normalization or conversion. The file includes utility functions and classes within the `detail` namespace, which support the main validation logic by providing helper functions for tasks like type conversion, string manipulation, and set operations. Overall, this header file is a comprehensive collection of validation tools that can be used to enhance the robustness and reliability of command-line applications by ensuring that inputs are correctly formatted and meet specified criteria.
# Imports and Dependencies

---
- `Error.hpp`
- `Macros.hpp`
- `StringTools.hpp`
- `TypeTools.hpp`
- `cmath`
- `cstdint`
- `functional`
- `iostream`
- `limits`
- `map`
- `memory`
- `string`
- `utility`
- `vector`
- `filesystem`
- `sys/stat.h`
- `sys/types.h`
- `impl/Validators_inl.hpp`


# Global Variables

---
### ExistingFile
- **Type**: ``const detail::ExistingFileValidator``
- **Description**: The `ExistingFile` variable is a global constant instance of the `ExistingFileValidator` class, which is part of the `detail` namespace. This validator is designed to check for the existence of a file, returning an error message if the file does not exist.
- **Use**: This variable is used to validate that a specified file exists, typically in command-line interface applications.


---
### ExistingDirectory
- **Type**: ``const detail::ExistingDirectoryValidator``
- **Description**: The `ExistingDirectory` variable is a constant instance of the `ExistingDirectoryValidator` class, which is part of the `detail` namespace. This validator is designed to check for the existence of a directory and returns an error message if the validation fails.
- **Use**: This variable is used to validate that a given directory path exists, ensuring that operations requiring a valid directory can proceed without errors.


---
### ExistingPath
- **Type**: ``const detail::ExistingPathValidator``
- **Description**: The `ExistingPath` variable is a global constant instance of the `ExistingPathValidator` class, which is part of the `detail` namespace. This validator is designed to check for the existence of a path, whether it is a file or a directory, and returns an error message if the path does not exist.
- **Use**: `ExistingPath` is used to validate that a given path exists in the filesystem.


---
### NonexistentPath
- **Type**: ``const detail::NonexistentPathValidator``
- **Description**: The `NonexistentPath` is a global constant instance of the `NonexistentPathValidator` class, which is part of the `detail` namespace. This validator is designed to check for paths that do not exist, returning an error message if the validation fails.
- **Use**: It is used to validate that a given path does not exist, typically in command-line interface applications.


---
### ValidIPV4
- **Type**: ``const detail::IPV4Validator``
- **Description**: The `ValidIPV4` is a global constant instance of the `detail::IPV4Validator` class. This class is designed to validate whether a given string is a legal IPv4 address. It inherits from the `Validator` class, which provides a framework for creating validation functions that return error messages if validation fails.
- **Use**: `ValidIPV4` is used to check if a string is a valid IPv4 address, returning an error message if the validation fails.


---
### EscapedString
- **Type**: ``const detail::EscapedStringTransformer``
- **Description**: `EscapedString` is a global constant variable of type `detail::EscapedStringTransformer`. This type is a subclass of `Validator`, which suggests that it is used for validating or transforming strings, specifically handling escaped characters.
- **Use**: `EscapedString` is used to convert escaped characters in strings into their associated values, likely as part of a validation or transformation process in the CLI library.


---
### Number
- **Type**: ``const TypeValidator<double>``
- **Description**: The `Number` variable is a constant instance of the `TypeValidator` class, specifically templated for the `double` type. It is initialized with the string "NUMBER", which likely serves as a name or identifier for this validator.
- **Use**: This variable is used to validate input strings to ensure they can be successfully parsed as double-precision floating-point numbers.


---
### NonNegativeNumber
- **Type**: ``Range``
- **Description**: The `NonNegativeNumber` is a global constant of type `Range` that represents a range validator for non-negative numbers. It is initialized with a maximum value of `std::numeric_limits<double>::max()` and is labeled with the name "NONNEGATIVE".
- **Use**: This variable is used to validate that a given number is non-negative, ensuring it falls within the range from 0 to the maximum representable double value.


---
### PositiveNumber
- **Type**: ``const Range``
- **Description**: The `PositiveNumber` variable is a constant instance of the `Range` class, which is used to define a range of valid values for a number. It is initialized with the smallest positive double value as the minimum and the largest double value as the maximum, effectively representing all positive numbers.
- **Use**: This variable is used to validate that a given number is positive, ensuring it falls within the specified range of positive double values.


# Data Structures

---
### Validator<!-- {{#data_structure:CLI::Validator}} -->
- **Type**: `class`
- **Members**:
    - `desc_function_`: A function that returns a string description of the validator.
    - `func_`: A function that performs validation and returns an error message if validation fails.
    - `name_`: A string representing the name of the validator for search purposes.
    - `application_index_`: An integer indicating the index of the value to which the validator applies, with -1 indicating all elements.
    - `active_`: A boolean indicating whether the validator is active.
    - `non_modifying_`: A boolean indicating whether the validator should not modify the input.
- **Description**: The `Validator` class is a flexible and extensible data structure designed to perform validation on strings. It encapsulates a validation function (`func_`) that checks the validity of a string and returns an error message if the validation fails. The class also includes a description function (`desc_function_`) to provide a textual description of the validator, a name for identification purposes, and several configuration options such as `application_index_` to specify which elements the validator applies to, `active_` to enable or disable the validator, and `non_modifying_` to ensure the input remains unchanged. The class supports logical operations to combine multiple validators and provides methods to set and retrieve its properties.
- **Member Functions**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)
    - [`CLI::Validator::Validator`](#ValidatorValidator)
    - [`CLI::Validator::Validator`](#ValidatorValidator)
    - [`CLI::Validator::Validator`](#ValidatorValidator)
    - [`CLI::Validator::operation`](#Validatoroperation)
    - [`CLI::Validator::operator()`](#Validatoroperator))
    - [`CLI::Validator::description`](#Validatordescription)
    - [`CLI::Validator::operator&`](impl/Validators_inl.hpp.driver.md#Validatoroperator)
    - [`CLI::Validator::operator|`](impl/Validators_inl.hpp.driver.md#Validatoroperator)
    - [`CLI::Validator::operator!`](impl/Validators_inl.hpp.driver.md#Validatoroperator)
    - [`CLI::Validator::_merge_description`](impl/Validators_inl.hpp.driver.md#Validator_merge_description)

**Methods**

---
#### Validator::Validator<!-- {{#callable:CLI::Validator::Validator}} -->
The `Validator` constructor initializes a `Validator` object with a description and a validation function.
- **Inputs**:
    - `validator_desc`: A string that describes the validator.
    - `func`: A function that takes a reference to a string and returns a string, used for validation logic.
- **Control Flow**:
    - The constructor initializes the `desc_function_` member with a lambda that returns the `validator_desc` string.
    - The `func_` member is initialized with the provided `func` argument, using `std::move` to transfer ownership.
- **Output**: The constructor does not return a value; it initializes the `Validator` object.
- **See also**: [`CLI::Validator`](#Validator)  (Data Structure)


---
#### Validator::Validator<!-- {{#callable:CLI::Validator::Validator}} -->
The `Validator` constructor initializes a `Validator` object with a default description function and validation function.
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as `default`, meaning it does not perform any custom initialization beyond what is automatically provided by the compiler.
    - The `desc_function_` is initialized with a lambda that returns an empty string.
    - The `func_` is initialized with a lambda that takes a `std::string` reference and returns an empty string.
- **Output**: A `Validator` object with default settings.
- **See also**: [`CLI::Validator`](#Validator)  (Data Structure)


---
#### Validator::Validator<!-- {{#callable:CLI::Validator::Validator}} -->
The `Validator` constructor initializes a `Validator` object with a description string, setting up a description function that returns this string.
- **Inputs**:
    - `validator_desc`: A string representing the description of the validator.
- **Control Flow**:
    - The constructor takes a single string argument `validator_desc`.
    - It initializes the `desc_function_` member with a lambda function that captures `validator_desc` and returns it when called.
- **Output**: A `Validator` object is constructed with its `desc_function_` member initialized to return the provided description string.
- **See also**: [`CLI::Validator`](#Validator)  (Data Structure)


---
#### Validator::Validator<!-- {{#callable:CLI::Validator::Validator}} -->
The `Validator` constructor initializes a `Validator` object with a validation operation, description, and optional name.
- **Inputs**:
    - `op`: A `std::function` that takes a `std::string&` and returns a `std::string`, representing the validation operation to be performed.
    - `validator_desc`: A `std::string` that provides a description of the validator.
    - `validator_name`: An optional `std::string` that specifies the name of the validator, defaulting to an empty string if not provided.
- **Control Flow**:
    - The constructor initializes the `desc_function_` member with a lambda that returns the `validator_desc` string.
    - The `func_` member is initialized by moving the `op` function into it, setting up the validation operation.
    - The `name_` member is initialized by moving the `validator_name` into it, allowing for an optional name for the validator.
- **Output**: The constructor does not return a value; it initializes a `Validator` object with the provided parameters.
- **See also**: [`CLI::Validator`](#Validator)  (Data Structure)


---
#### Validator::operation<!-- {{#callable:CLI::Validator::operation}} -->
The `operation` method sets the validation function for a `Validator` object and returns the modified `Validator` instance.
- **Inputs**:
    - `op`: A `std::function` that takes a `std::string&` as input and returns a `std::string`, representing the validation operation to be set for the `Validator`.
- **Control Flow**:
    - The method assigns the provided function `op` to the member variable `func_` using `std::move` to transfer ownership.
    - The method returns a reference to the current `Validator` instance (`*this`).
- **Output**: A reference to the current `Validator` instance, allowing for method chaining.
- **See also**: [`CLI::Validator`](#Validator)  (Data Structure)


---
#### Validator::operator\(\)<!-- {{#callable:CLI::Validator::operator()}} -->
The `operator()` function in the `Validator` class applies a validation function to a given string if the validator is active.
- **Inputs**:
    - `str`: A constant reference to a `std::string` that represents the input string to be validated.
- **Control Flow**:
    - The function first copies the input string `str` to a local variable `value`.
    - It checks if the `Validator` is active by evaluating the `active_` member variable.
    - If `active_` is true, it applies the validation function `func_` to `value` and returns the result.
    - If `active_` is false, it returns an empty `std::string`.
- **Output**: A `std::string` that is either the result of the validation function if the validator is active, or an empty string if it is not.
- **See also**: [`CLI::Validator`](#Validator)  (Data Structure)


---
#### Validator::description<!-- {{#callable:CLI::Validator::description}} -->
The `description` method sets a description function for the `Validator` object that returns a specified string.
- **Inputs**:
    - `validator_desc`: A string representing the description to be set for the `Validator`.
- **Control Flow**:
    - The method takes a string `validator_desc` as input.
    - It assigns a lambda function to `desc_function_` that returns the `validator_desc` string.
    - The method returns a reference to the current `Validator` object.
- **Output**: A reference to the current `Validator` object, allowing for method chaining.
- **See also**: [`CLI::Validator`](#Validator)  (Data Structure)



---
### CustomValidator<!-- {{#data_structure:CustomValidator}} -->
- **Type**: `class`
- **Description**: The `CustomValidator` class is a derived class from the `Validator` class, which is part of a validation framework in the CLI namespace. It inherits all the properties and functionalities of the `Validator` class, allowing it to perform string validation operations. The `CustomValidator` class itself does not introduce any new members or methods, serving as a specialized type of `Validator` that can be extended or customized further for specific validation needs.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### path\_type<!-- {{#data_structure:detail::path_type}} -->
- **Type**: `enum`
- **Members**:
    - `nonexistent`: Represents a path that does not exist.
    - `file`: Represents a path that is a file.
    - `directory`: Represents a path that is a directory.
- **Description**: The `path_type` enum class is a simple enumeration used to categorize paths into three distinct types: nonexistent, file, and directory. It is defined with an underlying type of `std::uint8_t`, which is a small, unsigned integer type. This enum is useful for distinguishing between different types of paths when performing file system operations or validations.


---
### ExistingFileValidator<!-- {{#data_structure:detail::ExistingFileValidator}} -->
- **Type**: `class`
- **Description**: The `ExistingFileValidator` class is a specialized validator that inherits from the `Validator` class, designed to check for the existence of a file. It is part of a set of validators in the CLI namespace that provide validation functionality for command-line interface applications. This class does not define any additional members beyond those inherited from `Validator`, and its primary purpose is to encapsulate the logic for verifying that a specified file exists, returning an error message if the validation fails.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### ExistingDirectoryValidator<!-- {{#data_structure:detail::ExistingDirectoryValidator}} -->
- **Type**: `class`
- **Description**: The `ExistingDirectoryValidator` is a class that inherits from the `Validator` class, designed to check for the existence of a directory. It is part of a set of validators that provide validation functionality for different types of inputs, specifically focusing on directory paths in this case. The class does not define any additional members or fields beyond those inherited from `Validator`, and its primary purpose is to encapsulate the logic for validating whether a given directory path exists.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### ExistingPathValidator<!-- {{#data_structure:detail::ExistingPathValidator}} -->
- **Type**: `class`
- **Description**: The `ExistingPathValidator` is a class that inherits from the `Validator` class and is designed to check for the existence of a path, whether it is a file or a directory. It does not have any additional members or fields beyond those inherited from `Validator`, and its primary purpose is to provide a validation mechanism that returns an error message if the specified path does not exist.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### NonexistentPathValidator<!-- {{#data_structure:detail::NonexistentPathValidator}} -->
- **Type**: `class`
- **Description**: The `NonexistentPathValidator` is a class that inherits from the `Validator` class, designed to check for paths that do not exist. It is part of a set of validators used to validate strings, particularly in the context of command-line interfaces. This class does not have any additional members or fields beyond those inherited from `Validator`, and it is likely used to ensure that a given path does not exist, returning an error message if the validation fails.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### IPV4Validator<!-- {{#data_structure:detail::IPV4Validator}} -->
- **Type**: `class`
- **Description**: The `IPV4Validator` class is a specialized validator that inherits from the `Validator` class, designed to validate whether a given string is a legal IPv4 address. It does not have any additional members or fields beyond those inherited from `Validator`, and its primary purpose is to encapsulate the logic for IPv4 address validation within the CLI11 library.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### EscapedStringTransformer<!-- {{#data_structure:detail::EscapedStringTransformer}} -->
- **Type**: `class`
- **Description**: The `EscapedStringTransformer` is a class that inherits from the `Validator` class, designed to transform strings by converting escaped characters into their associated values. It is part of a set of validators and transformers used to process and validate command-line input strings in the CLI11 library. This class does not have any additional members or fields beyond those inherited from `Validator`, and its primary function is to handle string transformations related to escape sequences.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### TypeValidator<!-- {{#data_structure:TypeValidator}} -->
- **Type**: `class`
- **Description**: The `TypeValidator` class is a template class that extends the `Validator` class, designed to validate input strings by attempting to parse them into a specified `DesiredType`. It uses a lambda function to perform the validation, which attempts to convert the input string into the `DesiredType` using a `lexical_cast` function. If the conversion fails, it returns an error message indicating the failure to parse the input as the desired type. The class provides constructors to initialize the validator with a specific name or default to the type name of the `DesiredType`.
- **Member Functions**:
    - [`TypeValidator::TypeValidator`](#TypeValidatorTypeValidator)
    - [`TypeValidator::TypeValidator`](#TypeValidatorTypeValidator)
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)

**Methods**

---
#### TypeValidator::TypeValidator<!-- {{#callable:TypeValidator::TypeValidator}} -->
The `TypeValidator` class template is a specialized validator that checks if a given string can be successfully parsed into a specified desired type.
- **Inputs**:
    - `validator_name`: A string representing the name of the validator, used for identification and description purposes.
- **Control Flow**:
    - The constructor initializes the `Validator` base class with a name and a lambda function for validation.
    - The lambda function attempts to parse the input string into the `DesiredType` using [`lexical_cast`](TypeTools.hpp.driver.md#lexical_cast).
    - If parsing fails, it returns an error message indicating the failure and the expected type.
    - If parsing succeeds, it returns an empty string indicating successful validation.
- **Output**: An instance of `TypeValidator` that can validate strings against the specified `DesiredType`, returning an error message if validation fails or an empty string if it succeeds.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#lexical_cast)
- **See also**: [`TypeValidator`](#TypeValidator)  (Data Structure)


---
#### TypeValidator::TypeValidator<!-- {{#callable:TypeValidator::TypeValidator}} -->
The `TypeValidator` class template is a specialized validator that checks if a given string can be parsed into a specified type, `DesiredType`, and returns an error message if parsing fails.
- **Inputs**:
    - `validator_name`: A string representing the name of the validator, used for identification and error messages.
- **Control Flow**:
    - The constructor initializes the base `Validator` class with a name and a lambda function for validation.
    - The lambda function attempts to parse the input string into the `DesiredType` using `lexical_cast`.
    - If parsing fails, it returns an error message indicating the failure and the expected type.
    - If parsing succeeds, it returns an empty string, indicating successful validation.
- **Output**: An error message string if validation fails, or an empty string if validation succeeds.
- **See also**: [`TypeValidator`](#TypeValidator)  (Data Structure)



---
### FileOnDefaultPath<!-- {{#data_structure:FileOnDefaultPath}} -->
- **Type**: `class`
- **Description**: The `FileOnDefaultPath` class is a specialized validator that inherits from the `Validator` class. It is designed to modify a file path if the file is located at a specified default location. The class can be used either as a check or a transformation, with an optional feature to disable error return. It is constructed with a default path and a boolean flag to enable or disable error return.
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)


---
### Range<!-- {{#data_structure:Range}} -->
- **Type**: `class`
- **Description**: The `Range` class is a specialized validator that extends the `Validator` class, designed to check if a given value falls within a specified range. It is templated to accept any type `T` and can be constructed with either a minimum and maximum value or just a maximum value, defaulting the minimum to zero. The class uses a lambda function to perform the validation, ensuring that the input value is within the specified bounds, and returns an error message if the validation fails. This class is useful for validating numerical inputs in command-line interfaces, ensuring they fall within acceptable limits.
- **Member Functions**:
    - [`Range::Range`](#RangeRange)
    - [`Range::Range`](#RangeRange)
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)

**Methods**

---
#### Range::Range<!-- {{#callable:Range::Range}} -->
The `Range` constructor template creates a validator that checks if a given input value is within a specified inclusive range, and optionally assigns a custom validator name.
- **Inputs**:
    - `T min_val`: The minimum value of the range, inclusive.
    - `T max_val`: The maximum value of the range, inclusive.
    - `const std::string &validator_name`: An optional name for the validator; defaults to an empty string if not provided.
- **Control Flow**:
    - The constructor initializes the base `Validator` class with the provided `validator_name`.
    - If `validator_name` is empty, it constructs a default description string indicating the type and range of values.
    - A lambda function is assigned to `func_` which attempts to convert the input string to the type `T`.
    - If conversion fails or the value is outside the specified range, an error message is returned.
    - If the value is within the range, an empty string is returned, indicating successful validation.
- **Output**: The constructor does not return a value, but it sets up a validation function that returns an error message if the input is invalid, or an empty string if valid.
- **Functions called**:
    - [`CLI::Validator::description`](#Validatordescription)
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#lexical_cast)
- **See also**: [`Range`](#Range)  (Data Structure)


---
#### Range::Range<!-- {{#callable:Range::Range}} -->
The `Range` constructor initializes a range validator with a specified maximum value, defaulting the minimum to zero, and optionally assigns a validator name.
- **Inputs**:
    - `T max_val`: The maximum value of the range, of a templated type `T`.
    - `const std::string &validator_name`: An optional name for the validator, defaulting to an empty string.
- **Control Flow**:
    - The constructor is templated to accept any type `T` for the maximum value.
    - It calls another `Range` constructor with the minimum value set to zero, the provided maximum value, and the optional validator name.
    - The `Range` constructor being called initializes a range validator with a minimum and maximum value, and sets up a validation function to check if a given input string can be converted to type `T` and falls within the specified range.
- **Output**: A `Range` object is constructed, which is a type of `Validator` that checks if a value is within a specified range.
- **See also**: [`Range`](#Range)  (Data Structure)



---
### Bound<!-- {{#data_structure:Bound}} -->
- **Type**: `class`
- **Description**: The `Bound` class is a specialized validator that extends the `Validator` class, designed to enforce that a given value falls within a specified inclusive range. It is constructed with a minimum and maximum value, and it modifies the input to ensure it stays within these bounds. If the input value is less than the minimum, it is set to the minimum; if it is greater than the maximum, it is set to the maximum. The class also provides a constructor for creating a range from 0 to a specified maximum value.
- **Member Functions**:
    - [`Bound::Bound`](#BoundBound)
    - [`Bound::Bound`](#BoundBound)
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)

**Methods**

---
#### Bound::Bound<!-- {{#callable:Bound::Bound}} -->
The `Bound` constructor template creates a validator that ensures a given input value is within a specified inclusive range, modifying the input if it falls outside the range.
- **Inputs**:
    - `min_val`: The minimum value of the range, inclusive, of type T.
    - `max_val`: The maximum value of the range, inclusive, of type T.
- **Control Flow**:
    - A stringstream is used to create a description of the bounded type and range, which is then set as the validator's description.
    - A lambda function is assigned to `func_`, capturing `min_val` and `max_val`.
    - The lambda attempts to convert the input string to type T using [`lexical_cast`](TypeTools.hpp.driver.md#lexical_cast).
    - If conversion fails, it returns an error message indicating the input could not be converted.
    - If the converted value is less than `min_val`, the input is set to `min_val` as a string.
    - If the converted value is greater than `max_val`, the input is set to `max_val` as a string.
    - If the value is within the range, the input remains unchanged and an empty string is returned.
- **Output**: The function returns a string, which is empty if the input is valid and within range, or an error message if the input could not be converted.
- **Functions called**:
    - [`CLI::Validator::description`](#Validatordescription)
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#lexical_cast)
- **See also**: [`Bound`](#Bound)  (Data Structure)


---
#### Bound::Bound<!-- {{#callable:Bound::Bound}} -->
The `Bound` constructor initializes a `Bound` object with a specified maximum value, setting the minimum value to zero.
- **Inputs**:
    - `max_val`: A value of type `T` representing the maximum bound for the range.
- **Control Flow**:
    - The constructor is templated to accept any type `T`.
    - It calls another constructor of the `Bound` class with the minimum value set to zero and the maximum value set to `max_val`.
    - The `static_cast<T>(0)` is used to ensure the minimum value is of the same type as `max_val`.
- **Output**: A `Bound` object initialized with a range from 0 to `max_val`.
- **See also**: [`Bound`](#Bound)  (Data Structure)



---
### has\_find<!-- {{#data_structure:detail::has_find}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constant that indicates whether the type C has a find method that can accept a parameter of type V.
    - `type`: A type alias for std::integral_constant<bool, value> that represents the result of the test as a type.
- **Description**: The `has_find` struct is a type trait used to determine if a given type `C` has a `find` method that can accept a parameter of type `V`. It uses SFINAE (Substitution Failure Is Not An Error) to test for the presence of the `find` method by attempting to call it with a value of type `V`. If the method exists, `value` is set to `true`, otherwise it is set to `false`. This trait is useful for template metaprogramming, allowing conditional compilation based on the presence of a `find` method in a type.


---
### IsMember<!-- {{#data_structure:IsMember}} -->
- **Type**: `class`
- **Description**: The `IsMember` class is a specialized validator that extends the `Validator` class, designed to check if a given item is part of a specified set. It supports in-place construction using an initializer list and allows for the use of filter functions to preprocess both the input and the set elements before comparison. The class can handle multiple filter functions, which are applied in a nested manner, and it maintains a description function to generate a string representation of the set for validation purposes. The validation function ensures that the input matches an element in the set, applying any specified filters, and returns an error message if the input is not found in the set.
- **Member Functions**:
    - [`IsMember::IsMember`](#IsMemberIsMember)
    - [`IsMember::IsMember`](#IsMemberIsMember)
    - [`IsMember::IsMember`](#IsMemberIsMember)
    - [`IsMember::IsMember`](#IsMemberIsMember)
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)

**Methods**

---
#### IsMember::IsMember<!-- {{#callable:IsMember::IsMember}} -->
The `IsMember` constructor initializes an `IsMember` object using an initializer list and forwards additional arguments to another constructor.
- **Inputs**:
    - `values`: An initializer list of type `T` representing the values to be checked for membership.
    - `args`: A variadic template parameter pack representing additional arguments to be forwarded to another constructor.
- **Control Flow**:
    - The constructor takes an initializer list `values` and additional arguments `args`.
    - It converts the initializer list `values` into a `std::vector<T>`.
    - It forwards the `std::vector<T>` and additional arguments `args` to another `IsMember` constructor.
- **Output**: The constructor does not return a value; it initializes an `IsMember` object.
- **See also**: [`IsMember`](#IsMember)  (Data Structure)


---
#### IsMember::IsMember<!-- {{#callable:IsMember::IsMember}} -->
The `IsMember` function template constructs an `IsMember` object to validate if an item is part of a given set, optionally using a filter function for comparison.
- **Inputs**:
    - `T`: A generic type representing the set or container to be checked against.
    - `F`: An optional filter function that processes both the input and set elements before comparison.
- **Control Flow**:
    - The function template is called with a set and an optional filter function.
    - It determines the type of elements in the set, adapting them if necessary.
    - A local copy of the filter function is created using `std::function`.
    - A description function is set up to generate a string representation of the set.
    - A validation function is defined to check if an input string can be converted to the set's element type, applying the filter function if provided.
    - The validation function searches the set for the input, using the filter function if necessary, and returns an empty string if found, or an error message if not.
- **Output**: The function constructs an `IsMember` object that can validate input strings against a set, returning an empty string on success or an error message if the input is not found in the set.
- **See also**: [`IsMember`](#IsMember)  (Data Structure)


---
#### IsMember::IsMember<!-- {{#callable:IsMember::IsMember}} -->
The `IsMember` function template checks if a given item is a member of a specified set, optionally applying a filter function to both the item and the set elements before comparison.
- **Inputs**:
    - `T set`: A container (e.g., vector, map) that holds the elements to be checked against.
    - `F filter_function`: An optional function that transforms elements before comparison; defaults to `nullptr` if not provided.
- **Control Flow**:
    - Determine the type of elements in the set, accounting for smart pointers and maps.
    - Convert the filter function to a `std::function` if it is not already one.
    - Define a description function that generates a string representation of the set's contents.
    - Define a validation function (`func_`) that attempts to convert the input string to the appropriate type using [`lexical_cast`](TypeTools.hpp.driver.md#lexical_cast).
    - If conversion fails, throw a [`ValidationError`](Error.hpp.driver.md#ValidationError).
    - If a filter function is provided, apply it to the converted input.
    - Search the set for the transformed input using the `search` function, which may apply the filter function to set elements as well.
    - If the item is found, ensure the input string matches the set's version of the item, applying the filter function if necessary, and return an empty string indicating success.
    - If the item is not found, return an error message indicating the item is not in the set.
- **Output**: A string indicating success (empty) or an error message if the item is not found in the set.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#lexical_cast)
    - [`ValidationError`](Error.hpp.driver.md#ValidationError)
- **See also**: [`IsMember`](#IsMember)  (Data Structure)


---
#### IsMember::IsMember<!-- {{#callable:IsMember::IsMember}} -->
The `IsMember` function constructs an `IsMember` object that checks if an item is in a set, applying a series of filter functions to both the item and the set elements before comparison.
- **Inputs**:
    - `T &&set`: A set or container of elements to check membership against, which can be passed by value or reference.
    - `filter_fn_t filter_fn_1`: The first filter function to apply to the elements before comparison.
    - `filter_fn_t filter_fn_2`: The second filter function to apply to the elements after the first filter function.
    - `Args &&...other`: Additional filter functions that can be applied in sequence.
- **Control Flow**:
    - The function is a constructor for the `IsMember` class, which inherits from `Validator`.
    - It takes a set and two filter functions as arguments, along with any additional filter functions.
    - The constructor calls another `IsMember` constructor, forwarding the set and a composed filter function that applies `filter_fn_1` followed by `filter_fn_2` to each element.
    - The additional filter functions are also forwarded to the next constructor call.
- **Output**: An `IsMember` object that can be used to validate if a given item is a member of the specified set, with the specified filter functions applied.
- **See also**: [`IsMember`](#IsMember)  (Data Structure)



---
### Transformer<!-- {{#data_structure:Transformer}} -->
- **Type**: `class`
- **Description**: The `Transformer` class is a specialized type of `Validator` that is designed to transform input strings based on a mapping of string pairs. It allows for in-place construction using initializer lists or other mapping types, and supports the use of filter functions to modify both sides of a comparison before performing the transformation. The class is capable of handling multiple filter functions, which can be nested to provide complex transformation logic. The `Transformer` is particularly useful for translating named items to other values or sets, and it leverages the `Validator` base class to provide validation and transformation functionalities.
- **Member Functions**:
    - [`Transformer::Transformer`](#TransformerTransformer)
    - [`Transformer::Transformer`](#TransformerTransformer)
    - [`Transformer::Transformer`](#TransformerTransformer)
    - [`Transformer::Transformer`](#TransformerTransformer)
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)

**Methods**

---
#### Transformer::Transformer<!-- {{#callable:Transformer::Transformer}} -->
The `Transformer` constructor initializes a `Transformer` object using an initializer list of string pairs and additional arguments, forwarding them to another `Transformer` constructor.
- **Inputs**:
    - `values`: An initializer list of pairs, where each pair consists of two strings, representing key-value mappings.
    - `args`: A variadic template parameter pack that can accept any number of additional arguments, which are forwarded to another constructor.
- **Control Flow**:
    - The constructor takes an initializer list of string pairs and additional arguments.
    - It calls another `Transformer` constructor by transforming the initializer list into a `TransformPairs<std::string>` and forwarding the additional arguments.
    - The `TransformPairs<std::string>` is a type alias for a vector of string pairs, which is used to initialize the `Transformer`.
- **Output**: The function does not return a value; it initializes a `Transformer` object.
- **See also**: [`Transformer`](#Transformer)  (Data Structure)


---
#### Transformer::Transformer<!-- {{#callable:Transformer::Transformer}} -->
The `Transformer` constructor initializes a `Transformer` object with a mapping and an optional filter function, setting up internal functions for description and transformation based on the mapping.
- **Inputs**:
    - `T &&mapping`: A mapping object that is forwarded to another `Transformer` constructor, expected to produce value pairs.
- **Control Flow**:
    - The constructor is a template that takes a single argument `mapping` and forwards it to another `Transformer` constructor with a `nullptr` as the second argument.
    - The constructor uses `std::forward` to perfectly forward the `mapping` argument, allowing for efficient handling of lvalue and rvalue references.
- **Output**: The constructor does not return a value; it initializes a `Transformer` object.
- **See also**: [`Transformer`](#Transformer)  (Data Structure)


---
#### Transformer::Transformer<!-- {{#callable:Transformer::Transformer}} -->
The `Transformer` function template constructs a transformation object that maps input strings to output strings using a specified mapping and optional filter function.
- **Inputs**:
    - `T mapping`: A mapping object that produces value pairs, used to transform input strings to output strings.
    - `F filter_function`: An optional filter function that processes input values before transformation.
- **Control Flow**:
    - The function asserts that the mapping produces value pairs using a static assertion.
    - It determines the type of the contained item and adapts it to a local item type, converting bad types to good ones if necessary.
    - A local copy of the filter function is created using `std::function`.
    - A description function is set up to generate a map representation of the current mapping contents.
    - The main transformation function (`func_`) is defined, which attempts to convert the input string to the local item type using [`lexical_cast`](TypeTools.hpp.driver.md#lexical_cast).
    - If conversion fails, an empty string is returned, indicating no match in the mapping.
    - If a filter function is provided, it is applied to the converted input value.
    - The function searches the mapping for the filtered value using the `detail::search` function.
    - If a match is found, the input string is updated with the corresponding output value from the mapping.
    - The function returns an empty string if the transformation is successful, or an empty string if no match is found.
- **Output**: The function does not return a value directly; instead, it modifies the input string in place if a transformation is successful, or leaves it unchanged if not.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#lexical_cast)
- **See also**: [`Transformer`](#Transformer)  (Data Structure)


---
#### Transformer::Transformer<!-- {{#callable:Transformer::Transformer}} -->
The `Transformer` constructor initializes a `Transformer` object by combining two filter functions into a single nested filter function and passing it along with other arguments to another `Transformer` constructor.
- **Inputs**:
    - `T &&mapping`: A mapping object that is forwarded to the next constructor.
    - `filter_fn_t filter_fn_1`: The first filter function that takes a string and returns a string.
    - `filter_fn_t filter_fn_2`: The second filter function that takes a string and returns a string.
    - `Args &&...other`: Additional arguments that are forwarded to the next constructor.
- **Control Flow**:
    - The constructor takes a mapping, two filter functions, and additional arguments.
    - It creates a new filter function by nesting `filter_fn_1` and `filter_fn_2`, such that the output of `filter_fn_1` is passed as input to `filter_fn_2`.
    - The constructor then calls another `Transformer` constructor, forwarding the mapping, the newly created nested filter function, and any additional arguments.
- **Output**: The function does not return a value; it initializes a `Transformer` object.
- **See also**: [`Transformer`](#Transformer)  (Data Structure)



---
### CheckedTransformer<!-- {{#data_structure:CheckedTransformer}} -->
- **Type**: `class`
- **Description**: The `CheckedTransformer` class is a specialized type of `Validator` that is designed to transform and validate string inputs based on a mapping of string pairs. It allows for in-place construction using an initializer list of string pairs and supports the use of filter functions to preprocess both sides of the comparison before validation. The class ensures that the input string is checked against a set of mapped values, and if a match is found, the input is transformed accordingly. If no match is found, an error message is generated indicating the failure of the check.
- **Member Functions**:
    - [`CheckedTransformer::CheckedTransformer`](#CheckedTransformerCheckedTransformer)
    - [`CheckedTransformer::CheckedTransformer`](#CheckedTransformerCheckedTransformer)
    - [`CheckedTransformer::CheckedTransformer`](#CheckedTransformerCheckedTransformer)
    - [`CheckedTransformer::CheckedTransformer`](#CheckedTransformerCheckedTransformer)
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)

**Methods**

---
#### CheckedTransformer::CheckedTransformer<!-- {{#callable:CheckedTransformer::CheckedTransformer}} -->
The `CheckedTransformer` function constructs a `CheckedTransformer` object that validates and potentially transforms input strings based on a mapping and optional filter functions.
- **Inputs**:
    - `values`: An initializer list of pairs of strings representing the mapping of input values to their corresponding transformed values.
    - `args`: Additional arguments that can be passed to the constructor, potentially including filter functions.
- **Control Flow**:
    - The constructor initializes a `CheckedTransformer` object by calling another constructor with a transformed version of the input pairs and any additional arguments.
    - The transformation of pairs is done using the `TransformPairs` template, which converts the initializer list into a vector of pairs.
    - The constructor supports additional arguments, which are forwarded to the next constructor call, allowing for flexible initialization with optional filter functions.
- **Output**: A `CheckedTransformer` object that can validate and transform input strings based on the provided mapping and filter functions.
- **See also**: [`CheckedTransformer`](#CheckedTransformer)  (Data Structure)


---
#### CheckedTransformer::CheckedTransformer<!-- {{#callable:CheckedTransformer::CheckedTransformer}} -->
The `CheckedTransformer` constructor initializes a `CheckedTransformer` object with a mapping and an optional filter function to validate and transform input strings based on the mapping.
- **Inputs**:
    - `T mapping`: A mapping of type T, which should produce value pairs, used to transform input strings.
    - `F filter_function`: An optional filter function of type F that processes both sides of the comparison before validation.
- **Control Flow**:
    - The constructor checks if the mapping produces value pairs using a static assertion.
    - It determines the types of elements and items within the mapping, converting them to appropriate types if necessary.
    - A local copy of the filter function is created using `std::function`.
    - A description function (`tfunc`) is defined to generate a string representation of the mapping.
    - The `desc_function_` is set to `tfunc`.
    - The `func_` lambda function is defined to validate and transform the input string based on the mapping and filter function.
    - The `func_` attempts to convert the input string to a local item type and applies the filter function if provided.
    - It searches the mapping for the converted input and updates the input string if a match is found.
    - If no match is found, it checks if the input string matches any output strings in the mapping.
    - If no match is found, it returns a failure message indicating the input check failed.
- **Output**: The constructor initializes the `CheckedTransformer` object with a description function and a validation function that returns an empty string on success or an error message on failure.
- **See also**: [`CheckedTransformer`](#CheckedTransformer)  (Data Structure)


---
#### CheckedTransformer::CheckedTransformer<!-- {{#callable:CheckedTransformer::CheckedTransformer}} -->
The `CheckedTransformer` function template constructs a transformer that validates and potentially modifies input strings based on a mapping and an optional filter function.
- **Inputs**:
    - `T mapping`: A mapping that produces value pairs, used to transform input strings.
    - `F filter_function`: An optional filter function that processes input values before comparison.
- **Control Flow**:
    - The function asserts that the mapping produces value pairs using a static assertion.
    - It deduces types for elements, items, and iteration types from the mapping.
    - A local copy of the filter function is created using `std::function`.
    - A description function `tfunc` is defined to generate a string representation of the mapping.
    - The `desc_function_` member is set to `tfunc`.
    - The `func_` member is defined as a lambda that processes input strings.
    - The lambda attempts to convert the input string to a local item type using [`lexical_cast`](TypeTools.hpp.driver.md#lexical_cast).
    - If conversion is successful, the filter function is applied if it exists.
    - The mapping is searched for the converted and filtered value using `detail::search`.
    - If a match is found, the input string is updated with the corresponding mapped value.
    - If no match is found, the function iterates over the mapping to check if the input matches any mapped values.
    - If no match is found, an error message is returned indicating the check failed.
- **Output**: The function does not return a value directly; it sets up a transformer that modifies input strings and returns error messages if validation fails.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#lexical_cast)
- **See also**: [`CheckedTransformer`](#CheckedTransformer)  (Data Structure)


---
#### CheckedTransformer::CheckedTransformer<!-- {{#callable:CheckedTransformer::CheckedTransformer}} -->
The `CheckedTransformer` function constructs a `CheckedTransformer` object that validates and potentially transforms input strings based on a mapping and a series of filter functions.
- **Inputs**:
    - `T &&mapping`: A mapping object that associates input strings with their corresponding transformed values.
    - `filter_fn_t filter_fn_1`: The first filter function applied to the input string before validation.
    - `filter_fn_t filter_fn_2`: The second filter function applied to the result of the first filter function.
    - `Args &&...other`: Additional filter functions that can be applied in sequence.
- **Control Flow**:
    - The constructor is called with a mapping and two filter functions, along with any additional filter functions.
    - The constructor forwards the mapping and a composed filter function (combining filter_fn_1 and filter_fn_2) to another `CheckedTransformer` constructor.
    - The composed filter function is created using a lambda that applies filter_fn_1 followed by filter_fn_2 to a string.
- **Output**: A `CheckedTransformer` object that can validate and transform input strings using the provided mapping and filter functions.
- **See also**: [`CheckedTransformer`](#CheckedTransformer)  (Data Structure)



---
### AsNumberWithUnit<!-- {{#data_structure:AsNumberWithUnit}} -->
- **Type**: `class`
- **Members**:
    - `Options`: An enum that defines options for case sensitivity and unit requirement for the AsNumberWithUnit class.
- **Description**: The `AsNumberWithUnit` class is a specialized validator that extends the `Validator` class to handle numeric inputs with optional unit literals. It allows for the conversion of human-readable strings with units into numerical values, supporting both case-sensitive and case-insensitive unit matching, as well as optional or required unit specifications. The class uses a mapping of unit strings to numerical factors to perform conversions and can throw validation errors if the input does not meet the specified criteria.
- **Member Functions**:
    - [`AsNumberWithUnit::AsNumberWithUnit`](#AsNumberWithUnitAsNumberWithUnit)
    - [`AsNumberWithUnit::validate_mapping`](#AsNumberWithUnitvalidate_mapping)
    - [`AsNumberWithUnit::generate_description`](#AsNumberWithUnitgenerate_description)
- **Inherits From**:
    - [`CLI::Validator::Validator`](#ValidatorValidator)

**Methods**

---
#### AsNumberWithUnit::AsNumberWithUnit<!-- {{#callable:AsNumberWithUnit::AsNumberWithUnit}} -->
The `AsNumberWithUnit` constructor initializes a validator that converts a string with a number and optional unit into a numerical value, applying a conversion factor based on the unit.
- **Inputs**:
    - `mapping`: A map of unit strings to their corresponding numerical conversion factors.
    - `opts`: An optional parameter that specifies the behavior of the unit matching, defaulting to `DEFAULT` which is case-insensitive and allows optional units.
    - `unit_name`: A string representing the name of the unit, defaulting to "UNIT".
- **Control Flow**:
    - The constructor sets a description using `generate_description` based on the unit name and options.
    - It validates the provided mapping using [`validate_mapping`](#AsNumberWithUnitvalidate_mapping) to ensure all units are valid and adjusts for case insensitivity if needed.
    - A lambda function `func_` is defined to process input strings, trimming whitespace and checking for empty input.
    - The function identifies the unit part of the input by iterating backwards from the end of the string until a non-alphabetic character is found.
    - If the `UNIT_REQUIRED` option is set and no unit is found, a [`ValidationError`](Error.hpp.driver.md#ValidationError) is thrown.
    - If `CASE_INSENSITIVE` is set, the unit is converted to lowercase.
    - If no unit is found, the input is converted to a number directly; otherwise, the unit is looked up in the mapping.
    - If the unit is not found in the mapping, a [`ValidationError`](Error.hpp.driver.md#ValidationError) is thrown with allowed values listed.
    - If the input number is not empty, it is converted and multiplied by the unit's factor, checking for overflow; otherwise, the number is set to the unit's factor.
    - The input string is updated with the resulting numerical value.
- **Output**: The function does not return a value directly; it modifies the input string to contain the converted numerical value or throws a [`ValidationError`](Error.hpp.driver.md#ValidationError) if validation fails.
- **Functions called**:
    - [`CLI::Validator::description`](#Validatordescription)
    - [`AsNumberWithUnit::validate_mapping`](#AsNumberWithUnitvalidate_mapping)
    - [`ValidationError`](Error.hpp.driver.md#ValidationError)
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#lexical_cast)
- **See also**: [`AsNumberWithUnit`](#AsNumberWithUnit)  (Data Structure)


---
#### AsNumberWithUnit::validate\_mapping<!-- {{#callable:AsNumberWithUnit::validate_mapping}} -->
The `validate_mapping` function checks the validity of unit keys in a mapping and optionally converts them to lowercase if case insensitivity is required.
- **Inputs**:
    - `mapping`: A reference to a `std::map` with `std::string` keys and `Number` type values, representing unit mappings.
    - `opts`: An `Options` enum value that specifies the behavior of the function, particularly regarding case sensitivity.
- **Control Flow**:
    - Iterate over each key-value pair in the `mapping`.
    - Check if the key (unit) is empty and throw a [`ValidationError`](Error.hpp.driver.md#ValidationError) if it is.
    - Check if the key contains only letters using `detail::isalpha` and throw a [`ValidationError`](Error.hpp.driver.md#ValidationError) if it does not.
    - If `opts` includes `CASE_INSENSITIVE`, create a new map `lower_mapping` with all keys converted to lowercase.
    - Check for duplicate lowercase keys in `lower_mapping` and throw a [`ValidationError`](Error.hpp.driver.md#ValidationError) if any are found.
    - Replace the original `mapping` with `lower_mapping` if case insensitivity is applied.
- **Output**: The function does not return a value but may modify the `mapping` in place and can throw a [`ValidationError`](Error.hpp.driver.md#ValidationError) if validation fails.
- **Functions called**:
    - [`ValidationError`](Error.hpp.driver.md#ValidationError)
- **See also**: [`AsNumberWithUnit`](#AsNumberWithUnit)  (Data Structure)


---
#### AsNumberWithUnit::generate\_description<!-- {{#callable:AsNumberWithUnit::generate_description}} -->
The `generate_description` function creates a string description of a number type with an optional unit, based on the provided options.
- **Inputs**:
    - `name`: A string representing the name of the unit to be included in the description.
    - `opts`: An `Options` enum value that determines whether the unit is required or optional in the description.
- **Control Flow**:
    - Initialize a stringstream object `out`.
    - Append the type name of the template parameter `Number` followed by a space to `out`.
    - Check if the `opts` parameter has the `UNIT_REQUIRED` flag set.
    - If `UNIT_REQUIRED` is set, append the `name` directly to `out`.
    - If `UNIT_REQUIRED` is not set, append the `name` enclosed in square brackets to `out`.
    - Return the constructed string from the stringstream `out`.
- **Output**: A string representing the description of the number type with the unit, formatted based on the options provided.
- **See also**: [`AsNumberWithUnit`](#AsNumberWithUnit)  (Data Structure)



---
### Options<!-- {{#data_structure:AsNumberWithUnit::Options}} -->
- **Type**: `enum`
- **Members**:
    - `CASE_SENSITIVE`: Represents a case-sensitive option with a value of 0.
    - `CASE_INSENSITIVE`: Represents a case-insensitive option with a value of 1.
    - `UNIT_OPTIONAL`: Represents an optional unit option with a value of 0.
    - `UNIT_REQUIRED`: Represents a required unit option with a value of 2.
    - `DEFAULT`: Represents the default option combining CASE_INSENSITIVE and UNIT_OPTIONAL.
- **Description**: The `Options` enum is a set of constants used to define configuration options for handling case sensitivity and unit requirements in a validation context. It uses a `std::uint8_t` underlying type to store its values, allowing for efficient storage and bitwise operations. The enum provides specific options for case sensitivity (`CASE_SENSITIVE` and `CASE_INSENSITIVE`) and unit requirement (`UNIT_OPTIONAL` and `UNIT_REQUIRED`), as well as a `DEFAULT` option that combines `CASE_INSENSITIVE` and `UNIT_OPTIONAL` using a bitwise OR operation.


---
### AsSizeValue<!-- {{#data_structure:AsSizeValue}} -->
- **Type**: `class`
- **Members**:
    - `result_t`: Defines a type alias for std::uint64_t, representing the result type for size values.
- **Description**: The `AsSizeValue` class is a specialized class derived from `AsNumberWithUnit` designed to convert human-readable size strings with unit literals into a `uint64_t` size value. It provides functionality to interpret size units like 'kb', 'k', 'kib', and 'ki' as either factors of 1000 or 1024, depending on the `kb_is_1000` flag. This class supports units up to exbibyte and is useful for applications requiring precise size conversions, such as file size parsing.
- **Inherits From**:
    - [`AsNumberWithUnit::AsNumberWithUnit`](#AsNumberWithUnitAsNumberWithUnit)


# Functions

---
### name<!-- {{#callable:CLI::name}} -->
The `name` function creates a new `Validator` object with a specified name and returns it.
- **Inputs**:
    - `validator_name`: A `std::string` representing the new name to be assigned to the `Validator`.
- **Control Flow**:
    - A new `Validator` object `newval` is created as a copy of the current object using the copy constructor.
    - The `name_` member of `newval` is set to the value of `validator_name`, using `std::move` to efficiently transfer ownership of the string.
    - The modified `newval` object is returned.
- **Output**: A new `Validator` object with the updated name.


---
### get\_name<!-- {{#callable:CLI::get_name}} -->
The `get_name` function returns the name of the Validator as a constant reference to a string.
- **Inputs**: None
- **Control Flow**:
    - The function simply returns the private member variable `name_`.
- **Output**: A constant reference to a `std::string` representing the name of the Validator.


---
### active<!-- {{#callable:CLI::active}} -->
The `active` method creates a new `Validator` object with its `active_` attribute set to the specified boolean value, defaulting to `true`, and returns this new object.
- **Inputs**:
    - `active_val`: A boolean value indicating whether the new `Validator` should be active or not, defaulting to `true`.
- **Control Flow**:
    - A new `Validator` object, `newval`, is created as a copy of the current object using the copy constructor.
    - The `active_` attribute of `newval` is set to the value of `active_val`.
    - The modified `newval` object is returned.
- **Output**: A new `Validator` object with the `active_` attribute set to the specified `active_val`.


---
### non\_modifying<!-- {{#callable:CLI::non_modifying}} -->
The `non_modifying` function sets the `non_modifying_` member variable of a `Validator` object to indicate whether the validator should modify the input or not.
- **Inputs**:
    - `no_modify`: A boolean value that defaults to `true`, indicating whether the validator should be non-modifying (`true`) or modifying (`false`).
- **Control Flow**:
    - The function assigns the value of `no_modify` to the `non_modifying_` member variable.
    - The function returns a reference to the current `Validator` object (`*this`).
- **Output**: A reference to the current `Validator` object, allowing for method chaining.


---
### application\_index<!-- {{#callable:CLI::application_index}} -->
The `application_index` function creates a new `Validator` object with a specified application index and returns it.
- **Inputs**:
    - `app_index`: An integer representing the application index to be set for the new `Validator` object.
- **Control Flow**:
    - A new `Validator` object `newval` is created as a copy of the current object using the copy constructor.
    - The `application_index_` member of `newval` is set to the provided `app_index`.
    - The modified `newval` object is returned.
- **Output**: A new `Validator` object with the `application_index_` set to the specified `app_index`.


---
### get\_application\_index<!-- {{#callable:CLI::get_application_index}} -->
The `get_application_index` function returns the current value of the `application_index_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function simply returns the value of the `application_index_` member variable without any additional logic or conditions.
- **Output**: An integer representing the current application index of the validator.


---
### get\_active<!-- {{#callable:CLI::get_active}} -->
The `get_active` function returns the current state of the `active_` member variable, indicating whether the `Validator` is active or not.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `active_` member variable.
- **Output**: A boolean value indicating the active state of the `Validator`.


---
### get\_modifying<!-- {{#callable:CLI::get_modifying}} -->
The `get_modifying` function returns a boolean indicating whether the validator is allowed to modify the input.
- **Inputs**: None
- **Control Flow**:
    - The function checks the value of the `non_modifying_` member variable.
    - It returns the negation of `non_modifying_`, meaning if `non_modifying_` is false, the function returns true, indicating the validator can modify the input.
- **Output**: A boolean value indicating if the validator can modify the input.


---
### smart\_deref<!-- {{#callable:detail::smart_deref}} -->
The `smart_deref` function returns a reference to the input value if it is not a copyable pointer.
- **Inputs**:
    - `T &value`: A reference to a value of type T, which is not a copyable pointer.
- **Control Flow**:
    - The function template is specialized for types T that are not copyable pointers, as determined by the `enable_if_t` condition.
    - The function simply returns the input reference `value` without any modification.
- **Output**: A reference to the input value of type `T`.


---
### generate\_set<!-- {{#callable:detail::generate_set}} -->
The `generate_set` function creates a string representation of a set-like container, formatting its elements as a comma-separated list enclosed in curly braces.
- **Inputs**:
    - `set`: A set-like container of elements, which can be dereferenced to access its elements.
- **Control Flow**:
    - The function begins by determining the element type of the input set using `detail::element_type` and `detail::pair_adaptor` to handle potential pair elements.
    - It initializes a string `out` with an opening curly brace '{'.
    - The function appends to `out` a joined string of the set's elements, using `detail::join` to concatenate them with a comma separator, and `detail::pair_adaptor::first` to extract the first element of each pair if applicable.
    - Finally, it appends a closing curly brace '}' to `out` and returns the resulting string.
- **Output**: A string representing the set, formatted as a comma-separated list of its elements enclosed in curly braces.


---
### generate\_map<!-- {{#callable:detail::generate_map}} -->
The `generate_map` function creates a string representation of a map, optionally including only the keys.
- **Inputs**:
    - `map`: A map-like container of key-value pairs to be converted into a string representation.
    - `key_only`: A boolean flag indicating whether to include only keys (true) or both keys and values (false) in the output string.
- **Control Flow**:
    - The function begins by defining the types for elements and iteration based on the input map's type.
    - It initializes a string `out` with an opening curly brace '{'.
    - The function uses `detail::join` to iterate over the map, converting each key-value pair to a string using a lambda function.
    - The lambda function checks the `key_only` flag to determine whether to append only the key or both key and value to the result string.
    - The result of the `join` operation is appended to `out`.
    - A closing curly brace '}' is added to `out`.
    - The function returns the constructed string `out`.
- **Output**: A string representing the map, formatted as '{key1->value1,key2->value2,...}' or '{key1,key2,...}' if `key_only` is true.


---
### search<!-- {{#callable:detail::search}} -->
The [`search`](#search) function attempts to find a value in a set, optionally applying a filter function to transform elements during the search.
- **Inputs**:
    - `set`: A collection of elements to search through, which can be any type that supports iteration.
    - `val`: The value to search for within the set.
    - `filter_function`: A function that transforms elements of the set during the search; it is optional and can be null.
- **Control Flow**:
    - The function first attempts a fast search using an overloaded [`search`](#search) function that does not apply the filter function.
    - If the fast search is successful or if the filter function is null, the result of the fast search is returned.
    - If the fast search fails and a filter function is provided, a linear search is performed over the set.
    - During the linear search, each element is transformed using the filter function before being compared to the search value.
    - The function returns a pair indicating whether the value was found and an iterator to the found element or the end of the set.
- **Output**: A `std::pair` where the first element is a boolean indicating if the value was found, and the second element is an iterator to the found element or the end of the set.
- **Functions called**:
    - [`detail::search`](#search)


---
### overflowCheck<!-- {{#callable:detail::overflowCheck}} -->
The `overflowCheck` function checks if multiplying two unsigned integers would result in an overflow.
- **Inputs**:
    - `a`: The first unsigned integer to be multiplied.
    - `b`: The second unsigned integer to be multiplied.
- **Control Flow**:
    - The function uses `std::enable_if` to ensure it only operates on unsigned types.
    - It calculates the maximum value of the type `T` using `std::numeric_limits<T>::max()`.
    - It checks if the maximum value divided by `a` is less than `b`, which would indicate an overflow if `a` and `b` were multiplied.
- **Output**: A boolean value indicating whether multiplying `a` and `b` would cause an overflow (true if overflow would occur, false otherwise).


---
### checked\_multiply<!-- {{#callable:detail::checked_multiply}} -->
The `checked_multiply` function multiplies two floating-point numbers and checks for overflow, updating the first argument with the result if no overflow occurs.
- **Inputs**:
    - `a`: A reference to a floating-point number that will be multiplied by `b` and updated with the result if no overflow occurs.
    - `b`: A floating-point number that will be multiplied with `a`.
- **Control Flow**:
    - Calculate the product of `a` and `b` and store it in `c`.
    - Check if `c` is infinite while both `a` and `b` are not infinite.
    - If the above condition is true, return `false` indicating overflow.
    - Otherwise, update `a` with the value of `c` and return `true`.
- **Output**: Returns `true` if the multiplication does not result in an overflow (infinity), otherwise returns `false`.


---
### ignore\_case<!-- {{#callable:ignore_case}} -->
The `ignore_case` function converts a given string to lowercase using a helper function from the `detail` namespace.
- **Inputs**:
    - `item`: A string that needs to be converted to lowercase.
- **Control Flow**:
    - The function takes a single string argument named `item`.
    - It calls the `detail::to_lower` function with `item` as the argument.
    - The result of `detail::to_lower(item)` is returned.
- **Output**: A new string that is the lowercase version of the input string.


---
### ignore\_underscore<!-- {{#callable:ignore_underscore}} -->
The `ignore_underscore` function removes underscores from a given string by calling the `remove_underscore` function from the `detail` namespace.
- **Inputs**:
    - `item`: A string from which underscores need to be removed.
- **Control Flow**:
    - The function is a single-line inline function that directly returns the result of calling `detail::remove_underscore` with the input string `item`.
- **Output**: A string with all underscores removed from the input string.


---
### ignore\_space<!-- {{#callable:ignore_space}} -->
The `ignore_space` function removes all spaces and tab characters from a given string.
- **Inputs**:
    - `item`: A string from which spaces and tab characters are to be removed.
- **Control Flow**:
    - The function uses `std::remove` to remove all space characters (' ') from the string.
    - It then uses `std::remove` again to remove all tab characters ('\t') from the string.
    - The `erase` method is used to actually remove the characters from the string after `std::remove` shifts them to the end.
    - The modified string is returned.
- **Output**: A string with all spaces and tab characters removed.


---
### operator|<!-- {{#callable:operator|}} -->
The `operator|` function performs a bitwise OR operation on two `AsNumberWithUnit::Options` objects and returns the result as a new `AsNumberWithUnit::Options` object.
- **Inputs**:
    - `a`: The first `AsNumberWithUnit::Options` object to be used in the bitwise OR operation.
    - `b`: The second `AsNumberWithUnit::Options` object to be used in the bitwise OR operation.
- **Control Flow**:
    - The function takes two `AsNumberWithUnit::Options` objects as input parameters.
    - It casts each `AsNumberWithUnit::Options` object to an integer.
    - It performs a bitwise OR operation on the two integers.
    - The result of the bitwise OR operation is cast back to an `AsNumberWithUnit::Options` object.
    - The function returns the resulting `AsNumberWithUnit::Options` object.
- **Output**: A new `AsNumberWithUnit::Options` object that is the result of the bitwise OR operation on the input options.


---
### Validator<!-- {{#callable:CLI::Validator::Validator}} -->
The `Validator` constructor initializes a `Validator` object with a description and a validation function.
- **Inputs**:
    - `validator_desc`: A string representing the description of the validator.
    - `func`: A function that takes a reference to a string and returns a string, used for validation logic.
- **Control Flow**:
    - The constructor initializes the `desc_function_` member with a lambda that returns the `validator_desc` string.
    - The `func_` member is initialized with the provided `func` after moving it to ensure efficient resource management.
- **Output**: The constructor does not return a value; it initializes a `Validator` object.


---
### AsNumberWithUnit<!-- {{#callable:AsNumberWithUnit::AsNumberWithUnit}} -->
The `AsNumberWithUnit` function template constructs a validator that converts a string with a numeric value and an optional unit into a numeric value by applying a unit conversion factor from a provided mapping.
- **Inputs**:
    - `mapping`: A `std::map` where keys are unit strings and values are conversion factors of type `Number`.
    - `opts`: An `Options` enum value that specifies behavior such as case sensitivity and whether a unit is required; defaults to `DEFAULT`.
    - `unit_name`: A `std::string` representing the name of the unit, defaulting to "UNIT".
- **Control Flow**:
    - The function begins by generating a description using `generate_description` and validates the mapping with `validate_mapping`.
    - A lambda function `func_` is defined to process the input string, trimming whitespace and checking for an empty input, which throws a `ValidationError` if true.
    - The function identifies the position where the unit begins in the input string by iterating backward from the end until a non-alphabetic character is found.
    - The unit is extracted from the input, and the input is resized to exclude the unit part, followed by trimming.
    - If the `UNIT_REQUIRED` option is set and no unit is found, a `ValidationError` is thrown.
    - If `CASE_INSENSITIVE` is set, the unit string is converted to lowercase.
    - If no unit is present, the input is converted to a number using `lexical_cast`, and a `ValidationError` is thrown if conversion fails.
    - If a unit is present, the function looks up the unit in the mapping; if not found, a `ValidationError` is thrown with allowed values.
    - If the input is not empty, it is converted to a number and multiplied by the unit's conversion factor using `checked_multiply`, throwing a `ValidationError` on failure.
    - If the input is empty, the number is set to the conversion factor of the unit.
    - The input string is updated with the converted numeric value.
- **Output**: The function does not return a value directly; it modifies the input string to contain the converted numeric value or throws a `ValidationError` if validation fails.


