sources = files(
  'csd-a11y-settings-manager.c',
  'main.c'
)

deps = plugins_deps + [
  gio_dep,
  gsettings_desktop_dep
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
