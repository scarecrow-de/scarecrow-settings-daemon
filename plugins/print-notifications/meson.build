sources = files(
  'csd-print-notifications-manager.c',
  'main.c'
)

deps = plugins_deps + [
  cups_dep,
  gtk_dep,
  libnotify_dep
]

cflags += ['-DLIBEXECDIR="@0@"'.format(csd_libexecdir)]
cflags += ['-DBINDIR="@0@"'.format(csd_bindir)]

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

program = 'csd-printer'

executable(
  program,
  program + '.c',
  include_directories: top_inc,
  dependencies: deps,
  c_args: '-DGNOME_SETTINGS_LOCALEDIR="@0@"'.format(csd_localedir),
  install: true,
  install_rpath: csd_pkglibdir,
  install_dir: csd_libexecdir
)
