sources = files(
  'csd-keyboard-manager.c',
  'main.c'
)

deps = plugins_deps + [
  gtk_dep,
  libcommon_dep,
  x11_dep
]

executable(
  'csd-' + plugin_name,
  sources,
  include_directories: [top_inc, data_inc],
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_rpath: csd_pkglibdir,
  install_dir: csd_libexecdir
)
