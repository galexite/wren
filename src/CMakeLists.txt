add_library(wren)
target_sources(wren
    PRIVATE
        "optional/wren_opt_meta.c"
        "optional/wren_opt_meta.h"
        "optional/wren_opt_random.c"
        "optional/wren_opt_random.h"
        "vm/wren_common.h"
        "vm/wren_compiler.c"
        "vm/wren_compiler.h"
        "vm/wren_core.c"
        "vm/wren_core.h"
        "vm/wren_debug.c"
        "vm/wren_debug.h"
        "vm/wren_math.h"
        "vm/wren_opcodes.h"
        "vm/wren_primitive.c"
        "vm/wren_primitive.h"
        "vm/wren_utils.c"
        "vm/wren_utils.h"
        "vm/wren_value.c"
        "vm/wren_value.h"
        "vm/wren_vm.c"
        "vm/wren_vm.h"

    PUBLIC
        FILE_SET HEADERS
        BASE_DIRS include
        FILES
            "include/wren.h"
)
target_include_directories(wren
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
    PRIVATE
        "vm"
        "optional"
)
target_link_libraries(wren PRIVATE m)
set_property(TARGET wren PROPERTY COMPILE_WARNING_AS_ERROR ON)

add_library(wren::wren ALIAS wren)

install(
    TARGETS wren
    EXPORT wren-targets
    FILE_SET HEADERS
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

install(
    EXPORT wren-targets
    NAMESPACE wren::
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/wren"
)

include(CMakePackageConfigHelpers)

configure_package_config_file("wren-config.cmake.in" "wren-config.cmake"
    INSTALL_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/wren"
    NO_SET_AND_CHECK_MACRO
    NO_CHECK_REQUIRED_COMPONENTS_MACRO
)

write_basic_package_version_file("wren-config-version.cmake"
    VERSION "${CMAKE_PROJECT_VERSION}"
    COMPATIBILITY AnyNewerVersion
)

install(
    FILES
        "${CMAKE_CURRENT_BINARY_DIR}/wren-config.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/wren-config-version.cmake"
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/wren"
)

configure_file("wren.pc.in" "pkgconfig/wren.pc" @ONLY)

install(
    FILES
        "${CMAKE_CURRENT_BINARY_DIR}/pkgconfig/wren.pc"
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/pkgconfig"
)
