# Purpose
This C++ source code file is a comprehensive test suite designed to validate the functionality of optional types in a command-line interface (CLI) application. The file includes tests for different implementations of optional types, such as `std::optional`, `std::experimental::optional`, and `boost::optional`, depending on the availability and configuration of the environment. The code is structured to conditionally include the appropriate headers and define macros to enable or disable support for these optional types. The tests are implemented using a testing framework, likely Catch2, as indicated by the use of `TEST_CASE` and `CHECK` macros.

The primary focus of the tests is to ensure that the CLI application correctly handles optional command-line arguments and flags. The tests cover a variety of scenarios, including handling of integers, vectors, complex numbers, and enums as optional values. Each test case method, such as `StdOptionalTest` or `BoostOptionalTest`, sets up a CLI application instance, adds options or flags, and verifies the expected behavior when different command-line arguments are provided. This file serves as a critical component in ensuring the robustness and correctness of the CLI application's handling of optional parameters across different optional type implementations.
# Imports and Dependencies

---
- `complex`
- `cstdint`
- `cstdlib`
- `iostream`
- `string`
- `vector`
- `app_helper.hpp`
- `boost/version.hpp`
- `optional`
- `experimental/optional`
- `boost/optional.hpp`
- `boost/optional/optional_io.hpp`


# Data Structures

---
### eval<!-- {{#data_structure:eval}} -->
- **Type**: `enum`
- **Members**:
    - `val0`: Represents the value 0 in the enumeration.
    - `val1`: Represents the value 1 in the enumeration.
    - `val2`: Represents the value 2 in the enumeration.
    - `val3`: Represents the value 3 in the enumeration.
    - `val4`: Represents the value 4 in the enumeration.
- **Description**: The `eval` enum class is a strongly-typed enumeration that defines a set of named integer constants ranging from 0 to 4. Each enumerator is associated with a specific character value, allowing for clear and type-safe representation of these values within the code. This enum is used in conjunction with `boost::optional` to provide optionality in handling these values.


