cmake_minimum_required(VERSION 3.28)

project(bme68x)

add_library(bme68x STATIC
    "bme68x.c"
)

target_include_directories(bme68x
    PUBLIC
        ""
)
