# Purpose
This C++ header file provides narrow functionality focused on string conversion utilities within the `CLI` namespace. It defines inline functions for converting between wide and narrow strings, which are essential for handling different character encodings in C++ applications. The code includes conditional compilation directives to support C++17 features, such as `std::string_view`, and filesystem path conversions when available. The use of `#pragma once` and inclusion guards ensures that the header is only included once per compilation unit, preventing redefinition errors. This file is intended to be included in other C++ source files, as indicated by the inclusion of "impl/Encoding_inl.hpp" for implementation details, suggesting it is part of a larger library, likely related to command-line interface (CLI) utilities.
# Imports and Dependencies

---
- `Macros.hpp`
- `string`
- `string_view`
- `filesystem`
- `impl/Encoding_inl.hpp`


