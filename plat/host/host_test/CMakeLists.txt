#
# SPDX-License-Identifier: BSD-3-Clause
# SPDX-FileCopyrightText: Copyright TF-RMM Contributors.
#

add_library(rmm-plat-host_test)

# host_test builds unittests for RMM
arm_config_option(
    NAME RMM_UNITTESTS
    HELP "Enable Unitests for the build"
    DEFAULT "ON"
    TYPE INTERNAL)

target_link_libraries(rmm-plat-host_test
    PRIVATE rmm-lib
            CppUTest
    # Needed to export host_utils.h
    PUBLIC  rmm-host-common)

# Used to locate test_groups.h
target_include_directories(rmm-plat-host_test
    PRIVATE "${CMAKE_BINARY_DIR}/plat/host/${HOST_VARIANT}/src")

target_include_directories(rmm-plat-host_test
    PUBLIC "include")

target_sources(rmm-plat-host_test
    PRIVATE "src/test_main.cpp"
            "src/host_harness.c"
            "src/test_helpers.c")

add_library(rmm-platform ALIAS rmm-plat-host_test)
