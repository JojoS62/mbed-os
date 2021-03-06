# Copyright (c) 2020 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

add_library(mbed-fvp-mps2-m3 INTERFACE)

if(${MBED_TOOLCHAIN} STREQUAL "ARM")
    set(LINKER_FILE device/TOOLCHAIN_ARM_STD/MPS2.sct)
    set(STARTUP_FILE device/TOOLCHAIN_ARM_STD/startup_MPS2.S)
elseif(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
    set(LINKER_FILE device/TOOLCHAIN_GCC_ARM/MPS2.ld)
    set(STARTUP_FILE device/TOOLCHAIN_GCC_ARM/startup_MPS2.S)
endif()

mbed_set_linker_script(mbed-fvp-mps2-m3 ${CMAKE_CURRENT_SOURCE_DIR}/${LINKER_FILE})

target_include_directories(mbed-fvp-mps2-m3
    INTERFACE
        device
)

target_sources(mbed-fvp-mps2-m3
    INTERFACE
        device/system_CMSDK_CM3.c
        ${STARTUP_FILE}
)

target_link_libraries(mbed-fvp-mps2-m3 INTERFACE mbed-fvp-mps2)
