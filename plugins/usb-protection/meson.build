sources = files(
  'csd-usb-protection-manager.c',
  'main.c'
)

deps = plugins_deps + [
  gsettings_desktop_dep,
  libcommon_dep,
  libnotify_dep,
]

executable(
  'csd-' + plugin_name,
  sources,
  include_directories: [top_inc, common_inc, data_inc],
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_rpath: csd_pkglibdir,
  install_dir: csd_libexecdir
)
