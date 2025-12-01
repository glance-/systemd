# SPDX-License-Identifier: LGPL-2.1-or-later

if conf.get('HAVE_BLKID') != 1
        subdir_done()
endif

executables += [
        executable_template + {
                'name' : 'systemd-dissect',
                'public' : true,
                'sources' : files('dissect.c'),
        },
]

install_emptydir(sbindir)
meson.add_install_script(sh, '-c',
                         ln_s.format(bindir / 'systemd-dissect',
                                     sbindir / 'mount.ddi'))

if have_static_binaries
        executables += [
                executable_template + {
                        'name' : 'systemd-dissect.static',
                        'public' : true,
                        'sources' : files('dissect.c'),
                        'link_args' : ['-static'],
                        'link_with' : [libshared_static_static_libs, libsystemd_static, libbasic_static],
                        'dependencies' : [
                                libmount,
                        ],
                }
        ]
endif
