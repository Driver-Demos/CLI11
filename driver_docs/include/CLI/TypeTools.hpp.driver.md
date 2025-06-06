# Purpose
This C++ header file is part of the CLI11 library, which is a command-line interface parser for C++. The file provides a collection of utility functions and type traits that facilitate type checking, type conversion, and lexical casting. It includes several template structures and functions that mimic or extend standard C++ type traits, such as `enable_if_t`, `void_t`, and `conditional_t`, to ensure compatibility with older C++ standards like C++11 and C++14. The file also defines a variety of type traits to determine characteristics of types, such as whether a type is a boolean, a shared pointer, or a container, and provides mechanisms to convert between strings and various data types, including complex numbers and tuples.

The file is structured to support the broader functionality of the CLI11 library by enabling flexible and robust parsing of command-line arguments into user-defined types. It includes detailed implementations for checking if types can be streamed to or from streams, if they are constructible from other types, and if they can be converted to strings. Additionally, it provides mechanisms for handling complex data structures like tuples and containers, ensuring that the library can handle a wide range of user input scenarios. The file is intended to be included in other parts of the CLI11 library, as indicated by the `#pragma once` directive and the inclusion of other headers like "Encoding.hpp" and "StringTools.hpp".
# Imports and Dependencies

---
- `algorithm`
- `cmath`
- `cstdint`
- `exception`
- `limits`
- `memory`
- `string`
- `type_traits`
- `utility`
- `vector`
- `Encoding.hpp`
- `StringTools.hpp`


# Data Structures

---
### enabler<!-- {{#data_structure:CLI::detail::enabler}} -->
- **Type**: `enum`
- **Description**: The `enabler` is an empty scoped enumeration defined within the `CLI::detail` namespace, using `std::uint8_t` as its underlying type. It serves as a utility type for type enabling and is used in conjunction with `enable_if_t` to conditionally enable template functions. The `enabler` itself does not have any enumerators, and its primary purpose is to act as a tag or marker in template metaprogramming.


---
### make\_void<!-- {{#data_structure:CLI::make_void}} -->
- **Type**: `struct`
- **Members**:
    - `type`: Defines a type alias for `void`.
- **Description**: The `make_void` struct is a utility template structure that is used to define a type alias `type` as `void`. This is a common technique used in template metaprogramming to create a type that can be used in SFINAE (Substitution Failure Is Not An Error) contexts. It is essentially a reimplementation of the `std::void_t` from C++17, providing compatibility for earlier versions of C++.


---
### is\_bool<!-- {{#data_structure:CLI::is_bool}} -->
- **Type**: `struct`
- **Description**: The `is_bool` struct is a type trait used to determine if a given type is a boolean. By default, it inherits from `std::false_type`, indicating that the type is not a boolean. However, it is specialized for the `bool` type to inherit from `std::true_type`, indicating that the type is indeed a boolean. This struct is part of a set of utilities for type checking and manipulation, often used in template metaprogramming to enable or disable certain code paths based on type characteristics.
- **Inherits From**:
    - `std::false_type`


---
### is\_shared\_ptr<!-- {{#data_structure:CLI::is_shared_ptr}} -->
- **Type**: `struct`
- **Description**: The `is_shared_ptr` struct is a type trait used to determine if a given type is a `std::shared_ptr`. By default, it inherits from `std::false_type`, indicating that a type is not a `std::shared_ptr`. Specializations of this struct for `std::shared_ptr<T>` and `const std::shared_ptr<T>` inherit from `std::true_type`, indicating that these types are indeed `std::shared_ptr`. This type trait is useful for template metaprogramming, allowing developers to conditionally enable or disable functionality based on whether a type is a `std::shared_ptr`.
- **Inherits From**:
    - `std::false_type`


---
### is\_copyable\_ptr<!-- {{#data_structure:CLI::is_copyable_ptr}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constant boolean that indicates if the type T is either a shared pointer or a raw pointer.
- **Description**: The `is_copyable_ptr` struct is a type trait used to determine if a given type T is a copyable pointer. It checks if T is either a shared pointer (using the `is_shared_ptr` trait) or a raw pointer (using `std::is_pointer`). The result is stored in the static constant `value`, which is true if T is a copyable pointer and false otherwise. This trait is useful for template metaprogramming where operations need to be restricted to types that are pointers.


---
### IsMemberType<!-- {{#data_structure:CLI::IsMemberType}} -->
- **Type**: `struct`
- **Members**:
    - `type`: A type alias for the template parameter T.
- **Description**: The `IsMemberType` struct is a simple templated data structure that provides a type alias `type` for the template parameter T. It is designed to be specialized for specific types to override the type deduction for `IsMember`. In the provided code, there is a specialization for `const char*` which maps it to `std::string`, indicating its use in type transformation or type traits within the CLI library.


---
### is\_lexical\_castable<!-- {{#data_structure:CLI::adl_detail::is_lexical_castable}} -->
- **Type**: `class`
- **Members**:
    - `value`: A static constexpr boolean indicating if a lexical cast is possible between the specified types.
- **Description**: The `is_lexical_castable` class template is a type trait used to determine if a lexical cast operation is possible between two types, `T` and `S` (defaulting to `std::string`). It uses SFINAE (Substitution Failure Is Not An Error) to test if the `lexical_cast` function can be called with a constant reference to `S` and a reference to `T`. If the function call is valid, the `value` member is set to `true`, otherwise it is set to `false`. This class is part of the `adl_detail` namespace to avoid interference with other `lexical_cast` overloads.


---
### element\_type<!-- {{#data_structure:CLI::detail::element_type}} -->
- **Type**: `struct`
- **Members**:
    - `type`: Defines a type alias for the template parameter T.
- **Description**: The `element_type` struct is a template structure that provides a type alias named `type`, which is set to the template parameter `T`. This struct is used to define a generic way to access the type of an element, particularly in the context of type traits and template metaprogramming. It can be specialized to handle different types, such as pointers or containers, to deduce the underlying element type.


---
### element\_value\_type<!-- {{#data_structure:CLI::detail::element_value_type}} -->
- **Type**: `struct`
- **Members**:
    - `type`: Defines a type alias for the value type of the element type of T.
- **Description**: The `element_value_type` struct template is a utility that extracts the `value_type` from a given type `T`. It does this by first determining the `element_type` of `T` and then accessing its `value_type`. This is particularly useful in generic programming where you need to work with the underlying value type of containers or pointer-like types.


---
### pair\_adaptor<!-- {{#data_structure:CLI::detail::pair_adaptor}} -->
- **Type**: `struct`
- **Members**:
    - `value_type`: Defines the type of the value in the pair.
    - `first_type`: Represents the type of the first element in the pair, derived from value_type.
    - `second_type`: Represents the type of the second element in the pair, derived from value_type.
- **Description**: The `pair_adaptor` struct is a template-based utility designed to adapt set-like structures by providing a uniform interface for accessing elements as pairs. It inherits from `std::false_type` by default, indicating that the type does not inherently support pair-like access unless specialized. The struct defines `value_type`, `first_type`, and `second_type` to represent the types of the elements it adapts. It provides static methods `first` and `second` to access the first and second elements of a pair, respectively, although in this default implementation, both methods simply return the underlying value without modification. This struct is part of a larger framework for type manipulation and adaptation, allowing for flexible handling of different container types.
- **Member Functions**:
    - [`CLI::detail::pair_adaptor::first`](#pair_adaptorfirst)
    - [`CLI::detail::pair_adaptor::second`](#pair_adaptorsecond)
- **Inherits From**:
    - `std::false_type`

**Methods**

---
#### pair\_adaptor::first<!-- {{#callable:CLI::detail::pair_adaptor::first}} -->
The `first` function template forwards its input argument, `pair_value`, preserving its value category.
- **Inputs**:
    - `Q`: A template parameter representing the type of the input argument, which can be any type.
    - `pair_value`: An input argument of type `Q`, which is a universal reference that can bind to both lvalues and rvalues.
- **Control Flow**:
    - The function takes a single argument, `pair_value`, which is a universal reference.
    - It uses `std::forward` to forward `pair_value`, preserving its value category (lvalue or rvalue).
    - The function returns the result of `std::forward<Q>(pair_value)`.
- **Output**: The function returns the forwarded `pair_value`, preserving its original value category.
- **See also**: [`CLI::detail::pair_adaptor`](#pair_adaptor)  (Data Structure)


---
#### pair\_adaptor::second<!-- {{#callable:CLI::detail::pair_adaptor::second}} -->
The `second` function template forwards its input argument, `pair_value`, using `std::forward`, effectively returning the input as-is.
- **Inputs**:
    - `Q &&pair_value`: A universal reference to a value, which can be an lvalue or rvalue, that is intended to be forwarded.
- **Control Flow**:
    - The function takes a single template parameter `Q` and a universal reference `pair_value` as input.
    - It uses `std::forward` to forward `pair_value`, preserving its value category (lvalue or rvalue).
    - The function returns the result of `std::forward<Q>(pair_value)`, which is essentially the input `pair_value`.
- **Output**: The function returns the input `pair_value`, forwarded with its original value category preserved.
- **See also**: [`CLI::detail::pair_adaptor`](#pair_adaptor)  (Data Structure)



---
### is\_direct\_constructible<!-- {{#data_structure:CLI::detail::is_direct_constructible}} -->
- **Type**: `class`
- **Members**:
    - `value`: A static constexpr boolean indicating if type T can be directly constructed from type C.
- **Description**: The `is_direct_constructible` class template is a type trait used to determine if a type `T` can be directly constructed from a type `C`. It uses SFINAE (Substitution Failure Is Not An Error) to test if a temporary object of type `T` can be initialized with an object of type `C`. The result of this test is stored in the static member `value`, which is `true` if `T` can be directly constructed from `C`, and `false` otherwise. This trait is useful for compile-time checks in template metaprogramming to ensure type compatibility and constructibility.


---
### is\_ostreamable<!-- {{#data_structure:CLI::detail::is_ostreamable}} -->
- **Type**: `class`
- **Members**:
    - `value`: A static constexpr boolean that indicates if a type T can be streamed to an output stream of type S.
- **Description**: The `is_ostreamable` class is a type trait used to determine if a given type `T` can be output to a stream of type `S`, which defaults to `std::ostringstream`. It uses SFINAE (Substitution Failure Is Not An Error) to test if the expression `std::declval<SS &>() << std::declval<TT>()` is valid, where `SS` and `TT` are template parameters. If the expression is valid, the `value` member is set to `true`, otherwise it is set to `false`. This trait is useful for compile-time checks to ensure that a type can be used with output streams.


---
### is\_istreamable<!-- {{#data_structure:CLI::detail::is_istreamable}} -->
- **Type**: `class`
- **Members**:
    - `value`: A static constexpr boolean that indicates if a type T can be input-streamed using a stream of type S.
- **Description**: The `is_istreamable` class template is a type trait used to determine if a type `T` can be input-streamed using a stream of type `S`, which defaults to `std::istringstream`. It uses SFINAE (Substitution Failure Is Not An Error) to test if the expression `std::declval<SS &>() >> std::declval<TT &>()` is valid, indicating that `T` can be streamed from `S`. The result is stored in the static member `value`, which is `true` if the type is streamable and `false` otherwise.


---
### is\_complex<!-- {{#data_structure:CLI::detail::is_complex}} -->
- **Type**: `class`
- **Members**:
    - `value`: A static constexpr boolean that indicates if the type T has real and imag methods, suggesting it is a complex type.
- **Description**: The `is_complex` class template is a type trait used to determine if a given type T behaves like a complex number by checking for the presence of `real()` and `imag()` methods. It uses SFINAE (Substitution Failure Is Not An Error) to test if these methods exist for the type T, and sets the static member `value` to true if they do, otherwise false. This is useful for template metaprogramming where behavior needs to be specialized for complex number types.


---
### is\_mutable\_container<!-- {{#data_structure:CLI::detail::is_mutable_container}} -->
- **Type**: `struct`
- **Description**: The `is_mutable_container` is a type trait struct that inherits from `std::false_type` by default, indicating that a given type `T` is not a mutable container. This struct can be specialized to determine if a type is a mutable container, which is defined as having a `value_type`, an iterator, `clear`, `end` methods, and an `insert` function. It excludes types that can be constructed from `std::string` or `std::wstring`. This trait is useful for template metaprogramming to enable or disable functionality based on whether a type is a mutable container.
- **Inherits From**:
    - `std::false_type`


---
### is\_readable\_container<!-- {{#data_structure:CLI::detail::is_readable_container}} -->
- **Type**: `struct`
- **Description**: The `is_readable_container` is a type trait struct that is used to determine if a given type `T` is a readable container. By default, it inherits from `std::false_type`, indicating that the type is not a readable container. However, it can be specialized to inherit from `std::true_type` for types that meet the criteria of having `begin()` and `end()` methods, which are typical indicators of a container that can be iterated over.
- **Inherits From**:
    - `std::false_type`


---
### is\_wrapper<!-- {{#data_structure:CLI::detail::is_wrapper}} -->
- **Type**: `struct`
- **Description**: The `is_wrapper` struct is a type trait used to determine if a given type `T` is a wrapper type. By default, it inherits from `std::false_type`, indicating that the type is not a wrapper. This struct can be specialized to return `std::true_type` for specific types that are considered wrappers, typically those that have a `value_type` defined. It is part of a larger set of utilities for type checking and manipulation within the CLI namespace.
- **Inherits From**:
    - `std::false_type`


---
### is\_tuple\_like<!-- {{#data_structure:CLI::detail::is_tuple_like}} -->
- **Type**: `class`
- **Description**: The `is_tuple_like` class is a type trait used to determine if a given type `S` behaves like a tuple, meaning it has a `std::tuple_size` type trait defined. It uses SFINAE (Substitution Failure Is Not An Error) to test if the type `S` has a `std::tuple_size` and is not a complex type. The result is stored in a static constexpr boolean `value`, which is true if `S` is tuple-like and false otherwise.


---
### type\_count\_base<!-- {{#data_structure:CLI::detail::type_count_base}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constant integer initialized to 0.
- **Description**: The `type_count_base` is a templated struct that serves as a base for type counting operations. It is designed to be specialized for different types and conditions, with the default implementation providing a static constant integer `value` initialized to 0. This struct is part of a larger type trait system used to determine characteristics of types, such as whether they are tuple-like or container-like, and to calculate type sizes or counts.


---
### wrapped\_type<!-- {{#data_structure:CLI::detail::wrapped_type}} -->
- **Type**: `struct`
- **Members**:
    - `type`: Defines a type alias for the template parameter `def`.
- **Description**: The `wrapped_type` struct is a template structure that provides a mechanism to define a type alias based on a condition. It takes three template parameters: `T`, `def`, and `Enable`. By default, it uses the `def` type as the alias for `type`. This struct is typically used in template metaprogramming to provide a default type when certain conditions are not met, allowing for flexible type handling in generic programming.


---
### type\_count<!-- {{#data_structure:CLI::detail::type_count}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constant integer initialized to 0.
- **Description**: The `type_count` struct is a template structure that provides a mechanism to determine the type count of a given type `T`. By default, it sets a static constant integer `value` to 0, indicating that the type count is zero unless specialized otherwise. This struct is part of a larger type trait utility system, likely used to facilitate type introspection and manipulation in template metaprogramming.


---
### subtype\_count<!-- {{#data_structure:CLI::detail::subtype_count}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constexpr integer that determines the subtype count based on whether the type T is a mutable container or not.
- **Description**: The `subtype_count` struct template is a utility that calculates a static integer value representing the subtype count for a given type T. It uses type traits to determine if T is a mutable container, in which case it assigns a predefined maximum vector size, otherwise it uses the type count of T. This struct is part of a type utility system designed to facilitate type introspection and manipulation in C++.


---
### type\_count\_min<!-- {{#data_structure:CLI::detail::type_count_min}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constant integer initialized to 0.
- **Description**: The `type_count_min` struct is a template structure that provides a default implementation for a type trait, which is used to determine the minimum count of a particular type. It is a part of a larger type utility framework, and by default, it sets the `value` to 0, indicating that the minimum count for the unspecified type is zero. This struct can be specialized for specific types to provide a different minimum count value.


---
### subtype\_count\_min<!-- {{#data_structure:CLI::detail::subtype_count_min}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constexpr integer that determines the minimum subtype count based on the type T.
- **Description**: The `subtype_count_min` struct template is a compile-time utility that calculates the minimum subtype count for a given type T. It uses a static constexpr integer `value` to store the result, which is determined by checking if T is a mutable container. If T is a mutable container, it compares the type count of T with an expected maximum vector size and assigns the type count if it's less than the maximum, otherwise assigns 0. If T is not a mutable container, it assigns the minimum type count of T. This struct is part of a type trait system used to handle type introspection and manipulation in a generic programming context.


---
### expected\_count<!-- {{#data_structure:CLI::detail::expected_count}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constant integer initialized to 0.
- **Description**: The `expected_count` struct is a template structure that provides a default static constant integer value of 0. It is designed to be specialized for different types to potentially provide different expected counts, but in its default form, it simply holds a static constant integer `value` initialized to 0. This struct is part of a larger set of utilities for type manipulation and deduction, likely used in a library for command-line interface parsing or similar applications.


---
### object\_category<!-- {{#data_structure:CLI::detail::object_category}} -->
- **Type**: `enum`
- **Members**:
    - `char_value`: Represents a character value with an underlying value of 1.
    - `integral_value`: Represents a signed integral value with an underlying value of 2.
    - `unsigned_integral`: Represents an unsigned integral value with an underlying value of 4.
    - `enumeration`: Represents an enumeration type with an underlying value of 6.
    - `boolean_value`: Represents a boolean value with an underlying value of 8.
    - `floating_point`: Represents a floating-point value with an underlying value of 10.
    - `number_constructible`: Represents a type that can be constructed from a number with an underlying value of 12.
    - `double_constructible`: Represents a type that can be constructed from a double with an underlying value of 14.
    - `integer_constructible`: Represents a type that can be constructed from an integer with an underlying value of 16.
    - `string_assignable`: Represents a type that can be assigned from a string with an underlying value of 23.
    - `string_constructible`: Represents a type that can be constructed from a string with an underlying value of 24.
    - `wstring_assignable`: Represents a type that can be assigned from a wide string with an underlying value of 25.
    - `wstring_constructible`: Represents a type that can be constructed from a wide string with an underlying value of 26.
    - `other`: Represents other types not specifically categorized with an underlying value of 45.
    - `wrapper_value`: Represents a special wrapper type with an underlying value of 50.
    - `complex_number`: Represents a complex number type with an underlying value of 60.
    - `tuple_value`: Represents a tuple type with an underlying value of 70.
    - `container_value`: Represents a container type with an underlying value of 80.
- **Description**: The `object_category` enum class categorizes different types of objects based on their characteristics and capabilities, such as whether they are integral, floating-point, string-like, or container types. Each category is represented by a unique underlying `std::uint8_t` value, allowing for efficient type classification and enabling type-specific operations within the software. This enum is particularly useful in scenarios where type traits and type-based logic are required, such as in template metaprogramming or type deduction.


---
### classify\_object<!-- {{#data_structure:CLI::detail::classify_object}} -->
- **Type**: `struct`
- **Members**:
    - `value`: A static constexpr member that holds the object category, defaulting to `object_category::other`.
- **Description**: The `classify_object` struct template is a utility for categorizing objects based on their type traits. It uses template specialization to determine the category of an object, such as integral, floating point, or other types, and assigns a corresponding `object_category` value. By default, it categorizes objects as `object_category::other`, but this can be overridden by specializing the template for specific types.


---
### uncommon\_type<!-- {{#data_structure:CLI::detail::uncommon_type}} -->
- **Type**: `struct`
- **Members**:
    - `type`: A nested type that evaluates to std::true_type if T is an uncommon type, otherwise std::false_type.
    - `value`: A static constexpr boolean that holds the value of type::value, indicating if T is an uncommon type.
- **Description**: The `uncommon_type` struct is a type trait used to determine if a given type T is considered 'uncommon' based on a set of conditions. Specifically, it checks if T is not a floating point, integral, string-assignable, string-constructible, complex, mutable container, or enum type. If T meets all these conditions, `type` is defined as `std::true_type`, otherwise as `std::false_type`. The `value` member provides a convenient boolean representation of this evaluation.


# Functions

---
### first<!-- {{#callable:CLI::detail::first}} -->
The `first` function template retrieves the first element of a pair-like object using perfect forwarding.
- **Inputs**:
    - `Q`: A template parameter representing a pair-like object, which can be a tuple or a pair, passed by universal reference.
- **Control Flow**:
    - The function uses `std::forward` to perfectly forward the `pair_value` to `std::get<0>`, ensuring that the value category of the argument is preserved.
    - `std::get<0>` is used to access the first element of the pair-like object.
- **Output**: The function returns the first element of the pair-like object, with the same type and value category as the original element.


---
### second<!-- {{#callable:CLI::detail::second}} -->
The `second` function template retrieves the second element from a pair-like structure using perfect forwarding.
- **Inputs**:
    - `Q`: A universal reference to a pair-like object from which the second element is to be retrieved.
- **Control Flow**:
    - The function uses `std::forward` to perfectly forward the input `pair_value` to `std::get<1>`.
    - `std::get<1>` is used to access the second element of the pair-like object.
- **Output**: The function returns the second element of the input pair-like object, with the type deduced by `decltype`.


---
### from\_stream<!-- {{#callable:CLI::detail::from_stream}} -->
The `from_stream` function template returns `false` for types that are not input-streamable.
- **Inputs**:
    - `istring`: A constant reference to a `std::string` representing the input string to be parsed.
    - `obj`: A reference to an object of type `T` where the parsed result would be stored if parsing were possible.
- **Control Flow**:
    - The function is a template specialized for types `T` that are not input-streamable, as determined by the `is_istreamable` type trait.
    - The function immediately returns `false`, indicating that the conversion from the string to the object is not possible for non-input-streamable types.
- **Output**: A boolean value `false`, indicating that the conversion from the string to the object is not possible for non-input-streamable types.


---
### to\_string<!-- {{#callable:CLI::detail::to_string}} -->
The `to_string` function converts a tuple-like object with at least two elements into a string representation enclosed in square brackets.
- **Inputs**:
    - `T &&value`: A tuple-like object that is not convertible to or constructible from a std::string, not ostreamable, and has at least two elements.
- **Control Flow**:
    - Check if the type T is not convertible to std::string, not constructible from std::string, not ostreamable, is tuple-like, and has at least two elements using enable_if_t.
    - Create a string starting with '[' and append the string representation of the first element of the tuple using `tuple_value_string<T, 0>(value)`.
    - Append ']' to the string to close the bracket.
    - Return the constructed string.
- **Output**: A std::string representing the tuple-like object, enclosed in square brackets.


---
### tuple\_value\_string<!-- {{#callable:CLI::detail::tuple_value_string}} -->
The `tuple_value_string` function recursively converts each element of a tuple to a string and concatenates them with commas, removing any trailing comma.
- **Inputs**:
    - `T`: A tuple-like object whose elements are to be converted to a string.
    - `I`: The current index of the tuple element being processed, starting from 0.
    - `value`: The tuple-like object passed to the function, which is being processed to generate a string representation.
- **Control Flow**:
    - The function checks if the current index I is less than the number of elements in the tuple using `std::enable_if` and `type_count_base<T>::value`.
    - It retrieves the I-th element of the tuple using `std::get<I>(value)` and converts it to a string using [`to_string`](#to_string).
    - The function concatenates the string representation of the current element with a comma and the result of a recursive call to `tuple_value_string` with the next index (I + 1).
    - If the resulting string ends with a comma, it removes the trailing comma using `str.pop_back()`.
    - Finally, the function returns the constructed string.
- **Output**: A string representing the concatenated string values of the tuple elements, separated by commas.
- **Functions called**:
    - [`CLI::detail::to_string`](#to_string)


---
### checked\_to\_string<!-- {{#callable:CLI::detail::checked_to_string}} -->
The `checked_to_string` function template returns an empty string if the two template types `T1` and `T2` are not the same.
- **Inputs**:
    - `T1`: The first template type parameter used for type comparison.
    - `T2`: The second template type parameter used for type comparison.
    - `T`: The type of the input argument, which is a forwarding reference.
- **Control Flow**:
    - The function checks if `T1` and `T2` are not the same using `std::is_same<T1, T2>::value`.
    - If `T1` and `T2` are not the same, the function returns an empty `std::string`.
- **Output**: An empty `std::string` is returned if `T1` and `T2` are not the same.


---
### value\_string<!-- {{#callable:CLI::detail::value_string}} -->
The `value_string` function converts a non-enum, non-arithmetic type to a string using the `to_string` function.
- **Inputs**:
    - `T`: A template parameter representing the type of the input value, which must not be an enum or arithmetic type.
    - `value`: A constant reference to an object of type T, which is the value to be converted to a string.
- **Control Flow**:
    - The function template is enabled only for types T that are neither enum nor arithmetic types, using SFINAE (Substitution Failure Is Not An Error) with `enable_if_t`.
    - The function attempts to convert the input `value` to a string by calling the `to_string` function, which must be defined for the type T.
- **Output**: The function returns the result of `to_string(value)`, which is a string representation of the input value.


---
### tuple\_type\_size<!-- {{#callable:CLI::detail::tuple_type_size}} -->
The `tuple_type_size` function calculates the sum of subtype counts for each element in a tuple-like type, starting from a specified index.
- **Inputs**:
    - `T`: A tuple-like type whose elements' subtype counts are to be summed.
    - `I`: The starting index in the tuple-like type from which to begin summing subtype counts.
- **Control Flow**:
    - The function checks if the index I is less than the total number of elements in the tuple-like type T using `type_count_base<T>::value`.
    - If the condition is true, it calculates the subtype count of the element at index I using `subtype_count<typename std::tuple_element<I, T>::type>::value`.
    - It then recursively calls itself with the next index (I + 1) and adds the result to the current subtype count.
    - If the condition is false (i.e., I is equal to the number of elements), the function returns 0, terminating the recursion.
- **Output**: An integer representing the sum of subtype counts for each element in the tuple-like type starting from index I.


---
### tuple\_type\_size\_min<!-- {{#callable:CLI::detail::tuple_type_size_min}} -->
The `tuple_type_size_min` function calculates the minimum sum of subtype counts for each element in a tuple-like type starting from a given index.
- **Inputs**:
    - `T`: A tuple-like type whose elements' subtype counts are to be summed.
    - `I`: The starting index in the tuple from which to begin summing subtype counts.
- **Control Flow**:
    - The function checks if the index `I` is less than the number of types in the tuple `T` using `type_count_base<T>::value`.
    - If `I` is less than the number of types, it recursively calls `tuple_type_size_min` for the next index `I + 1`.
    - It adds the minimum subtype count of the current element type `std::tuple_element<I, T>::type` to the result of the recursive call.
- **Output**: An integer representing the sum of minimum subtype counts for each element in the tuple starting from index `I`.


---
### type\_name<!-- {{#callable:CLI::detail::type_name}} -->
The `type_name` function template returns the type name of the value type of a container or wrapper type as a string.
- **Inputs**:
    - `T`: A template parameter representing a type that is either a container or a wrapper, as determined by the `classify_object` type trait.
- **Control Flow**:
    - The function is enabled only if the type `T` is classified as either a container or a wrapper using the `classify_object` type trait.
    - The function returns the result of calling `type_name` recursively on the `value_type` of `T`.
- **Output**: A `std::string` representing the type name of the `value_type` of the container or wrapper type `T`.


---
### tuple\_name<!-- {{#callable:CLI::detail::tuple_name}} -->
The `tuple_name` function recursively generates a comma-separated string representation of the types of elements in a tuple.
- **Inputs**:
    - `T`: A tuple type whose element types are to be converted to a string.
    - `I`: The current index in the tuple, starting from 0, used for recursion.
- **Control Flow**:
    - The function checks if the current index `I` is less than the number of types in the tuple `T` using `type_count_base<T>::value`.
    - If the condition is true, it retrieves the type name of the `I`-th element in the tuple using `type_name` and appends it to a string, followed by a comma.
    - The function then recursively calls itself with the next index `I + 1` to process the next element type.
    - After the recursive call, if the last character in the string is a comma, it is removed to ensure the string does not end with a comma.
    - The function returns the constructed string.
- **Output**: A string representing the types of the elements in the tuple, separated by commas.


---
### integral\_conversion<!-- {{#callable:CLI::detail::integral_conversion}} -->
The [`integral_conversion`](#integral_conversion) function attempts to convert a string representation of a number into a signed integral type, handling various formats and edge cases.
- **Inputs**:
    - `input`: A constant reference to a `std::string` that represents the number to be converted.
    - `output`: A reference to a variable of type `T` (which must be a signed integral type) where the converted value will be stored.
- **Control Flow**:
    - Check if the input string is empty and return false if it is.
    - Use `std::strtoll` to attempt conversion of the string to a 64-bit signed integer, checking for range errors.
    - If conversion is successful and the entire string was consumed, cast the result to type `T` and return true.
    - Handle special case where input is "true" by setting output to 1 and returning true.
    - If the input contains group separators, remove them and recursively call [`integral_conversion`](#integral_conversion).
    - Trim trailing whitespace and recursively call [`integral_conversion`](#integral_conversion) if necessary.
    - Handle octal and binary number formats by checking prefixes and using appropriate base in `std::strtoll`.
    - Return false if none of the conditions for successful conversion are met.
- **Output**: Returns a boolean indicating whether the conversion was successful, with the result stored in the `output` parameter if successful.
- **Functions called**:
    - [`CLI::detail::std::string::get_group_separators`](impl/StringTools_inl.hpp.driver.md#stringget_group_separators)
    - [`CLI::detail::integral_conversion`](#integral_conversion)
    - [`CLI::detail::trim_copy`](StringTools.hpp.driver.md#trim_copy)


---
### to\_flag\_value<!-- {{#callable:CLI::detail::to_flag_value}} -->
The `to_flag_value` function converts a string representation of a flag into an integer value, returning 1 for true-like values, -1 for false-like values, and attempting to parse numeric values otherwise.
- **Inputs**:
    - `val`: A string representing a flag or numeric value to be converted to an integer.
- **Control Flow**:
    - Check if the input string `val` is equal to "true" or "false" and return 1 or -1 respectively.
    - Convert the input string to lowercase using `detail::to_lower`.
    - If the string length is 1, check if it is a digit between '1' and '9' and return its integer value.
    - For single character strings, use a switch statement to return 1 for 't', 'y', '+', and -1 for '0', 'f', 'n', '-'.
    - If the string matches "on", "yes", "enable", return 1; if it matches "off", "no", "disable", return -1.
    - Attempt to convert the string to a long long integer using `std::strtoll`, setting `errno` to `EINVAL` if conversion fails.
- **Output**: Returns an integer value representing the flag: 1 for true-like values, -1 for false-like values, or a numeric conversion of the string if possible.


---
### lexical\_cast<!-- {{#callable:CLI::detail::lexical_cast}} -->
The `lexical_cast` function template provides a fallback mechanism for converting a string to a non-standard type that lacks a user-defined lexical cast overload or streaming input operator.
- **Inputs**:
    - `input`: A constant reference to a `std::string` representing the input string to be converted.
    - `output`: A reference to an object of type `T` where the converted value will be stored.
- **Control Flow**:
    - The function is a template specialized for types classified as `object_category::other` that are not assignable from an `int`, not streamable, and not user-defined lexical castable.
    - A static assertion is used to ensure that the function is only instantiated for types that do not have a lexical cast overload or streaming input operator defined.
    - The function immediately returns `false`, indicating that the conversion is not possible.
- **Output**: The function returns a boolean value `false`, indicating that the conversion was unsuccessful.


---
### lexical\_assign<!-- {{#callable:CLI::detail::lexical_assign}} -->
The `lexical_assign` function attempts to convert a string input into a specified output type using a temporary conversion type, handling cases where direct assignment is not possible.
- **Inputs**:
    - `input`: A constant reference to a `std::string` that represents the input data to be converted.
    - `output`: A reference to an `AssignTo` type variable where the converted value will be stored.
- **Control Flow**:
    - Initialize a `ConvertTo` type variable `val` to its default value.
    - Check if the input string is empty; if so, set `parse_result` to true, otherwise attempt to convert the input string to `val` using [`lexical_cast`](#lexical_cast).
    - If `parse_result` is true, assign `val` to `output` using the constructor of `AssignTo` to allow implicit conversions.
    - Return `parse_result` indicating whether the conversion was successful.
- **Output**: Returns a boolean indicating whether the conversion from the input string to the output type was successful.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](#lexical_cast)


---
### lexical\_conversion<!-- {{#callable:CLI::detail::lexical_conversion}} -->
The `lexical_conversion` function attempts to convert a vector of strings into a specified output type using a template-based approach, particularly for wrapper types that are not directly assignable.
- **Inputs**:
    - `strings`: A constant reference to a vector of strings that represents the input data to be converted.
    - `output`: A reference to the output variable of type `AssignTo` where the converted value will be stored.
- **Control Flow**:
    - Check if the input vector `strings` is empty or its first element is empty; if so, assign a default-constructed `ConvertType` to `output` and return true.
    - Declare a variable `val` of type `ConvertType` to hold the intermediate conversion result.
    - Call `lexical_conversion` recursively with `ConvertTo::value_type` to attempt conversion of `strings` into `val`.
    - If the recursive conversion is successful, assign `val` to `output` and return true.
    - If the conversion fails, return false.
- **Output**: A boolean value indicating whether the conversion was successful.


---
### tuple\_conversion<!-- {{#callable:CLI::detail::tuple_conversion}} -->
The `tuple_conversion` function recursively converts a vector of strings into a tuple-like structure by converting each string to the appropriate type and assigning it to the corresponding element in the output tuple.
- **Inputs**:
    - `strings`: A vector of strings that need to be converted and assigned to the elements of the output tuple.
    - `output`: A reference to the tuple-like structure where the converted values from the strings will be stored.
- **Control Flow**:
    - The function checks if the index I is less than the number of elements in the AssignTo type using `std::enable_if` to ensure the function is only instantiated for valid indices.
    - It initializes a boolean `retval` to true, which will be used to track the success of the conversion process.
    - The function determines the type of the current element in the ConvertTo type using `std::conditional` and `std::tuple_element`.
    - If the strings vector is not empty, it attempts to convert the current string to the appropriate type and assigns it to the corresponding element in the output tuple using `tuple_type_conversion`.
    - The function recursively calls itself with the next index (I + 1) to process the next element in the tuple.
    - The result of the recursive call is combined with the current `retval` using logical AND to ensure all conversions are successful.
    - Finally, the function returns the boolean `retval` indicating the success of the entire conversion process.
- **Output**: A boolean value indicating whether the conversion of all strings to the tuple elements was successful.


---
### tuple\_type\_conversion<!-- {{#callable:CLI::detail::tuple_type_conversion}} -->
The `tuple_type_conversion` function converts a subset of a vector of strings into a specified output type using lexical conversion, while handling separators and adjusting the input vector accordingly.
- **Inputs**:
    - `strings`: A reference to a vector of strings that serves as the input data to be converted.
    - `output`: A reference to the output variable of type `AssignTo` where the converted data will be stored.
- **Control Flow**:
    - Initialize `index` to the minimum subtype count of `ConvertTo` and `mx_count` to the subtype count of `ConvertTo`.
    - Calculate `mx` as the minimum of `mx_count` and the size of `strings` minus one.
    - Iterate over `strings` starting from `index` until `mx`, checking for a separator using [`is_separator`](StringTools.hpp.driver.md#is_separator); break if found.
    - Perform lexical conversion on the subset of `strings` up to `index` and store the result in `output`.
    - If `strings` has more elements than `index`, erase the processed elements and the separator; otherwise, clear `strings`.
    - Return the result of the lexical conversion as a boolean.
- **Output**: A boolean indicating whether the lexical conversion was successful.
- **Functions called**:
    - [`CLI::detail::is_separator`](StringTools.hpp.driver.md#is_separator)


---
### sum\_string\_vector<!-- {{#callable:CLI::detail::sum_string_vector}} -->
The `sum_string_vector` function attempts to sum a vector of strings as numerical values and returns the sum as a string, or concatenates the strings if any conversion fails.
- **Inputs**:
    - `values`: A constant reference to a vector of strings that are to be summed or concatenated.
- **Control Flow**:
    - Initialize a double `val` to 0.0 and a boolean `fail` to false.
    - Iterate over each string `arg` in the `values` vector.
    - Attempt to convert `arg` to a double `tv` using [`lexical_cast`](#lexical_cast).
    - If conversion fails, reset `errno` and attempt to convert `arg` to a flag value using `detail::to_flag_value`.
    - Set `fail` to true and break the loop if `errno` is non-zero after flag conversion.
    - Add `tv` to `val` if conversion is successful.
    - If `fail` is true, concatenate all strings in `values` into `output`.
    - If `fail` is false, convert `val` to a string with 16 decimal precision and assign it to `output`.
- **Output**: A string representing either the sum of the numerical values of the input strings or the concatenated input strings if any conversion fails.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](#lexical_cast)


