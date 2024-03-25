cmake_minimum_required(VERSION 3.5)

project(chntpw VERSION 1.0.2 DESCRIPTION "The Offline NT Password Editor")

find_package(OpenSSL REQUIRED COMPONENTS Crypto)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

add_compile_options("-Wall" "-D_XOPEN_SOURCE" "-DDOCRYPTO")

add_library(edlib OBJECT "edlib.c")
add_library(ntreg OBJECT "ntreg.c")
add_library(sam OBJECT "libsam.c")

add_executable(chntpw "chntpw.c")
add_executable(cpnt "cpnt.c")
add_executable(reged "reged.c")
add_executable(sampasswd "sampasswd.c")
add_executable(samusrgrp "samusrgrp.c")

target_link_libraries(edlib PRIVATE ntreg)
target_link_libraries(sam PRIVATE ntreg)

target_link_libraries(chntpw PRIVATE edlib ntreg sam OpenSSL::Crypto)
target_link_libraries(reged PRIVATE edlib ntreg)
target_link_libraries(sampasswd PRIVATE ntreg sam)
target_link_libraries(samusrgrp PRIVATE ntreg sam)
