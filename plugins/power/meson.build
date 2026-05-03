sources = files(
  'gpm-common.c',
  'csd-backlight.c',
  'csd-power-manager.c',
  'main.c'
)

deps = plugins_deps + [
  libcanberra_gtk_dep,
  libcommon_dep,
  libnotify_dep,
  gio_unix_dep,
  gnome_desktop_dep,
  m_dep,
  upower_glib_dep,
  x11_dep,
  dependency('xext')
]

# required for csd-power-enums-update, which we have
# to compile natively
native_deps = [
  dependency('glib-2.0', native: true),
  dependency('gio-2.0', native:true)
]

if host_is_linux
  deps += gudev_dep
endif

cflags += ['-DLIBEXECDIR="@0@"'.format(csd_libexecdir)]

csd_power = executable(
  'csd-' + plugin_name,
  sources,
  include_directories: [top_inc, data_inc],
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_rpath: csd_pkglibdir,
  install_dir: csd_libexecdir
)

sources = files('csd-power-enums-update.c')

enums_headers = files(
  'gsm-inhibitor-flag.h',
  'gsm-presence-flag.h'
)

enums = 'csd-power-enums'

sources += gnome.mkenums(
  enums,
  sources: enums_headers,
  c_template: enums + '.c.in',
  h_template: enums + '.h.in'
)

csd_power_enums_update = executable(
  'csd-power-enums-update',
  sources,
  include_directories: top_inc,
  dependencies: native_deps,
  c_args: cflags,
  native: true
)

if host_is_linux
  policy = 'io.github.scarecrow_de.settings-daemon.plugins.power.policy'

  policy_in = configure_file(
    input: policy + '.in.in',
    output: policy + '.in',
    configuration: plugins_conf
  )

  i18n.merge_file(
    input: policy_in,
    output: policy,
    po_dir: po_dir,
    install: true,
    install_dir: join_paths(csd_datadir, 'polkit-1', 'actions')
  )

  sources = files(
    'csd-backlight-helper.c',
  )

  deps = [
  ]

  executable(
    'csd-backlight-helper',
    sources,
    include_directories: top_inc,
    dependencies: deps,
    install: true,
    install_rpath: csd_pkglibdir,
    install_dir: csd_libexecdir
  )
endif

output = 'csdpowerconstants.py'

csdpowerconstants_py = custom_target(
  output,
  input: 'csd-power-constants.h',
  output: output,
  build_by_default: true,
  command: [join_paths(meson.current_source_dir(), 'csd-power-constants-update.pl'), '@INPUT@', '@OUTPUT@']
)

output = 'csdpowerenums.py'

csdpowerenums_py = custom_target(
  output,
  output: output,
  capture: true,
  build_by_default: true,
  command: [csd_power_enums_update]
)

test_py = find_program('test.py')

envs = environment()
#envs.prepend('G_DEBUG', 'fatal-warnings')
envs.set('BUILDDIR', meson.current_build_dir())
envs.set('TOP_BUILDDIR', meson.build_root())
envs.set('LD_PRELOAD', 'libumockdev-preload.so.0')
envs.set('NO_AT_BRIDGE', '1')
envs.set('HAVE_SYSFS_BACKLIGHT', host_is_linux ? '1' : '0')

if get_option('b_sanitize').split(',').contains('address')
  # libasan needs to be loaded first; so we need to explicitly preload it
  envs.set('POWER_LD_PRELOAD', 'libasan.so.5')
endif

foreach i : [ 1, 2, 3, 4, 5, 6, 7, 8 ]
  test(
    'test-power @0@/8'.format(i),
    test_py,
    args: [ 'PowerPluginTest@0@'.format(i) ],
    env: envs,
    # The first set of tests takes very long because of SCREENSAVER_TIMEOUT_BLANK
    timeout: i == 1 ? 180 : 120
  )
endforeach

