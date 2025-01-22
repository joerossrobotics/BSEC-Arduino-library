cmake_minimum_required(VERSION 3.28)

project(BSEC-Arduino-library C CXX)

add_subdirectory("src/bme68x")

add_library(BSEC-Arduino-library STATIC
    "src/bsec.cpp"
)

target_include_directories(BSEC-Arduino-library
    PUBLIC
        "src"
)

# Set platform-specific libraries
if(CMAKE_SYSTEM_PROCESSOR MATCHES "cortex-m0")
    # Cortex-M0
    set(ALGO_BSEC_LIB "${CMAKE_CURRENT_SOURCE_DIR}/src/cortex-m0/libalgobsec.a")
elseif(CMAKE_SYSTEM_PROCESSOR MATCHES "cortex-m0plus")
    # Cortex-M0+
    set(ALGO_BSEC_LIB "${CMAKE_CURRENT_SOURCE_DIR}/src/cortex-m0plus/libalgobsec.a")
else()
    message(FATAL_ERROR "Unsupported platform: ${CMAKE_SYSTEM_PROCESSOR}")
endif()

target_link_libraries(BSEC-Arduino-library
    PUBLIC
        pico_stdlib
        bme68x
        ${ALGO_BSEC_LIB}
)