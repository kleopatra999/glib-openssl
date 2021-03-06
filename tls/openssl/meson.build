tlsopenssl_sources = [
  'openssl-module.c',
  'gtlsbackend-openssl.c',
  'gtlscertificate-openssl.c',
  'gtlsconnection-openssl.c',
  'gtlsserverconnection-openssl.c',
  'gtlsclientconnection-openssl.c',
  'gtlsdatabase-openssl.c',
  'gtlsfiledatabase-openssl.c',
  'gtlsbio.c',
  'openssl-util.c',
]

platform_deps = [ openssl, gio, glib, gobject ]

tlsopenssl = static_library('tlsopenssl',
  tlsopenssl_sources,
  dependencies: [tlsbase_dep, platform_deps],
  include_directories: config_h_include,
)

tlsopenssl_dep = declare_dependency(
  link_with: tlsopenssl,
  include_directories: include_directories('.', '../base'),
  dependencies: platform_deps
)

gioopenssl = shared_module('gioopenssl',
  tlsopenssl_sources,
  dependencies: [tlsopenssl_dep],
  include_directories: config_h_include,
  install: true,
  install_dir: giomoduledir,
  c_args: [extra_args + common_flags],
)

# Internal dependency, for tests and benchmarks
tlsopenssl_inc = include_directories([ '.', '..' ])
tlsopenssl_dep = declare_dependency(link_with: tlsopenssl,
                                    include_directories: [ tlsopenssl_inc, config_h_include ],
                                    dependencies: platform_deps)
