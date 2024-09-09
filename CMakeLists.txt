# specifica versiunea minima necesară de CMake
cmake_minimum_required(VERSION 3.13)

# Include fisierul de configurare Pico SDK folosind calea din variabila de mediu PICO_SDK_PATH
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

# Defineste proiectul cu numele "clion_template" și specifica limbajele folosite: C, C++ și Assembly
project(clion_template C CXX ASM)

set(CMAKE_C_STANDARD 11)  # Seteaza standardul pentru C la C11
set(CMAKE_CXX_STANDARD 17)  # Seteaza standardul pentru C++ la C++17

pico_sdk_init()  # init SDK-ul Pico

# Aduaga un executabil numit "clion_template" care foloseste fisierul "main.c" din directorul "src"
add_executable(clion_template
        src/main.c
)
# Leaga executabilul "clion_template" de biblioteca standard Pico
target_link_libraries(clion_template pico_stdlib hardware_pwm)

#pico_enable_stdio_usb(clion_template 1)  # Activeaza intrarea/iesirea standard prin USB (comentat pentru a nu fi folosit)
pico_enable_stdio_uart(clion_template 1)  # Activeaza intrarea/iesirea standard prin UART

pico_add_extra_outputs(clion_template)  # Adauga iesiri suplimentare (binare, debug etc.) pentru executabil
