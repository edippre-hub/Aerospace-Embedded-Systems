cmake_minimum_required(VERSION 3.20)
project(AerospaceEmbeddedMonitor VERSION 1.0.0 LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
option(AERO_ENABLE_WARNINGS "Enable strict compiler warnings" ON)
add_library(aero_core src/monitor.cpp)
target_include_directories(aero_core PUBLIC include)
if(AERO_ENABLE_WARNINGS)
  if(MSVC)
    target_compile_options(aero_core PRIVATE /W4)
  else()
    target_compile_options(aero_core PRIVATE -Wall -Wextra -Wpedantic -Wconversion -Wshadow)
  endif()
endif()
add_executable(aero_monitor src/main.cpp)
target_link_libraries(aero_monitor PRIVATE aero_core)
enable_testing()
add_executable(aero_tests tests/test_monitor.cpp)
target_link_libraries(aero_tests PRIVATE aero_core)
add_test(NAME aero_unit_tests COMMAND aero_tests)
# Optional FreeRTOS target: provide a FreeRTOS-Kernel checkout via FREERTOS_KERNEL_PATH.
if(DEFINED FREERTOS_KERNEL_PATH)
  add_executable(aero_freertos rtos/freertos_main.cpp
    ${FREERTOS_KERNEL_PATH}/tasks.c
    ${FREERTOS_KERNEL_PATH}/queue.c
    ${FREERTOS_KERNEL_PATH}/list.c
    ${FREERTOS_KERNEL_PATH}/timers.c
    ${FREERTOS_KERNEL_PATH}/portable/MemMang/heap_4.c)
  target_include_directories(aero_freertos PRIVATE include
    ${FREERTOS_KERNEL_PATH}/include
    ${FREERTOS_KERNEL_PATH}/portable/ GCC/ARM_CM4F)
  target_compile_definitions(aero_freertos PRIVATE AERO_FREERTOS_TARGET=1)
endif()

