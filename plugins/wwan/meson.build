sources = files(
  'cc-wwan-device.c',
  'csd-wwan-manager.c',
  'main.c'
)

deps = plugins_deps + [gio_dep, gcr_base_dep, mm_glib_dep, polkit_gobject_dep]

cflags += ['-DGNOMECC_DATA_DIR="@0@"'.format(csd_pkgdatadir)]

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

