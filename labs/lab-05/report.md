# Lab 5: Build Systems

# Part 1

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
```
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

options(USE_MYMATH "Use tutorial provided math implementation" ON)

# configure a header file to pass some of the CMake settings
# to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

if(USE_MYMATH)
        add_subdirectory(MathFunctions)
        list(APPEND EXTRA_LIBS MathFunctions)
        list(APPEND EXTRA_INCLUDES "${PROJECT_SOURCE_DIR}/MathFunctions")
endif()

# add the executable
add_executable(Tutorial tutorial.cxx)

target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           ${EXTRA_INCLUDES}
                           )
```

Tutorial:

![image](https://user-images.githubusercontent.com/86938356/153738610-f446b4fb-1c92-4d5e-9e57-1417859907c2.png)

Tutorial 10:
![image](https://user-images.githubusercontent.com/86938356/153738642-abdc4acd-d0a6-46c3-897a-2c3889699652.png)

Tutorial 4294967296:
![image](https://user-images.githubusercontent.com/86938356/153738658-d141a73c-06eb-44da-82bd-483154bea0dd.png)

### Step 3:

CMakeLists.txt:
```
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# should we use our own math functions
option(USE_MYMATH "Use tutorial provided math implementation" ON)

# configure a header file to pass some of the CMake settings
# to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

# add the MathFunctions library
if(USE_MYMATH)
  add_subdirectory(MathFunctions)
  list(APPEND EXTRA_LIBS MathFunctions)
endif()

# add the executable
add_executable(Tutorial tutorial.cxx)

target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )
```

MathFunctions/CMakeLists.txt:
```
add_library(MathFunctions mysqrt.cxx)
target_include_directories(MathFunctions
        INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
        )
 ```

Tutorial:
![image](https://user-images.githubusercontent.com/86938356/153649861-3cb6fca3-8171-4689-b56f-4f3b7bd42a3a.png)

Tutorial 10:
![image](https://user-images.githubusercontent.com/86938356/153649894-01827016-c3bc-4d6a-8707-8602cb104b08.png)

Tutorial 4294967296:
![image](https://user-images.githubusercontent.com/86938356/153649922-4f7879a5-852b-451b-87f9-8d617705e1e0.png)

### Step 4:
CMakeLists.txt:
```
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# should we use our own math functions
option(USE_MYMATH "Use tutorial provided math implementation" ON)

# configure a header file to pass some of the CMake settings
# to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

# add the MathFunctions library
if(USE_MYMATH)
  add_subdirectory(MathFunctions)
  list(APPEND EXTRA_LIBS MathFunctions)
endif()

# add the executable
add_executable(Tutorial tutorial.cxx)

target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )
install(TARGETS Tutorial DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/TutorialConfig.h"
        DESTINATION include
        )

enable_testing()

# does the application run
add_test(NAME Runs COMMAND Tutorial 25)

# does the usage message work?
add_test(NAME Usage COMMAND Tutorial)
set_tests_properties(Usage
          PROPERTIES PASS_REGULAR_EXPRESSION "Usage:.*number"
          )

# define a function to simplify adding tests
function(do_test target arg result)
        add_test(NAME Comp${arg} COMMAND ${target} ${arg})
        set_tests_properties(Comp${arg}
                PROPERTIES PASS_REGULAR_EXPRESSION ${result}
                )
endfunction()

# do a bunch of result based tests
do_test(Tutorial 4 "4 is 2")
do_test(Tutorial 9 "9 is 3")
do_test(Tutorial 5 "5 is 2.236")
do_test(Tutorial 7 "7 is 2.645")
do_test(Tutorial 25 "25 is 5")
do_test(Tutorial -25 "-25 is (-nan|nan|0)")
do_test(Tutorial 0.0001 "0.0001 is 0.01")
```

MathFunctions/CMakeLists.txt:
```
add_library(MathFunctions mysqrt.cxx)

# state that anybody linking to us needs to include the current source dir
# to find MathFunctions.h, while we don't.
target_include_directories(MathFunctions
          INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
          )
install(TARGETS MathFunctions DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include)
```

ctest -W output:
![image](https://user-images.githubusercontent.com/86938356/153652691-114b7849-433f-4fba-9f00-bb6bee763fe0.png)

### Step 5:
CMakeLists.txt:
```
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# should we use our own math functions
option(USE_MYMATH "Use tutorial provided math implementation" ON)

# configure a header file to pass some of the CMake settings
# to the source code
configure_file(TutorialConfig.h.in TutorialConfig.h)

# add the MathFunctions library
if(USE_MYMATH)
  add_subdirectory(MathFunctions)
  list(APPEND EXTRA_LIBS MathFunctions)
endif()

# add the executable
add_executable(Tutorial tutorial.cxx)
target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})
# add the binary tree to the search path for include files
# so that we will find TutorialConfig.h
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )

# add the install targets
install(TARGETS Tutorial DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/TutorialConfig.h"
  DESTINATION include
  )

# enable testing
enable_testing()

# does the application run
add_test(NAME Runs COMMAND Tutorial 25)

# does the usage message work?
add_test(NAME Usage COMMAND Tutorial)
set_tests_properties(Usage
  PROPERTIES PASS_REGULAR_EXPRESSION "Usage:.*number"
  )
# define a function to simplify adding tests
function(do_test target arg result)
  add_test(NAME Comp${arg} COMMAND ${target} ${arg})
  set_tests_properties(Comp${arg}
    PROPERTIES PASS_REGULAR_EXPRESSION ${result}
    )
endfunction()

# do a bunch of result based tests
do_test(Tutorial 4 "4 is 2")
do_test(Tutorial 9 "9 is 3")
do_test(Tutorial 5 "5 is 2.236")
do_test(Tutorial 7 "7 is 2.645")
do_test(Tutorial 25 "25 is 5")
do_test(Tutorial -25 "-25 is (-nan|nan|0)")
do_test(Tutorial 0.0001 "0.0001 is 0.01")
```

MathFunctions/CMakeLists.txt:
```
add_library(MathFunctions mysqrt.cxx)

# state that anybody linking to us needs to include the current source dir
# to find MathFunctions.h, while we don't.
target_include_directories(MathFunctions
          INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
          )
# does this system provide the log and exp functions?
include(CheckSymbolExists)
check_symbol_exists(log "math.h" HAVE_LOG)
check_symbol_exists(exp "math.h" HAVE_EXP)
if(NOT (HAVE_LOG AND HAVE_EXP))
        unset(HAVE_LOG CACHE)
        unset(HAVE_EXP CACHE)
        set(CMAKE_REQUIRED_LIBRARIES "m")
        check_symbol_exists(log "math.h" HAVE_LOG)
        check_symbol_exists(exp "math.h" HAVE_EXP)
        if(HAVE_LOG AND HAVE_EXP)
                target_link_libraries(MathFunctions PRIVATE m)
        endif()
endif()
if(HAVE_LOG AND HAVE_EXP)
        target_compile_definitions(MathFunctions
                PRIVATE "HAVE_LOG" "HAVE_EXP")
endif()
# install rules
install(TARGETS MathFunctions DESTINATION lib)
install(FILES MathFunctions.h DESTINATION include)
```

Tutorial:
![image](https://user-images.githubusercontent.com/86938356/153656150-b51b5f39-28ec-46f5-947a-1b60609452f4.png)

Tutorial 10:
![image](https://user-images.githubusercontent.com/86938356/153656067-5ff49cfc-34e9-4235-ae23-d218bbeaf9b6.png)

Tutorial 4294967296:
![image](https://user-images.githubusercontent.com/86938356/153656042-5aa7fd28-fb08-46f1-a4f6-a5150a6a64e8.png)

# Part 2
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



