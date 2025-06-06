# Purpose
This C++ source code file is part of the CLI11 library, which is a command-line interface parser for C++. The file primarily focuses on providing functionality for converting between narrow (UTF-8) and wide (UTF-16/UTF-32) character strings, which is essential for handling Unicode text in a cross-platform manner. The code includes functions for both narrowing (converting wide strings to narrow strings) and widening (converting narrow strings to wide strings), with implementations that account for different platform-specific requirements, such as Windows and non-Windows systems. The file also includes mechanisms to set appropriate Unicode locales when necessary, ensuring that character conversions are performed correctly.

The code is structured to be included as part of a larger library, as indicated by the use of `#pragma once` and the inclusion of other header files. It defines public APIs for string conversion, such as [`narrow`](#stringnarrow) and [`widen`](#wstringwiden), which are accessible to other parts of the library or external code that uses CLI11. The file also includes conditional compilation directives to handle different C++ standards and platform-specific features, such as the availability of the `<codecvt>` header and the C++17 filesystem library. Overall, this file provides a focused and essential utility for string conversion within the CLI11 library, facilitating the handling of Unicode text in command-line applications.
# Imports and Dependencies

---
- `../Encoding.hpp`
- `../Macros.hpp`
- `array`
- `clocale`
- `cstdlib`
- `cstring`
- `cwchar`
- `locale`
- `stdexcept`
- `string`
- `type_traits`
- `utility`


# Data Structures

---
### scope\_guard\_t<!-- {{#data_structure:CLI::detail::scope_guard_t}} -->
- **Type**: `struct`
- **Members**:
    - `closure`: A callable object that is executed when the scope_guard_t object is destroyed.
- **Description**: The `scope_guard_t` struct is a utility designed to ensure that a given function or callable object is executed when the `scope_guard_t` object goes out of scope, typically used for resource management and cleanup tasks. It takes a callable object as a parameter during construction and stores it in the `closure` member. Upon destruction of the `scope_guard_t` object, the stored callable is invoked, providing a mechanism to automatically manage resources or perform cleanup actions when a scope is exited.
- **Member Functions**:
    - [`CLI::detail::scope_guard_t::scope_guard_t`](#scope_guard_tscope_guard_t)
    - [`CLI::detail::scope_guard_t::~scope_guard_t`](#scope_guard_tscope_guard_t)

**Methods**

---
#### scope\_guard\_t::scope\_guard\_t<!-- {{#callable:CLI::detail::scope_guard_t::scope_guard_t}} -->
The `scope_guard_t` struct is a utility that ensures a given closure is executed when the `scope_guard_t` object goes out of scope.
- **Inputs**:
    - `F closure_`: A callable object (closure) that is stored and executed when the `scope_guard_t` object is destroyed.
- **Control Flow**:
    - The constructor `scope_guard_t(F closure_)` initializes the `closure` member with the provided callable object `closure_`.
    - The destructor `~scope_guard_t()` is called when the `scope_guard_t` object goes out of scope, executing the stored `closure`.
- **Output**: There is no return value; the destructor executes the closure as a side effect.
- **See also**: [`CLI::detail::scope_guard_t`](#scope_guard_t)  (Data Structure)


---
#### scope\_guard\_t::\~scope\_guard\_t<!-- {{#callable:CLI::detail::scope_guard_t::~scope_guard_t}} -->
The destructor `~scope_guard_t` executes a stored closure function when a `scope_guard_t` object goes out of scope.
- **Inputs**:
    - `None`: The destructor does not take any input arguments.
- **Control Flow**:
    - The destructor `~scope_guard_t` is called automatically when a `scope_guard_t` object is destroyed, typically when it goes out of scope.
    - The stored closure function, which is a callable object, is executed within the destructor.
- **Output**: The destructor does not return any value; its purpose is to execute the closure function as a side effect.
- **See also**: [`CLI::detail::scope_guard_t`](#scope_guard_t)  (Data Structure)



# Functions

---
### set\_unicode\_locale<!-- {{#callable:CLI::detail::set_unicode_locale}} -->
The `set_unicode_locale` function attempts to set the program's locale to one of several UTF-8 compatible locales for proper Unicode handling.
- **Inputs**: None
- **Control Flow**:
    - A static array `unicode_locales` is defined with three locale strings: "C.UTF-8", "en_US.UTF-8", and ".UTF-8".
    - The function iterates over each locale in the `unicode_locales` array.
    - For each locale, it attempts to set the program's locale using `std::setlocale(LC_ALL, locale_name)`.
    - If setting the locale is successful (i.e., `std::setlocale` returns a non-null pointer), the function returns immediately.
    - If none of the locales can be set successfully, a `std::runtime_error` is thrown with a specific error message.
- **Output**: The function does not return a value but will throw a `std::runtime_error` if it fails to set any of the specified locales.


---
### scope\_guard<!-- {{#callable:CLI::detail::CLI11_INLINE::scope_guard_t<F>::scope_guard}} -->
The `scope_guard` function creates a `scope_guard_t` object that ensures a given closure is executed when the object goes out of scope.
- **Inputs**:
    - `F &&closure`: A callable object (closure) that will be executed when the `scope_guard_t` object is destroyed.
- **Control Flow**:
    - The function takes a forwarding reference to a closure as its parameter.
    - It constructs a `scope_guard_t` object using the provided closure, forwarding the closure to the constructor of `scope_guard_t`.
    - The `scope_guard_t` object is returned, which will execute the closure upon its destruction.
- **Output**: A `scope_guard_t<F>` object that will execute the provided closure when it is destroyed.


---
### narrow\_impl<!-- {{#callable:CLI::detail::CLI11_DIAGNOSTIC_IGNORE_DEPRECATED::string::narrow_impl}} -->
The `narrow_impl` function converts a wide character string to a narrow (UTF-8) string, handling different platform and library support scenarios.
- **Inputs**:
    - `str`: A pointer to the wide character string to be converted.
    - `str_size`: The size of the wide character string to be converted.
- **Control Flow**:
    - Check if `CLI11_HAS_CODECVT` is defined to determine if `std::wstring_convert` can be used for conversion.
    - If on Windows and `CLI11_HAS_CODECVT` is defined, use `std::wstring_convert` with `std::codecvt_utf8_utf16<wchar_t>` to convert the string.
    - If not on Windows and `CLI11_HAS_CODECVT` is defined, use `std::wstring_convert` with `std::codecvt_utf8<wchar_t>` to convert the string.
    - If `CLI11_HAS_CODECVT` is not defined, ignore `str_size` and initialize a `std::mbstate_t` state object for conversion.
    - Store the current locale and set a new Unicode locale using [`set_unicode_locale`](#detailset_unicode_locale).
    - Calculate the size of the resulting narrow string using `std::wcsrtombs` and handle conversion errors by throwing a `std::runtime_error`.
    - Allocate a string of the calculated size and perform the conversion using `std::wcsrtombs`.
    - Restore the original locale using a scope guard.
- **Output**: A `std::string` containing the converted narrow (UTF-8) string.
- **Functions called**:
    - [`CLI::detail::CLI11_INLINE::scope_guard_t<F>::scope_guard`](#scope_guard_t<F>scope_guard)
    - [`CLI::detail::set_unicode_locale`](#detailset_unicode_locale)


---
### widen\_impl<!-- {{#callable:CLI::detail::std::wstring::widen_impl}} -->
The `widen_impl` function converts a narrow character string to a wide character string, handling different platform and locale settings.
- **Inputs**:
    - `str`: A pointer to the narrow character string to be converted.
    - `str_size`: The size of the narrow character string.
- **Control Flow**:
    - Check if `CLI11_HAS_CODECVT` is defined to determine the conversion method.
    - If on Windows and `CLI11_HAS_CODECVT` is defined, use `std::wstring_convert` with `std::codecvt_utf8_utf16` to convert the string.
    - If not on Windows and `CLI11_HAS_CODECVT` is defined, use `std::wstring_convert` with `std::codecvt_utf8` to convert the string.
    - If `CLI11_HAS_CODECVT` is not defined, ignore `str_size` and initialize a `std::mbstate_t` state object.
    - Store the current locale and set a new Unicode locale using `set_unicode_locale()`.
    - Calculate the size of the resulting wide string using `std::mbsrtowcs` and handle conversion errors by throwing a `std::runtime_error`.
    - Allocate a `std::wstring` of the calculated size and perform the conversion using `std::mbsrtowcs`.
    - Return the resulting wide string.
- **Output**: A `std::wstring` that represents the converted wide character string.
- **Functions called**:
    - [`CLI::detail::CLI11_INLINE::scope_guard_t<F>::scope_guard`](#scope_guard_t<F>scope_guard)
    - [`CLI::detail::set_unicode_locale`](#detailset_unicode_locale)


---
### narrow<!-- {{#callable:CLI::std::string::narrow}} -->
The `narrow` function converts a wide string (`std::wstring_view`) to a narrow string (`std::string`) using an implementation detail function.
- **Inputs**:
    - `str`: A `std::wstring_view` representing the wide string to be converted to a narrow string.
- **Control Flow**:
    - The function calls `detail::narrow_impl` with the data and size of the input wide string view.
    - The `narrow_impl` function handles the conversion of the wide string to a narrow string, potentially using different methods depending on the platform and availability of certain features like `std::codecvt`.
- **Output**: Returns a `std::string` that is the narrow string representation of the input wide string.


---
### widen<!-- {{#callable:CLI::std::wstring::widen}} -->
The `widen` function converts a `std::string_view` to a `std::wstring` by utilizing the `widen_impl` function from the `detail` namespace.
- **Inputs**:
    - `str`: A `std::string_view` representing the string to be converted to a wide string.
- **Control Flow**:
    - The function calls `detail::widen_impl` with the data and size of the input `std::string_view`.
- **Output**: A `std::wstring` that is the wide character representation of the input string.


---
### to\_path<!-- {{#callable:CLI::std::filesystem::path::to_path}} -->
The `to_path` function converts a string view to a `std::filesystem::path`, with special handling for Windows systems.
- **Inputs**:
    - `str`: A `std::string_view` representing the string to be converted into a `std::filesystem::path`.
- **Control Flow**:
    - The function checks if the code is being compiled on a Windows system using the `_WIN32` preprocessor directive.
    - If on Windows, it calls the [`widen`](#wstringwiden) function to convert the string view to a wide string before constructing the `std::filesystem::path`.
    - If not on Windows, it directly constructs the `std::filesystem::path` using the provided string view.
- **Output**: A `std::filesystem::path` object constructed from the input string view, with conversion to a wide string on Windows systems.
- **Functions called**:
    - [`CLI::std::wstring::widen`](#wstringwiden)


