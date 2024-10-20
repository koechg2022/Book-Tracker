



cmake_minimum_required(VERSION 3.10)


project(Book_tracker)


set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)



# Include directories
include_directories(${PROJECT_SOURCE_DIR}/headers)
include_directories(${PROJECT_SOURCE_DIR}/headers/networking)


# Add source files
set( SOURCES
    ${PROJECT_SOURCE_DIR}/libraries/networking_functions.c++
    ${PROJECT_SOURCE_DIR}/libraries/string_functions.c++
)


# Create static libraries from source files
add_library(networking_functions STATIC ${PROJECT_SOURCE_DIR}/libraries/networking_functions.c++)
add_library(string_functions STATIC ${PROJECT_SOURCE_DIR}/libraries/string_functions.c++)


# Create executables
add_executable(book_tracker ${PROJECT_SOURCE_DIR}/source/book_tracker.c++)


# Link libraries to executables
target_link_libraries(book_tracker PRIVATE networking_functions string_functions)


# Set output directory for the executables
set_target_properties(book_tracker PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/objects)


if (CMAKE_CXX_COMPILER_ID MATCHES "Clang|GNU")
    target_compile_options(networking_functions PRIVATE -Wall -Wextra)
    target_compile_options(string_functions PRIVATE -Wall -Wextra)
    target_compile_options(book_tracker PRIVATE -Wall -Wextra)
elseif(MSVC)
    target_compile_options(book_tracker PRIVATE /W4)
endif()