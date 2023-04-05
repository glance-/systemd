# SPDX-License-Identifier: LGPL-2.1-or-later

if conf.get('HAVE_LIBCRYPTSETUP') != 1
        subdir_done()
endif

subdir('cryptsetup-tokens')

systemd_cryptsetup_sources = files(
        'cryptsetup.c',
        'cryptsetup-keyfile.c',
        'cryptsetup-pkcs11.c',
)

executables += [
        executable_template + {
                'name' : 'systemd-cryptsetup',
                'public' : true,
                'sources' : systemd_cryptsetup_sources,
                'dependencies' : [
                        libcryptsetup,
                        libopenssl,
                        libp11kit_cflags,
                ],
        },
        generator_template + {
                'name' : 'systemd-cryptsetup-generator',
                'sources' : files('cryptsetup-generator.c'),
        },
]

# symlink for backwards compatibility after rename
install_symlink('systemd-cryptsetup',
                pointing_to : libexecdir_to_bin / 'systemd-cryptsetup',
                install_dir : libexecdir)

if have_static_binaries
        executables += [
                executable_template + {
                        'name' : 'systemd-cryptsetup.static',
                        'public' : true,
                        'conditions' : ['HAVE_LIBCRYPTSETUP'],
                        'sources' : systemd_cryptsetup_sources,
                        'link_args' : ['-static'],
                        'link_with' : [libshared_static_static_libs, libsystemd_static, libbasic_static],
                        'dependencies' : [
                                libcryptsetup_static,
                                tpm2_static,
                                libp11kit_cflags,
                        ],
                }
        ]
endif
