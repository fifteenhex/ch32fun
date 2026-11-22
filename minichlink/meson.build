# minichlink runs on the build machine, so it is a native target even when
# the parent is a cross build. Needs libusb-1.0 and, on Linux, libudev.
minichlink = disabler()
if add_languages('c', native: true, required: false)
    libusb = dependency('libusb-1.0', native: true, required: false)
    deps = [libusb, dependency('threads', native: true)]
    if build_machine.system() == 'linux'
        deps += dependency('libudev', native: true, required: false)
    endif
    found = true
    foreach d : deps
        found = found and d.found()
    endforeach
    if found
        git = find_program('git', required: false)
        version = 'unknown'
        if git.found()
            r = run_command(git, '-C', meson.current_source_dir(),
                'rev-parse', '--short', 'HEAD', check: false)
            if r.returncode() == 0
                version = r.stdout().strip()
            endif
        endif
        minichlink = executable('minichlink',
            'minichlink.c', 'pgm-wch-linke.c', 'pgm-wch-isp.c',
            'pgm-esp32s2-ch32xx.c', 'nhc-link042.c', 'ardulink.c',
            'serial_dev.c', 'pgm-b003fun.c', 'minichgdb.c', 'chips.c',
            'ch5xx.c',
            c_args: ['-DCH32V003', '-DMINICHLINK', '-DVERSION="' + version + '"',
                '-Wno-unused-function'],
            dependencies: deps,
            native: true,
        )
    endif
endif
if not minichlink.found()
    warning('not building minichlink: needs a native C compiler, libusb-1.0 and libudev')
endif
