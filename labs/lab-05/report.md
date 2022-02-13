# Lab 5: Build Systems

### Part 1

### Step 1:

tutorial.cxx:
```
// A simple program that computes the square root of a number
#include <cmath>
#include <iostream>
#include <string>
#include "TutorialConfig.h"

int main(int argc, char* argv[])
{
  if (argc < 2) {
    // report version
    std::cout << argv[0] << " Version " << Tutorial_VERSION_MAJOR << "."
              << Tutorial_VERSION_MINOR << std::endl;
    std::cout << "Usage: " << argv[0] << " number" << std::endl;
    return 1;
  }

  // convert input to double
  const double inputValue = std::stod(argv[1]);

  // calculate square root
  const double outputValue = sqrt(inputValue);
  std::cout << "The square root of " << inputValue << " is " << outputValue
            << std::endl;
  return 0;
}
```

CMakeLists.txt:
```
cmake_minimum_required(VERSION 3.10)

project(Tutorial VERSION 1.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

configure_file(TutorialConfig.h.in TutorialConfig.h)

add_executable(Tutorial tutorial.cxx)

target_include_directories(Tutorial PUBLIC
        "${PROJECT_BINARY_DIR}"
        )
```

Tutorial:
![image](https://user-images.githubusercontent.com/86938356/153641898-0861b5e1-ef19-469b-adca-68996fee2633.png)

Tutorial 10:
![image](https://user-images.githubusercontent.com/86938356/153641949-a5916b97-d708-4c4f-a62a-2f19f7272e46.png)

Tutorial 4294967296:
![image](https://user-images.githubusercontent.com/86938356/153642059-691bed21-16b8-4307-9a33-7f6b351dab64.png)

### Step 2:

tutorial.cxx:
```
#include <iostream>
#include <string>
#include "TutorialConfig.h"
#ifdef USE_MYMATH
#       include "MathFunctions.h"
#endif

int main(int argc, char* argv[])
{
  if (argc < 2) {
    std::cout << argv[0] << " Version " << Tutorial_VERSION_MAJOR << "."
            <<Tutorial_VERSION_MINOR << std::endl;
    std::cout << "Usage: " << argv[0] << " number" << std::endl;
    return 1;
  }

  // convert input to double
  const double inputValue = std::stod(argv[1]);

  // calculate square root
  #ifdef USE_MYMATH
         const double outputValue = mysqrt(inputValue);
  #else
         const double outputValue = sqrt(inputValue);
  #endif
  std::cout << "The square root of " << inputValue << " is " << outputValue
            << std::endl;
  return 0;
}
```

CMakeLists.txt:


### Step 3:

CMakeLists.txt:
![image](https://user-images.githubusercontent.com/86938356/153650019-97d3f7d8-daa6-469a-9ea4-2dc75063d2d0.png)

MathFunctions/CMakeLists.txt:
![image](https://user-images.githubusercontent.com/86938356/153650083-6ab467d7-8dc0-4be4-8fa3-d3ffbe449467.png)

Tutorial:
![image](https://user-images.githubusercontent.com/86938356/153649861-3cb6fca3-8171-4689-b56f-4f3b7bd42a3a.png)

Tutorial 10:
![image](https://user-images.githubusercontent.com/86938356/153649894-01827016-c3bc-4d6a-8707-8602cb104b08.png)

Tutorial 4294967296:
![image](https://user-images.githubusercontent.com/86938356/153649922-4f7879a5-852b-451b-87f9-8d617705e1e0.png)

### Step 4:
CMakeLists.txt:

MathFunctions/CMakeLists.txt:
![image](https://user-images.githubusercontent.com/86938356/153653400-5342bdea-1b79-4b8f-9d5c-9d55ee50c896.png)

ctest -W output:
![image](https://user-images.githubusercontent.com/86938356/153652691-114b7849-433f-4fba-9f00-bb6bee763fe0.png)

### Step 5:
CMakeLists.txt:

MathFunctions/CMakeLists.txt:
![image](https://user-images.githubusercontent.com/86938356/153656312-dbaecfd3-04cd-4a60-91b9-c030760a607e.png)

Tutorial:
![image](https://user-images.githubusercontent.com/86938356/153656150-b51b5f39-28ec-46f5-947a-1b60609452f4.png)

Tutorial 10:
![image](https://user-images.githubusercontent.com/86938356/153656067-5ff49cfc-34e9-4235-ae23-d218bbeaf9b6.png)

Tutorial 4294967296:
![image](https://user-images.githubusercontent.com/86938356/153656042-5aa7fd28-fb08-46f1-a4f6-a5150a6a64e8.png)

### Part 2
Makefile:
```
all: static_block dynamic_block

clean:
        rm static_block dynamic_block program.o block.o static_lib.a dynamic_lib.so

static_block: static_lib program.o
        gcc program.o static_lib.a -o static_block

dynamic_block: dynamic_lib program.o
        gcc program.o dynamic_lib.so -o dynamic_block

static_lib: block.o
        ar qc static_lib.a block.o

dynamic_lib: block.o
        gcc -shared -o dynamic_lib.so block.o

program.o: program.c
        gcc -c program.c -o program.o

block.o: source/block.c
        gcc -c source/block.c -o block.o
```
CMakeLists.txt:
```
cmake_minimum_required(VERSION 3.10)

project(Lab5Part2)

add_library(static_lib source/block.c)
add_library(dynamic_lib SHARED source/block.c)

add_executable(static_block program.c)
add_executable(dynamic_block program.c)

target_link_libraries(static_block static_lib)
target_link_libraries(dynamic_block dynamic_lib)
```

Size Difference: Static = 8464 and Dynamic = 8296
![image](https://user-images.githubusercontent.com/86938356/153730227-8b69aa26-f19d-4f99-b324-b3a9d3fe9082.png)

Running Program:
![image](https://user-images.githubusercontent.com/86938356/153730181-ecafad04-d02c-4d8a-bdc5-93a21f75f233.png)



