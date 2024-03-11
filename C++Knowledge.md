Try Catch C++ 20:

```c++
try {
        cout << AddPositiveIntegers(-1, 2); //exception
}
catch (std::invalid_argument& e) {
        cerr << e.what() << endl;
        return -1;
}

```

```c++
class MyException : public std::exception {
public:
    // Constructor that takes an error message
    MyException(const char* message) : message_(message) {}

    // Override the what() function to provide error description
    const char* what() const noexcept override {
        return message_.c_str(); // return a c-stype string of type const char*
    }

private:
    std::string message_;
};
```

```c++
[](const std::string& a, const std::string& b) {
    return a.length() > b.length();
}

```

- `[]( ... )` is the lambda function syntax, indicating that we're defining an anonymous function.
- `(const std::string& a, const std::string& b)` are the lambda's parameter list, specifying that it takes two `const std::string&` parameters.
- `return a.length() > b.length();` is the lambda's body, which defines the custom comparison logic. In this case, it returns `true` if the length of `a` is greater than the length of `b`, which sorts the strings in descending order of length.



this in cpp class is a ptr, so need to use this->a



unordered_map use insert(make_pair(a,b))

and use at(key)



how linker works in cpp



ChatGPT



Linking is a crucial step in the compilation process of a C++ program. It's the phase that combines object files generated during compilation into an executable program. Here's an overview of how the linker works in C++:

1. **Compilation**: The C++ source code is first compiled into object files. Each source file (.cpp) is compiled separately into an object file (.o or .obj). These object files contain machine code for the individual translation units (source files).
2. **Symbol Resolution**: During the compilation, the compiler generates references to functions, variables, and other symbols defined in the source code. These references are typically stored in a symbol table within each object file. Symbols can be functions, variables, or other identifiers with a memory location.
3. **Object File Generation**: The compiler generates object files for each translation unit, and these files include both the compiled code and information about symbols referenced and defined within that translation unit.
4. **Linking**: The linker takes all the object files generated during compilation, including any external libraries and object files provided, and resolves the references to symbols. It matches references (e.g., function calls) to their actual definitions (e.g., function implementations). This process ensures that the program knows where to find the memory addresses associated with each symbol.
5. **Symbol Table**: The linker builds a global symbol table that keeps track of all symbols across all object files. It checks for any unresolved symbols (symbols referenced but not defined) and attempts to find their definitions in other object files or libraries.
6. **Relocation**: The linker calculates and performs relocations, which are adjustments to memory addresses in the object files to reflect the final location of symbols in the executable. These adjustments are necessary because the memory layout of the program can differ from the individual object files.
7. **Executable Output**: Finally, the linker produces the executable program. This is typically an executable file (e.g., an `.exe` file on Windows or an ELF binary on Unix-based systems) that can be run by the operating system. The linker ensures that all necessary code and data are properly combined into the executable.

In summary, the linker plays a critical role in combining object files, resolving symbols, and producing a coherent executable program. It ensures that functions and variables referenced across different parts of your code are correctly connected and that the program can execute as expected.

 `#pragma once` and the traditional `#ifndef`, `#define`, and `#endif` include guards serve the same purpose: they prevent a header file from being included multiple times in the same translation unit (source file) to avoid issues like duplicate symbol definitions and increased compilation times.

```c++
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> sortedNumbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int targetValue = 5;

    bool found = std::binary_search(sortedNumbers.begin(), sortedNumbers.end(), targetValue);
  // std::sort(a.begin(), a.end(), Comparator())
  // class Com{
  // bool operator()(string a, string b) const {return true;}
 // }

    if (found) {
        std::cout << "Value " << targetValue << " found in the vector." << std::endl;
    } else {
        std::cout << "Value " << targetValue << " not found in the vector." << std::endl;
    }

    return 0;
}
```

why operator()(argument) is that to make operator() a function name distinguish from void operator(argument) for example



std::optional`std::optional` is a C++17 feature that provides a way to represent optional values, meaning values that can be either valid or absent (empty). It's a safer and more expressive alternative to using sentinel values or pointers to indicate missing values. Here's how to use `std::optional`:

**1. Include the `<optional>` header:**

```
cppCopy code
#include <optional>
```

**2. Declare an `std::optional` variable:**

You can declare an `std::optional` variable for a specific type. For example, to declare an optional integer:

```
cppCopy code
std::optional<int> optionalInt;
```

**3. Assign a value or make it empty:**

You can assign a value to an `std::optional` or make it empty (no value) using the `std::nullopt` keyword. For example:

```
cppCopy code
std::optional<int> optionalIntWithValue = 42; // Assign a value
std::optional<int> emptyOptional = std::nullopt; // Make it empty
```

**4. Check if it has a value:**

You can check if an `std::optional` has a value using the `has_value()` member function:

```
cppCopy code
if (optionalInt.has_value()) {
    // It has a value
    int value = optionalInt.value(); // Access the value
} else {
    // It's empty
}
```

**5. Access the value (if it has one):**

You can access the stored value (if it exists) using the `value()` member function, but make sure to check if it has a value first to avoid undefined behavior:

```
cppCopy code
if (optionalInt.has_value()) {
    int value = optionalInt.value(); // Access the value
}
```

**6. Use value or a default value:**

You can use the `value_or()` member function to retrieve the stored value or a default value if the optional is empty:

```
cppCopy code
int result = optionalInt.value_or(0); // Use 0 as the default value if empty
```

**7. Emplace a value (for non-default constructors):**

If you want to construct the stored value in-place (e.g., using a non-default constructor), you can use the `emplace()` member function:

```
cppCopy code
std::optional<std::string> optionalStr;
optionalStr.emplace("Hello, World!");
```

**8. Reset (make empty) an optional:**

You can reset an `std::optional` to be empty using the `reset()` member function:

```
cppCopy code
optionalInt.reset(); // Make it empty
```

Using `std::optional` can help make your code more readable and safer by explicitly indicating when a value may or may not be present, reducing the need for special sentinel values or complex error handling.





std::lower_bound(vec.begin(), vec.end(), target) returns the first iterator point to the element that is not less than target (>= target), if all smaller, then return vec.end()

std::upper_bound(...) first element's iterator that the value of this element is larger than the target, also can be vec.end()

auto it = std::lower_bound(vec.begin(), vec.end(), MyObject(target), MyObjectComparator());// used on customized object and comparator

multiset and map used bst for innter implementation, they are inner sorted 

```c++
vector<int>::iterator ptr;
```

C++ comparator should return false when equal, since if return true when equal, that means you want a == b, a before b, but that also means, b before a, contradict! so a==b, a don't comes before b, also means b don't comes before a (comes before is an action), nothing happened.



greedy used when local optimal contribute to global optimal



Three main  characteristics:

1. Encapsulation C++:https://www.geeksforgeeks.org/encapsulation-in-cpp/

2. Inheritance C++: https://www.geeksforgeeks.org/inheritance-in-c/

   ```c++
   class  <derived_class_name> : <access-specifier> <base_class_name>
   {
           //body
   }
   ```

   1. **Public Mode**: If we derive a subclass from a public base class. Then the public member of the base class will become public in the derived class and protected members of the base class will become protected in the derived class.
      1. public->public, protected->protected, private->private

   1. **Protected Mode**: If we derive a subclass from a Protected base class. Then both public members and protected members of the base class will become protected in the derived class.
      1. Public->protected, protected->protected, private->private

   1. **Private Mode**: If we derive a subclass from a Private base class. Then both public members and protected members of the base class will become Private in the derived class.
      1. Public->private, protected->private, private->private

Single inheritance

Multiple inheritance constructor calls follows the order of inheritance

Multilevel inheritance

Hierarchical inheritance

hybrid inheritance (combination of more than one type of inheritances)

multipath inheritance (a special case of hybrid inheritance): A is the base class of B and C, D inheritant from both B and C, then will have two copies of A, and we need to specify the path to help compiler to find which A we want to access: for example obj.B::a; obj.C::a (if a is a publicly inheritanted attribute of A) (Diamond problem in inheritance)

Virtual function in c++:https://www.geeksforgeeks.org/virtual-function-cpp/

1. Virtual functions cannot be static.
2. A virtual function can be a friend function of another class.
3. Virtual functions should be accessed using a pointer or reference of base class type to achieve runtime polymorphism.
4. The prototype of virtual functions should be the same in the base as well as the derived class.
5. They are always defined in the base class and overridden in a derived class. It is not mandatory for the derived class to override (or re-define the virtual function), in that case, the base class version of the function is used.
6. A class may have a [virtual destructor](https://www.geeksforgeeks.org/virtual-destructor/) but it cannot have a virtual constructor.
7. virtual function enable late binding (call virtual function, determine which function to call at runtime since cannot determine at compile time).

Friend class and function: https://www.geeksforgeeks.org/friend-class-function-cpp/ https://www.tutorialspoint.com/cplusplus/cpp_friend_functions.html
function or class outside of this class but can access private/protected members of this class ( need friend declaration in this class: friend class B; or friend void print(A& a);)



Polymorphism C++:https://www.geeksforgeeks.org/cpp-polymorphism/

function overloading is determined at compile time: same function name with different parameters

Operator() overloading

VPTR is only in class **object** that has virtual function (as a hidden class member)

 point to the VTABLE of the class, VTABLE contains function pointer to each of virtual function, and when base* a = new B() happens the overriden virtual funciton's pointer will be replaced by the right function pointer in the derived class override the corresponding virtual funciton in base class.

Shape* ptr = new Circle(5.0);

or 

Circle c(5.0);

Shape* ptr = &c;

## log and log2

Use log2 instead of log to make precision high. floating point conversion and calculation is easier to lose more precision. See here for some more hints:https://graphics.stanford.edu/~seander/bithacks.html#IntegerLogLookup

## memset

memset value used two-complement so that's why use INT_MAX result in -1

so better only use this to set 0 or 1 etc.

int a[26] = {} will by default all 0
