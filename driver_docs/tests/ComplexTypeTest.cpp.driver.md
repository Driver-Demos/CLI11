# Purpose
This C++ source code file is designed to extend the functionality of a command-line interface (CLI) application by adding support for parsing complex numbers as command-line options. The file primarily focuses on defining a function [`add_option`](#add_option) that integrates with the CLI11 library to allow users to specify complex numbers in the command line. The function uses a callback mechanism to parse the input strings into `std::complex<double>` objects, handling both real and imaginary parts. The code also includes test cases using the Catch2 testing framework to ensure the correct parsing and handling of complex numbers, both with and without default values.

Additionally, the file contains a conditional compilation section that checks for the availability of the `<regex>` library, which is used to implement a custom `lexical_cast` function for parsing complex numbers from strings. This function uses regular expressions to support various complex number formats, including those with 'j' or 'i' suffixes. The file also defines a new class [`complex_new`](#complex_newcomplex_new) to demonstrate the extensibility of the parsing mechanism for user-defined complex number types. Overall, this code provides a specialized utility for handling complex numbers in CLI applications, enhancing the flexibility and usability of command-line tools that require complex number inputs.
# Imports and Dependencies

---
- `app_helper.hpp`
- `complex`
- `cstdint`
- `string`
- `regex`


# Data Structures

---
### complex\_new<!-- {{#data_structure:complex_new}} -->
- **Type**: `class`
- **Members**:
    - `val1_`: Represents the real part of the complex number.
    - `val2_`: Represents the imaginary part of the complex number.
- **Description**: The `complex_new` class is a custom implementation of a complex number, encapsulating two private double members, `val1_` and `val2_`, which represent the real and imaginary parts of the complex number, respectively. It provides a default constructor and a parameterized constructor for initialization, as well as public member functions `real()` and `imag()` to access the real and imaginary components. This class is designed to be used in applications where complex number operations are required, and it integrates with the CLI11 library for command-line interface options.
- **Member Functions**:
    - [`complex_new::complex_new`](#complex_newcomplex_new)
    - [`complex_new::complex_new`](#complex_newcomplex_new)
    - [`complex_new::real`](#complex_newreal)
    - [`complex_new::imag`](#complex_newimag)

**Methods**

---
#### complex\_new::complex\_new<!-- {{#callable:complex_new::complex_new}} -->
The `complex_new` constructor initializes a complex number object with two double values representing the real and imaginary parts.
- **Inputs**:
    - `v1`: A double representing the real part of the complex number.
    - `v2`: A double representing the imaginary part of the complex number.
- **Control Flow**:
    - The constructor initializes the private member `val1_` with the value of `v1`.
    - The constructor initializes the private member `val2_` with the value of `v2`.
- **Output**: An instance of the `complex_new` class with specified real and imaginary parts.
- **See also**: [`complex_new`](#complex_new)  (Data Structure)


---
#### complex\_new::complex\_new<!-- {{#callable:complex_new::complex_new}} -->
The `complex_new` constructor initializes a complex number object with two double values representing the real and imaginary parts.
- **Inputs**:
    - `v1`: A double representing the real part of the complex number.
    - `v2`: A double representing the imaginary part of the complex number.
- **Control Flow**:
    - The constructor initializes the private member `val1_` with the value of `v1`.
    - The constructor initializes the private member `val2_` with the value of `v2`.
- **Output**: An instance of the `complex_new` class with the specified real and imaginary parts.
- **See also**: [`complex_new`](#complex_new)  (Data Structure)


---
#### complex\_new::real<!-- {{#callable:complex_new::real}} -->
The `real` function returns the real part of a `complex_new` object.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member `val1_`, which represents the real part of the complex number.
- **Output**: A `double` representing the real part of the complex number stored in the `complex_new` object.
- **See also**: [`complex_new`](#complex_new)  (Data Structure)


---
#### complex\_new::imag<!-- {{#callable:complex_new::imag}} -->
The `imag` function returns the imaginary part of a `complex_new` object.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member `val2_`, which represents the imaginary part of the complex number.
- **Output**: A `double` representing the imaginary part of the complex number.
- **See also**: [`complex_new`](#complex_new)  (Data Structure)



# Functions

---
### add\_option<!-- {{#callable:add_option}} -->
The `add_option` function adds a command-line option to a CLI application that parses and assigns complex number values to a given variable.
- **Inputs**:
    - `app`: A reference to a `CLI::App` object where the option will be added.
    - `name`: A string representing the name of the command-line option.
    - `variable`: A reference to a `cx` (std::complex<double>) variable where the parsed complex number will be stored.
    - `description`: An optional string providing a description of the command-line option.
    - `defaulted`: A boolean indicating whether the option has a default value.
- **Control Flow**:
    - Define a callback function `fun` that attempts to parse two double values from the command-line results and assigns them to the `variable` as a complex number.
    - Add the option to the `app` using `app.add_option` with the specified name, callback function, description, and defaulted flag.
    - Set the option's type name to 'COMPLEX' and type size to 2, indicating it expects two values.
    - If the option is defaulted, convert the current value of `variable` to a string and set it as the default string for the option.
    - Return the created `CLI::Option` pointer.
- **Output**: A pointer to the created `CLI::Option` object.


---
### lexical\_cast<std::complex<double>><!-- {{#callable:CLI::detail::lexical_cast<std::complex<double>>}} -->
The function `lexical_cast<std::complex<double>>` converts a string representation of a complex number into a `std::complex<double>` object.
- **Inputs**:
    - `input`: A string representing a complex number, which can be in various formats including 'a+bi', 'a-bi', 'a', or 'bi'.
    - `output`: A reference to a `std::complex<double>` object where the parsed complex number will be stored.
- **Control Flow**:
    - A regular expression is used to match the input string against a pattern that represents complex numbers.
    - If the match is successful and the size of the match is 9, the real and imaginary parts are extracted and converted using `CLI::detail::lexical_cast`.
    - If the input ends with 'j' or 'i', it is treated as a purely imaginary number, and the real part is set to zero.
    - If the input does not end with 'j' or 'i', it is treated as a purely real number, and the imaginary part is set to zero.
    - If the conversion is successful, the `output` is set to the complex number formed by the extracted real and imaginary parts.
    - The function returns a boolean indicating whether the conversion was successful.
- **Output**: A boolean value indicating whether the conversion from string to `std::complex<double>` was successful.


