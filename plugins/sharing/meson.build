sources = files(
  'scsd-sharing-manager.c',
  'main.c'
)

deps = plugins_deps + [
  gio_unix_dep,
  libnotify_dep
]

if enable_network_manager
  deps += libnm_dep
endif

executable(
  'scsd-' + plugin_name,
  sources,
  include_directories: [top_inc, common_inc],
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_rpath: gsd_pkglibdir,
  install_dir: gsd_libexecdir
)
