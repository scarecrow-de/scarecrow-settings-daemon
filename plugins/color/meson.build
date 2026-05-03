sources = files(
  'gcm-edid.c',
  'scarecrow-datetime-source.c',
  'csd-color-calibrate.c',
  'csd-color-manager.c',
  'csd-color-profiles.c',
  'csd-color-state.c',
  'csd-night-light.c',
  'csd-night-light-common.c',
  'main.c'
)

deps = plugins_deps + [
  colord_dep,
  gnome_desktop_dep,
  lcms_dep,
  libcanberra_gtk_dep,
  libgeoclue_dep,
  libnotify_dep,
  m_dep,
]

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

sources = files(
  'gcm-edid.c',
  'gcm-self-test.c',
  'scarecrow-datetime-source.c',
  'csd-night-light.c',
  'csd-night-light-common.c'
)

test_unit = 'gcm-self-test'

exe = executable(
  test_unit,
  sources,
  include_directories: top_inc,
  dependencies: deps,
  c_args: '-DTESTDATADIR="@0@"'.format(join_paths(meson.current_source_dir(), 'test-data'))
)

envs = ['GSETTINGS_SCHEMA_DIR=@0@'.format(join_paths(meson.build_root(), 'data'))]
test(test_unit, exe, env: envs)
