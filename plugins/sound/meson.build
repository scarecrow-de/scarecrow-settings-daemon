sources = files(
  'csd-sound-manager.c',
  'main.c'
)

deps = plugins_deps + [
  gio_dep,
  libpulse_mainloop_glib_dep
]

executable(
  'csd-' + plugin_name,
  sources,
  include_directories: [top_inc, common_inc],
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_rpath: csd_pkglibdir,
  install_dir: csd_libexecdir
)
