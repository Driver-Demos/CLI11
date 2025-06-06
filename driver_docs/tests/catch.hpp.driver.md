# Purpose
This C++ header file is designed to facilitate unit testing by integrating with the Catch2 testing framework. It provides narrow functionality, specifically tailored for use in test environments where Catch2 is employed. The code conditionally includes different sets of Catch2 headers and sets up convenient aliases for commonly used Catch2 components, such as matchers and generators, depending on whether the `CLI11_CATCH3` macro is defined. This allows for flexibility in supporting different versions of Catch2. The use of `#pragma once` ensures the file is included only once per compilation, preventing duplicate definitions. Overall, this header file is intended to be imported into other C++ files to streamline the process of writing and managing tests.
# Imports and Dependencies

---
- `string`
- `catch2/catch_approx.hpp`
- `catch2/catch_template_test_macros.hpp`
- `catch2/catch_test_macros.hpp`
- `catch2/generators/catch_generators.hpp`
- `catch2/generators/catch_generators_range.hpp`
- `catch2/matchers/catch_matchers_floating_point.hpp`
- `catch2/matchers/catch_matchers_string.hpp`
- `catch2/catch.hpp`


# Functions

---
### Contains<!-- {{#callable:Contains}} -->
The `Contains` function returns a Catch2 matcher that checks if a given string contains a specified substring.
- **Inputs**:
    - `x`: A constant reference to a `std::string` representing the substring to be checked for containment.
- **Control Flow**:
    - The function is defined inline, meaning it is expanded in place where it is called, rather than being invoked through a function call.
    - It uses the Catch2 library's `ContainsSubstring` matcher to create a matcher object that can be used in test assertions to verify if a string contains the specified substring.
- **Output**: A Catch2 matcher object that can be used to check if a string contains the specified substring.


