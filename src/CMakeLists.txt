add_library(wren
    "include/wren.h"
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
)
target_include_directories(wren
    PUBLIC
        "include"
    PRIVATE
        "vm"
        "optional"
)
target_link_libraries(wren PRIVATE m)

add_library(wren::wren ALIAS wren)
