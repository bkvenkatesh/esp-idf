target_include_directories(${COMPONENT_LIB} PUBLIC .)
target_include_directories(${COMPONENT_LIB} PUBLIC private_include)

set(srcs
    "rtc_clk.c"
    "rtc_clk_init.c"
    "rtc_init.c"
    "rtc_pm.c"
    "rtc_sleep.c"
    "rtc_time.c"
    "rtc_wdt.c"
    "regi2c_ctrl.c"
    "chip_info.c"
    )

if(NOT BOOTLOADER_BUILD)
    list(APPEND srcs "async_memcpy_impl_cp_dma.c")
endif()

add_prefix(srcs "${CMAKE_CURRENT_LIST_DIR}/" "${srcs}")
target_sources(${COMPONENT_LIB} PRIVATE "${srcs}")

if(NOT CMAKE_BUILD_EARLY_EXPANSION)
    set_source_files_properties("${CMAKE_CURRENT_LIST_DIR}/rtc_clk.c" PROPERTIES
                                COMPILE_FLAGS "-fno-jump-tables -fno-tree-switch-conversion")
endif()
