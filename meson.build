# ch32fun as a meson subproject. Firmware projects pull it in with
#
#     ch32fun = subproject('ch32fun')
#     ch32fun_dep = ch32fun.get_variable('ch32fun_dep')   # ch32fun.c + headers
#     ch32fun_ld = ch32fun.get_variable('ch32fun_ld')     # ch32fun.ld template
#     fsusb_src = ch32fun.get_variable('fsusb_src')       # extralibs/fsusb.c
#     minichlink = ch32fun.get_variable('minichlink')     # native tool, or not found
#
# The firmware sources are handed over as files() so the parent compiles
# them with its own flags and its own funconfig.h. The parent still passes
# the TARGET_MCU defines ch32fun.mk would have.
project('ch32fun', 'c',
    meson_version: '>= 1.3',
    default_options: ['warning_level=1', 'werror=false'],
)

ch32fun_inc = include_directories('ch32fun', 'extralibs', is_system: true)
ch32fun_dep = declare_dependency(
    include_directories: ch32fun_inc,
    sources: files('ch32fun/ch32fun.c'),
)
ch32fun_ld = files('ch32fun/ch32fun.ld')
fsusb_src = files('extralibs/fsusb.c')

subdir('minichlink')
