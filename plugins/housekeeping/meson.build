common_files = files(
  'csd-disk-space.c',
  'csd-disk-space-helper.c'
)

sources = common_files + files(
  'csd-housekeeping-manager.c',
  'main.c'
)

deps = plugins_deps + [
  gio_unix_dep,
  gtk_dep,
  libnotify_dep
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

programs = [
  'csd-disk-space-test',
  'csd-empty-trash-test',
  'csd-purge-temp-test'
]

foreach program: programs
  executable(
    program,
    common_files + [program + '.c'],
    include_directories: top_inc,
    dependencies: deps
  )
endforeach
