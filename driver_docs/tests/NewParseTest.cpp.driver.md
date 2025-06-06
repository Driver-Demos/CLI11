# Purpose
This C++ source code file is a comprehensive test suite designed to validate the functionality of a command-line interface (CLI) application, specifically focusing on the parsing and handling of complex data types and custom data structures. The file utilizes the Catch2 testing framework to define multiple test cases, each encapsulated within the `TEST_CASE_METHOD` macro, which leverages a fixture class `TApp` to set up the testing environment. The primary focus of these tests is to ensure that the application can correctly parse and handle complex numbers, custom string pairs, and various wrapped data types, including those with custom conversion logic.

The code includes tests for parsing complex numbers with different formats and delimiters, ensuring that both real and imaginary parts are correctly interpreted. It also tests custom conversion functions for user-defined types like [`spair`](#spairspair), [`badlywrapped`](#badlywrappedbadlywrapped), and [`anotherstring`](#anotherstringanotherstring), demonstrating the flexibility of the CLI library in handling non-standard data types. The file further explores the use of template classes and type traits to enforce specific construction and assignment rules, ensuring robust type safety and conversion handling. Overall, this file serves as a critical component in validating the robustness and flexibility of the CLI application's parsing capabilities, ensuring it can handle a wide range of input scenarios and data types.
# Imports and Dependencies

---
- `app_helper.hpp`
- `complex`
- `cstdint`
- `string`
- `utility`
- `vector`


# Data Structures

---
### spair<!-- {{#data_structure:spair}} -->
- **Type**: `class`
- **Members**:
    - `first`: A string representing the first element of the pair.
    - `second`: A string representing the second element of the pair.
- **Description**: The `spair` class is a simple data structure designed to hold a pair of strings. It provides a default constructor and a parameterized constructor for initializing the two string members, `first` and `second`. This class is useful for testing lexical cast and conversions, as demonstrated in the provided code.
- **Member Functions**:
    - [`spair::spair`](#spairspair)
    - [`spair::spair`](#spairspair)

**Methods**

---
#### spair::spair<!-- {{#callable:spair::spair}} -->
The `spair` constructor initializes an `spair` object with two strings, moving the input strings into the object's `first` and `second` members.
- **Inputs**:
    - `s1`: A `std::string` representing the first string to be stored in the `spair` object.
    - `s2`: A `std::string` representing the second string to be stored in the `spair` object.
- **Control Flow**:
    - The constructor is called with two `std::string` arguments, `s1` and `s2`.
    - The `std::move` function is used to move `s1` into the `first` member of the `spair` object, avoiding unnecessary copying.
    - Similarly, `std::move` is used to move `s2` into the `second` member of the `spair` object.
- **Output**: An `spair` object with its `first` and `second` members initialized to the moved values of `s1` and `s2`, respectively.
- **See also**: [`spair`](#spair)  (Data Structure)


---
#### spair::spair<!-- {{#callable:spair::spair}} -->
The `spair` constructor initializes an `spair` object with two strings, moving the input strings into the object's `first` and `second` members.
- **Inputs**:
    - `s1`: A `std::string` representing the first string to be stored in the `spair` object.
    - `s2`: A `std::string` representing the second string to be stored in the `spair` object.
- **Control Flow**:
    - The constructor takes two `std::string` arguments, `s1` and `s2`.
    - It uses `std::move` to transfer ownership of `s1` and `s2` to the `first` and `second` members of the `spair` object, respectively.
- **Output**: An `spair` object with its `first` and `second` members initialized to the values of `s1` and `s2`, respectively.
- **See also**: [`spair`](#spair)  (Data Structure)



---
### badlywrapped<!-- {{#data_structure:badlywrapped}} -->
- **Type**: `class`
- **Members**:
    - `value`: A private member variable of type T that stores the value wrapped by the class.
- **Description**: The `badlywrapped` class is a template class that acts as a simple wrapper around a single value of type T. It provides a basic interface with a constructor to initialize the value, a `get` method to retrieve the value, and a `set` method to update the value. The class is designed to encapsulate a value and provide controlled access to it, although its interface is described as inconvenient, possibly due to its simplicity or lack of additional functionality.
- **Member Functions**:
    - [`badlywrapped::badlywrapped`](#badlywrappedbadlywrapped)
    - [`badlywrapped::get`](#badlywrappedget)
    - [`badlywrapped::set`](#badlywrappedset)

**Methods**

---
#### badlywrapped::badlywrapped<!-- {{#callable:badlywrapped::badlywrapped}} -->
The `badlywrapped` constructor initializes an instance of the `badlywrapped` class with a default value.
- **Inputs**: None
- **Control Flow**:
    - The constructor initializes the private member `value` using its default constructor.
- **Output**: An instance of the `badlywrapped` class with its `value` member initialized to its default state.
- **See also**: [`badlywrapped`](#badlywrapped)  (Data Structure)


---
#### badlywrapped::get<!-- {{#callable:badlywrapped::get}} -->
The `get` function returns the current value stored in the `badlywrapped` class template.
- **Inputs**: None
- **Control Flow**:
    - The function is a simple getter that directly returns the private member `value` of the `badlywrapped` class.
    - It is marked as `const`, indicating it does not modify the state of the object.
- **Output**: The function returns the value of type `T` stored in the `value` member variable of the `badlywrapped` class.
- **See also**: [`badlywrapped`](#badlywrapped)  (Data Structure)


---
#### badlywrapped::set<!-- {{#callable:badlywrapped::set}} -->
The `set` function assigns a given value to the private member variable `value` of the `badlywrapped` class.
- **Inputs**:
    - `val`: A value of type `T` that will be assigned to the private member variable `value`.
- **Control Flow**:
    - The function takes a single argument `val` of type `T`.
    - It assigns the value of `val` to the private member variable `value`.
- **Output**: The function does not return any value.
- **See also**: [`badlywrapped`](#badlywrapped)  (Data Structure)



---
### anotherstring<!-- {{#data_structure:anotherstring}} -->
- **Type**: `struct`
- **Members**:
    - `s`: A string member that holds a std::string object.
- **Description**: The `anotherstring` struct is a simple wrapper around a `std::string` object, providing a default constructor and a single member `s` to store the string. It is used in conjunction with custom converters to extend parsing options in the CLI library, specifically by specializing the `lexical_cast` function to append an exclamation mark to the string when converted.
- **Member Functions**:
    - [`anotherstring::anotherstring`](#anotherstringanotherstring)

**Methods**

---
#### anotherstring::anotherstring<!-- {{#callable:anotherstring::anotherstring}} -->
The `anotherstring` constructor initializes an instance of the `anotherstring` struct with a default constructor and an empty string member `s`.
- **Inputs**: None
- **Control Flow**:
    - The constructor `anotherstring()` is defined as `default`, meaning it uses the compiler-generated default constructor.
    - The member `s` is initialized as an empty `std::string`.
- **Output**: An instance of the `anotherstring` struct with its member `s` initialized to an empty string.
- **See also**: [`anotherstring`](#anotherstring)  (Data Structure)



---
### yetanotherstring<!-- {{#data_structure:yetanotherstring}} -->
- **Type**: `struct`
- **Members**:
    - `s`: A standard string member to hold string data.
- **Description**: The `yetanotherstring` struct is a simple wrapper around a standard C++ string, providing a default constructor and a single member `s` of type `std::string`. This struct is likely used to facilitate custom string handling or conversion operations, as indicated by its use in conjunction with a custom `lexical_cast` function that enables specific parsing behavior for this type.
- **Member Functions**:
    - [`yetanotherstring::yetanotherstring`](#yetanotherstringyetanotherstring)

**Methods**

---
#### yetanotherstring::yetanotherstring<!-- {{#callable:yetanotherstring::yetanotherstring}} -->
The `yetanotherstring` constructor initializes an instance of the `yetanotherstring` struct with a default empty string.
- **Inputs**: None
- **Control Flow**:
    - The constructor `yetanotherstring()` is defined with the `= default` specifier, indicating that it uses the default behavior provided by the compiler.
    - The member variable `s` is initialized as an empty `std::string`.
- **Output**: An instance of the `yetanotherstring` struct with its member `s` initialized to an empty string.
- **See also**: [`yetanotherstring`](#yetanotherstring)  (Data Structure)



---
### is\_my\_lexical\_cast\_enabled<!-- {{#data_structure:is_my_lexical_cast_enabled}} -->
- **Type**: `struct`
- **Description**: The `is_my_lexical_cast_enabled` is a template struct that inherits from `std::false_type`, which means it defaults to `false` for any type `T`. This struct is used as a trait to enable or disable custom lexical casting for specific types. By default, it is disabled for all types, but it can be specialized for specific types to enable custom behavior, as seen in the code where it is specialized for `yetanotherstring` to enable lexical casting.
- **Inherits From**:
    - `std::false_type`


---
### objWrapper<!-- {{#data_structure:objWrapper}} -->
- **Type**: `class`
- **Members**:
    - `val_`: A private member variable of type X that stores the wrapped object.
- **Description**: The `objWrapper` class is a template class designed to wrap an object of any type X, providing a controlled interface for construction and assignment. It includes a default constructor, a move constructor, and a copy constructor, while explicitly deleting constructors and assignment operators for other types to prevent unintended conversions. The class provides a method to access the wrapped value, ensuring encapsulation and controlled access to the underlying object.
- **Member Functions**:
    - [`objWrapper::objWrapper`](#objWrapperobjWrapper)
    - [`objWrapper::objWrapper`](#objWrapperobjWrapper)
    - [`objWrapper::objWrapper`](#objWrapperobjWrapper)
    - [`objWrapper::objWrapper`](#objWrapperobjWrapper)
    - [`objWrapper::operator=`](#objWrapperoperator)
    - [`objWrapper::operator=`](#objWrapperoperator)
    - [`objWrapper::value`](#objWrappervalue)

**Methods**

---
#### objWrapper::objWrapper<!-- {{#callable:objWrapper::objWrapper}} -->
The `objWrapper` class template provides a wrapper for an object of type `X`, with specific constructors and assignment operators to control how objects are constructed and assigned.
- **Inputs**:
    - `X`: The type of the object to be wrapped by the `objWrapper` class.
    - `obj`: An object of type `X` to be wrapped by the `objWrapper` class.
- **Control Flow**:
    - The default constructor `objWrapper()` initializes an empty `objWrapper` object.
    - The explicit constructor `objWrapper(X obj)` initializes the `objWrapper` with the given object `obj`, using `std::move` to transfer ownership.
    - The copy constructor `objWrapper(const objWrapper &ow)` is defaulted, allowing for copying of `objWrapper` objects.
    - A template constructor `objWrapper(const TT &obj)` is deleted to prevent construction from types other than `X`.
    - The copy assignment operator `operator=(const objWrapper &)` is defaulted, allowing for assignment from another `objWrapper` of the same type.
    - The move assignment operator `operator=(objWrapper &&)` is defaulted, allowing for move assignment from another `objWrapper` of the same type, but without `noexcept` due to GCC 4.8 limitations.
    - A template assignment operator `operator=(TT &&obj)` is deleted to prevent assignment from types other than `X`.
- **Output**: The class provides a method `value()` that returns a constant reference to the wrapped object of type `X`.
- **See also**: [`objWrapper`](#objWrapper)  (Data Structure)


---
#### objWrapper::objWrapper<!-- {{#callable:objWrapper::objWrapper}} -->
The `objWrapper` class template is a simple wrapper for an object of type `X`, providing specific constructors and assignment operators to control object management.
- **Inputs**:
    - `X obj`: An object of type `X` to be wrapped by the `objWrapper`.
    - `const objWrapper &ow`: A reference to another `objWrapper` object for copy construction.
- **Control Flow**:
    - The constructor `objWrapper(X obj)` initializes the `val_` member with the given object `obj`, using `std::move` to transfer ownership.
    - The copy constructor `objWrapper(const objWrapper &ow)` is defaulted, allowing for default copy construction.
    - A template constructor `objWrapper(const TT &obj)` is deleted to prevent construction from types other than `X`.
    - The copy assignment operator `operator=(const objWrapper &)` is defaulted, allowing for default copy assignment.
    - The move assignment operator `operator=(objWrapper &&)` is defaulted, allowing for default move assignment, but without `noexcept` due to GCC 4.8 limitations.
    - A template assignment operator `operator=(TT &&obj)` is deleted to prevent assignment from types other than `X`.
- **Output**: The class provides a method `value()` that returns a constant reference to the wrapped object of type `X`.
- **See also**: [`objWrapper`](#objWrapper)  (Data Structure)


---
#### objWrapper::objWrapper<!-- {{#callable:objWrapper::objWrapper}} -->
The `objWrapper` class template provides a wrapper for an object of type `X`, with specific constructors and assignment operators to control how objects are created and assigned.
- **Inputs**:
    - `ow`: A reference to an `objWrapper` object of the same type `X` for copy construction.
    - `obj`: An object of any type `TT` for which the constructor is deleted, preventing construction from types other than `X`.
- **Control Flow**:
    - The default copy constructor `objWrapper(const objWrapper &ow) = default;` allows for copying of `objWrapper` objects of the same type `X`.
    - The template constructor `template <class TT> objWrapper(const TT &obj) = delete;` is deleted, preventing construction of `objWrapper` from any type other than `X`.
- **Output**: The `objWrapper` class does not produce an output directly, but it encapsulates an object of type `X` and provides access to it through the `value()` method.
- **See also**: [`objWrapper`](#objWrapper)  (Data Structure)


---
#### objWrapper::objWrapper<!-- {{#callable:objWrapper::objWrapper}} -->
The `objWrapper` constructor template is deleted to prevent implicit conversions from types other than the specified type `X`.
- **Inputs**:
    - `TT`: A template parameter representing the type of the object being passed to the constructor.
    - `obj`: A constant reference to an object of type `TT` that is attempted to be wrapped by `objWrapper`.
- **Control Flow**:
    - The constructor template `objWrapper(const TT &obj)` is explicitly deleted, which means any attempt to construct an `objWrapper` object with a type other than `X` will result in a compilation error.
- **Output**: There is no output from this constructor as it is deleted and cannot be used.
- **See also**: [`objWrapper`](#objWrapper)  (Data Structure)


---
#### objWrapper::operator=<!-- {{#callable:objWrapper::operator=}} -->
The `operator=` function in the `objWrapper` class is a default copy assignment operator that assigns the contents of one `objWrapper` object to another.
- **Inputs**:
    - `const objWrapper &`: A reference to another `objWrapper` object of the same type, which is the source object for the assignment.
- **Control Flow**:
    - The function is defined as the default copy assignment operator, meaning it uses the compiler-generated implementation to copy the contents of the source object to the target object.
    - No custom logic is implemented in this operator, as it relies on the default behavior provided by the compiler.
- **Output**: The function returns a reference to the current `objWrapper` object after the assignment is complete.
- **See also**: [`objWrapper`](#objWrapper)  (Data Structure)


---
#### objWrapper::operator=<!-- {{#callable:objWrapper::operator=}} -->
The `operator=` function is a move assignment operator for the `objWrapper` class, which is defaulted to allow move semantics.
- **Inputs**:
    - `objWrapper &&`: A rvalue reference to an `objWrapper` object, which is the source object for the move assignment.
- **Control Flow**:
    - The function is defaulted, meaning it uses the compiler-generated implementation for move assignment.
    - It allows the `objWrapper` object to be assigned from another `objWrapper` object using move semantics, transferring ownership of resources from the source to the destination object.
- **Output**: The function returns a reference to the current `objWrapper` object after the move assignment is completed.
- **See also**: [`objWrapper`](#objWrapper)  (Data Structure)


---
#### objWrapper::value<!-- {{#callable:objWrapper::value}} -->
The `value` method returns a constant reference to the private member `val_` of the `objWrapper` class.
- **Inputs**: None
- **Control Flow**:
    - The method is marked as `const`, indicating it does not modify the state of the object.
    - The method returns a constant reference to the member variable `val_`.
- **Output**: A constant reference to the private member `val_` of type `X`.
- **See also**: [`objWrapper`](#objWrapper)  (Data Structure)



---
### objWrapperRestricted<!-- {{#data_structure:objWrapperRestricted}} -->
- **Type**: `class`
- **Members**:
    - `val_`: A private member variable of type X that stores the value wrapped by the class.
- **Description**: The `objWrapperRestricted` class is a template class designed to wrap a value of type X with restricted copy and move semantics. It provides a default constructor and a constructor that initializes the wrapped value with an integer. The class deletes the copy constructor, move constructor, copy assignment operator, and move assignment operator to prevent copying and moving of instances. It allows assignment from an integer to update the wrapped value and provides a method to access the wrapped value. This class is useful in scenarios where you want to ensure that instances are not inadvertently copied or moved, maintaining strict control over the object's lifecycle.
- **Member Functions**:
    - [`objWrapperRestricted::objWrapperRestricted`](#objWrapperRestrictedobjWrapperRestricted)
    - [`objWrapperRestricted::objWrapperRestricted`](#objWrapperRestrictedobjWrapperRestricted)
    - [`objWrapperRestricted::objWrapperRestricted`](#objWrapperRestrictedobjWrapperRestricted)
    - [`objWrapperRestricted::objWrapperRestricted`](#objWrapperRestrictedobjWrapperRestricted)
    - [`objWrapperRestricted::operator=`](#objWrapperRestrictedoperator)
    - [`objWrapperRestricted::operator=`](#objWrapperRestrictedoperator)
    - [`objWrapperRestricted::operator=`](#objWrapperRestrictedoperator)
    - [`objWrapperRestricted::value`](#objWrapperRestrictedvalue)

**Methods**

---
#### objWrapperRestricted::objWrapperRestricted<!-- {{#callable:objWrapperRestricted::objWrapperRestricted}} -->
The `objWrapperRestricted` class template provides a restricted wrapper for an object of type `X`, allowing only construction from an integer and assignment from an integer, while deleting copy and move operations.
- **Inputs**:
    - `val`: An integer value used to initialize the internal value `val_` of type `X`.
- **Control Flow**:
    - The default constructor initializes the internal value `val_` to its default state.
    - The explicit constructor initializes the internal value `val_` with the provided integer `val`.
    - Copy constructor and move constructor are deleted to prevent copying or moving instances of the class.
    - Copy assignment operator and move assignment operator are deleted to prevent assignment from another instance of the class.
    - The assignment operator allows assigning an integer to the internal value `val_`.
- **Output**: The class does not produce an output directly, but it provides a method `value()` to access the internal value `val_` of type `X`.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)


---
#### objWrapperRestricted::objWrapperRestricted<!-- {{#callable:objWrapperRestricted::objWrapperRestricted}} -->
The `objWrapperRestricted` class template is a restricted wrapper for a type `X` that only allows construction from an integer and assignment from an integer, while disallowing copy and move operations.
- **Inputs**:
    - `val`: An integer value used to initialize the private member `val_`.
- **Control Flow**:
    - The constructor `objWrapperRestricted(int val)` initializes the private member `val_` with the given integer value.
    - The copy constructor `objWrapperRestricted(const objWrapperRestricted &)` is deleted, preventing copy construction.
    - The move constructor `objWrapperRestricted(objWrapperRestricted &&)` is deleted, preventing move construction.
    - The copy assignment operator `operator=(const objWrapperRestricted &)` is deleted, preventing copy assignment.
    - The move assignment operator `operator=(objWrapperRestricted &&)` is deleted, preventing move assignment.
    - The assignment operator `operator=(int val)` assigns the given integer value to the private member `val_` and returns a reference to the current object.
- **Output**: The class provides a method `value()` that returns a constant reference to the private member `val_` of type `X`.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)


---
#### objWrapperRestricted::objWrapperRestricted<!-- {{#callable:objWrapperRestricted::objWrapperRestricted}} -->
The `objWrapperRestricted` class template is a wrapper that restricts copy and move operations, allowing only assignment from an integer value.
- **Inputs**:
    - `X`: The type of the value to be wrapped by the `objWrapperRestricted` class.
- **Control Flow**:
    - The default constructor initializes the wrapped value to its default state.
    - The explicit constructor initializes the wrapped value with an integer.
    - Copy constructor and move constructor are deleted to prevent copying and moving of `objWrapperRestricted` objects.
    - Copy assignment operator and move assignment operator are deleted to prevent assignment from other `objWrapperRestricted` objects.
    - The assignment operator from an integer updates the wrapped value with the given integer.
    - The `value` method returns a constant reference to the wrapped value.
- **Output**: The class does not produce a direct output, but it provides a method `value()` that returns a constant reference to the wrapped value of type `X`.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)


---
#### objWrapperRestricted::objWrapperRestricted<!-- {{#callable:objWrapperRestricted::objWrapperRestricted}} -->
The `objWrapperRestricted` class template is a wrapper that restricts copy and move operations, allowing only assignment from an integer value.
- **Inputs**:
    - `X`: The type of the value to be wrapped by the `objWrapperRestricted` class.
- **Control Flow**:
    - The default constructor initializes the wrapped value to its default state.
    - The explicit constructor initializes the wrapped value with an integer.
    - Copy constructor is deleted to prevent copying of the object.
    - Move constructor is deleted to prevent moving of the object.
    - Copy assignment operator is deleted to prevent assignment from another object of the same type.
    - Move assignment operator is deleted to prevent move assignment from another object of the same type.
    - The assignment operator from an integer updates the wrapped value with the given integer.
- **Output**: The class provides a method `value()` that returns a constant reference to the wrapped value of type `X`.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)


---
#### objWrapperRestricted::operator=<!-- {{#callable:objWrapperRestricted::operator=}} -->
The `operator=` for `objWrapperRestricted` is deleted to prevent assignment from both copy and move operations.
- **Inputs**:
    - `const objWrapperRestricted &`: A constant reference to another `objWrapperRestricted` object, representing the source object for copy assignment.
    - `objWrapperRestricted &&`: An rvalue reference to another `objWrapperRestricted` object, representing the source object for move assignment.
- **Control Flow**:
    - The copy assignment operator `operator=(const objWrapperRestricted &)` is explicitly deleted, preventing any copy assignment of `objWrapperRestricted` objects.
    - The move assignment operator `operator=(objWrapperRestricted &&)` is explicitly deleted, preventing any move assignment of `objWrapperRestricted` objects.
- **Output**: There is no output as the assignment operators are deleted, meaning they cannot be used.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)


---
#### objWrapperRestricted::operator=<!-- {{#callable:objWrapperRestricted::operator=}} -->
The move assignment operator for the `objWrapperRestricted` class is deleted, preventing move assignment of objects of this class.
- **Inputs**: None
- **Control Flow**:
    - The move assignment operator `operator=` for `objWrapperRestricted` is explicitly deleted, which means any attempt to move-assign an object of this class will result in a compilation error.
- **Output**: There is no output from this function as it is deleted and cannot be used.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)


---
#### objWrapperRestricted::operator=<!-- {{#callable:objWrapperRestricted::operator=}} -->
The `operator=` function assigns an integer value to an `objWrapperRestricted` object and returns a reference to the object itself.
- **Inputs**:
    - `val`: An integer value to be assigned to the `objWrapperRestricted` object.
- **Control Flow**:
    - Assign the input integer `val` to the private member variable `val_`.
    - Return a reference to the current object (`*this`).
- **Output**: A reference to the current `objWrapperRestricted` object after assignment.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)


---
#### objWrapperRestricted::value<!-- {{#callable:objWrapperRestricted::value}} -->
The `value` method returns a constant reference to the private member `val_` of the `objWrapperRestricted` class.
- **Inputs**: None
- **Control Flow**:
    - The method is marked as `CLI11_NODISCARD`, indicating that the return value should not be ignored.
    - The method is a constant member function, meaning it does not modify the state of the object.
    - The method simply returns the private member `val_`.
- **Output**: A constant reference to the private member `val_` of type `X`.
- **See also**: [`objWrapperRestricted`](#objWrapperRestricted)  (Data Structure)



---
### dobjWrapper<!-- {{#data_structure:dobjWrapper}} -->
- **Type**: `class`
- **Members**:
    - `dval_`: A private member variable of type double, initialized to 0.0, used to store a double value.
    - `ival_`: A private member variable of type int, initialized to 0, used to store an integer value.
- **Description**: The `dobjWrapper` class is a simple wrapper class designed to encapsulate a double and an integer value. It provides constructors for initializing the object with either a double or an integer, and offers methods to retrieve these values. The class is primarily used to test and demonstrate option assignments in a command-line interface application, ensuring that both double and integer values can be handled appropriately.
- **Member Functions**:
    - [`dobjWrapper::dobjWrapper`](#dobjWrapperdobjWrapper)
    - [`dobjWrapper::dobjWrapper`](#dobjWrapperdobjWrapper)
    - [`dobjWrapper::dobjWrapper`](#dobjWrapperdobjWrapper)
    - [`dobjWrapper::dvalue`](#dobjWrapperdvalue)
    - [`dobjWrapper::ivalue`](#dobjWrapperivalue)

**Methods**

---
#### dobjWrapper::dobjWrapper<!-- {{#callable:dobjWrapper::dobjWrapper}} -->
The `dobjWrapper` class provides a wrapper for storing and accessing either a double or an integer value, with constructors for both types.
- **Inputs**:
    - `obj`: A double value to initialize the `dval_` member variable.
- **Control Flow**:
    - The default constructor initializes the `dval_` to 0.0 and `ival_` to 0.
    - The explicit constructor with a double parameter initializes the `dval_` member with the provided double value.
    - The explicit constructor with an int parameter initializes the `ival_` member with the provided integer value.
- **Output**: The class does not have a direct output, but provides access to its stored values through the `dvalue()` and `ivalue()` methods, which return the double and integer values respectively.
- **See also**: [`dobjWrapper`](#dobjWrapper)  (Data Structure)


---
#### dobjWrapper::dobjWrapper<!-- {{#callable:dobjWrapper::dobjWrapper}} -->
The `dobjWrapper` class provides constructors to initialize its internal state with either a double or an integer value.
- **Inputs**:
    - `obj`: A double or an integer value used to initialize the internal state of the `dobjWrapper` object.
- **Control Flow**:
    - The constructor for `dobjWrapper` is called with a double argument, initializing the private member `dval_` with the provided double value.
    - Alternatively, the constructor for `dobjWrapper` can be called with an integer argument, initializing the private member `ival_` with the provided integer value.
- **Output**: The constructors do not return any value as they are used to initialize the object state.
- **See also**: [`dobjWrapper`](#dobjWrapper)  (Data Structure)


---
#### dobjWrapper::dobjWrapper<!-- {{#callable:dobjWrapper::dobjWrapper}} -->
The `dobjWrapper` constructor initializes an instance of the `dobjWrapper` class with an integer value, setting the private member `ival_` to the provided integer.
- **Inputs**:
    - `obj`: An integer value used to initialize the `ival_` member of the `dobjWrapper` class.
- **Control Flow**:
    - The constructor is explicitly called with an integer argument.
    - The integer argument `obj` is assigned to the private member `ival_`.
- **Output**: An instance of the `dobjWrapper` class with the `ival_` member initialized to the provided integer value.
- **See also**: [`dobjWrapper`](#dobjWrapper)  (Data Structure)


---
#### dobjWrapper::dvalue<!-- {{#callable:dobjWrapper::dvalue}} -->
The `dvalue` function returns the stored double value from a `dobjWrapper` object.
- **Inputs**: None
- **Control Flow**:
    - The function is a simple getter that returns the private member `dval_`.
- **Output**: A `double` representing the stored value in the `dobjWrapper` object.
- **See also**: [`dobjWrapper`](#dobjWrapper)  (Data Structure)


---
#### dobjWrapper::ivalue<!-- {{#callable:dobjWrapper::ivalue}} -->
The `ivalue` function returns the integer value stored in the `ival_` member of the `dobjWrapper` class.
- **Inputs**: None
- **Control Flow**:
    - The function is a simple getter that directly returns the value of the private member variable `ival_`.
- **Output**: The function returns an integer, which is the value of the `ival_` member variable.
- **See also**: [`dobjWrapper`](#dobjWrapper)  (Data Structure)



---
### AobjWrapper<!-- {{#data_structure:AobjWrapper}} -->
- **Type**: `class`
- **Members**:
    - `val_`: A private member variable of type X that stores the value wrapped by the AobjWrapper.
- **Description**: The `AobjWrapper` class is a template class designed to wrap an object of type `X` with a restricted interface. It provides a default constructor and a single assignment operator for assigning values of type `X` to the wrapper. All other constructors and assignment operators are deleted to prevent unintended conversions or assignments. The class includes a method to retrieve the stored value, ensuring that only the intended type can be assigned to the wrapper, thus enforcing type safety and preventing misuse.
- **Member Functions**:
    - [`AobjWrapper::AobjWrapper`](#AobjWrapperAobjWrapper)
    - [`AobjWrapper::AobjWrapper`](#AobjWrapperAobjWrapper)
    - [`AobjWrapper::operator=`](#AobjWrapperoperator)
    - [`AobjWrapper::value`](#AobjWrappervalue)

**Methods**

---
#### AobjWrapper::AobjWrapper<!-- {{#callable:AobjWrapper::AobjWrapper}} -->
The `AobjWrapper` class template is a wrapper for a single value of type `X` that restricts construction and assignment to only allow direct assignment of the same type.
- **Inputs**:
    - `X`: The type of the value to be wrapped by the `AobjWrapper`.
- **Control Flow**:
    - The default constructor initializes the wrapped value to its default state.
    - All other constructors are deleted, preventing any form of construction other than default.
    - The assignment operator is defined to allow assignment of a value of type `X` to the wrapper, updating the internal value.
    - All other assignment operators are deleted, preventing assignment from any type other than `X`.
    - The `value` method returns a constant reference to the wrapped value.
- **Output**: A constant reference to the wrapped value of type `X`.
- **See also**: [`AobjWrapper`](#AobjWrapper)  (Data Structure)


---
#### AobjWrapper::AobjWrapper<!-- {{#callable:AobjWrapper::AobjWrapper}} -->
The `AobjWrapper` class template is a wrapper that restricts construction and assignment to only allow direct assignment of a specific type, while deleting all other constructors and assignment operators.
- **Inputs**:
    - `X`: The type of the value that the `AobjWrapper` will wrap and manage.
- **Control Flow**:
    - The default constructor initializes the wrapped value to its default state.
    - The template constructor is deleted to prevent construction from any type other than the specified type `X`.
    - The assignment operator is defined to allow assignment of a value of type `X` to the wrapped value.
    - All other assignment operators are deleted to prevent assignment from any type other than `X`.
    - The `value` method returns a constant reference to the wrapped value.
- **Output**: A constant reference to the wrapped value of type `X`.
- **See also**: [`AobjWrapper`](#AobjWrapper)  (Data Structure)


---
#### AobjWrapper::operator=<!-- {{#callable:AobjWrapper::operator=}} -->
The `operator=` function assigns a value of type `X` to an `AobjWrapper` object and returns a reference to the object itself.
- **Inputs**:
    - `val`: A value of type `X` to be assigned to the `AobjWrapper` object.
- **Control Flow**:
    - Assign the input value `val` to the private member `val_` of the `AobjWrapper` object.
    - Return a reference to the current `AobjWrapper` object (`*this`).
- **Output**: A reference to the current `AobjWrapper` object after assignment.
- **See also**: [`AobjWrapper`](#AobjWrapper)  (Data Structure)


---
#### AobjWrapper::value<!-- {{#callable:AobjWrapper::value}} -->
The `value` function returns a constant reference to the private member `val_` of the `AobjWrapper` class.
- **Inputs**: None
- **Control Flow**:
    - The function is a simple getter that returns the private member `val_`.
- **Output**: A constant reference to the private member `val_` of type `X`.
- **See also**: [`AobjWrapper`](#AobjWrapper)  (Data Structure)



---
### SimpleWrapper<!-- {{#data_structure:SimpleWrapper}} -->
- **Type**: `class`
- **Members**:
    - `val_`: A private member variable of type T that stores the value wrapped by the SimpleWrapper.
- **Description**: The `SimpleWrapper` class is a template class designed to wrap a single value of any type `T`. It provides a default constructor and a constructor that initializes the wrapped value. The class includes a method `getRef()` that returns a reference to the wrapped value, allowing for direct manipulation of the value. This class is useful for scenarios where a simple wrapper around a value is needed, providing a consistent interface for accessing and modifying the value.
- **Member Functions**:
    - [`SimpleWrapper::SimpleWrapper`](#SimpleWrapperSimpleWrapper)
    - [`SimpleWrapper::SimpleWrapper`](#SimpleWrapperSimpleWrapper)
    - [`SimpleWrapper::getRef`](#SimpleWrappergetRef)

**Methods**

---
#### SimpleWrapper::SimpleWrapper<!-- {{#callable:SimpleWrapper::SimpleWrapper}} -->
The `SimpleWrapper` constructor initializes an instance of the `SimpleWrapper` class with default values.
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as `default`, meaning it does not perform any custom initialization and relies on the compiler-generated default constructor.
    - No parameters are taken, and no operations are performed within the constructor body.
- **Output**: An instance of `SimpleWrapper` is created with its member variable `val_` initialized to its default value.
- **See also**: [`SimpleWrapper`](#SimpleWrapper)  (Data Structure)


---
#### SimpleWrapper::SimpleWrapper<!-- {{#callable:SimpleWrapper::SimpleWrapper}} -->
The `SimpleWrapper` constructor initializes the `SimpleWrapper` object with a given initial value of type `T`.
- **Inputs**:
    - `initial`: An object of type `T` that is used to initialize the `SimpleWrapper`.
- **Control Flow**:
    - The constructor takes an argument `initial` of type `T`.
    - It uses `std::move` to move the `initial` value into the private member `val_`.
- **Output**: A `SimpleWrapper` object initialized with the provided `initial` value.
- **See also**: [`SimpleWrapper`](#SimpleWrapper)  (Data Structure)


---
#### SimpleWrapper::getRef<!-- {{#callable:SimpleWrapper::getRef}} -->
The `getRef` function returns a reference to the private member `val_` of the `SimpleWrapper` class.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the private member `val_` of the `SimpleWrapper` class.
- **Output**: A reference to the private member `val_` of type `T`.
- **See also**: [`SimpleWrapper`](#SimpleWrapper)  (Data Structure)



# Functions

---
### lexical\_cast<!-- {{#callable:lexical_cast}} -->
The `lexical_cast` function template converts a string input to a specified output type if the type is enabled for conversion.
- **Inputs**:
    - `input`: A constant reference to a `std::string` that represents the input data to be converted.
    - `output`: A reference to an object of type `T` where the converted result will be stored.
- **Control Flow**:
    - The function checks if the type `T` is enabled for lexical casting using `is_my_lexical_cast_enabled<T>::value`.
    - If the type is enabled, the function assigns the input string to the `s` member of the output object.
    - The function returns `true` to indicate successful conversion.
- **Output**: A boolean value `true` indicating that the conversion was successful.


---
### lexical\_cast<anotherstring><!-- {{#callable:CLI::detail::lexical_cast<anotherstring>}} -->
The function `lexical_cast<anotherstring>` attempts to convert a `std::string` input into an `anotherstring` object, appending an exclamation mark to the result if successful.
- **Inputs**:
    - `input`: A constant reference to a `std::string` that represents the input string to be converted.
    - `output`: A reference to an `anotherstring` object where the converted result will be stored.
- **Control Flow**:
    - The function calls [`lexical_cast`](../include/CLI/TypeTools.hpp.driver.md#lexical_cast) with the input string and the `s` member of the `anotherstring` output object.
    - If the conversion is successful (i.e., [`lexical_cast`](../include/CLI/TypeTools.hpp.driver.md#lexical_cast) returns true), an exclamation mark is appended to the `s` member of the `anotherstring` object.
    - The function returns the result of the [`lexical_cast`](../include/CLI/TypeTools.hpp.driver.md#lexical_cast) call, indicating whether the conversion was successful.
- **Output**: A boolean value indicating whether the conversion from `std::string` to `anotherstring` was successful.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](../include/CLI/TypeTools.hpp.driver.md#lexical_cast)


