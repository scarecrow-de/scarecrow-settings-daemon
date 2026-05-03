common_files = files(
  'scsd-disk-space.c',
  'scsd-disk-space-helper.c'
)

sources = common_files + files(
  'scsd-housekeeping-manager.c',
  'main.c'
)

deps = plugins_deps + [
  gio_unix_dep,
  gtk_dep,
  libnotify_dep
]

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

programs = [
  'scsd-disk-space-test',
  'scsd-empty-trash-test',
  'scsd-purge-temp-test'
]

foreach program: programs
  executable(
    program,
    common_files + [program + '.c'],
    include_directories: top_inc,
    dependencies: deps
  )
endforeach
