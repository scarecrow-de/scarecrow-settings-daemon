policy = 'io.github.scarecrow_de.settings-daemon.plugins.wacom.policy'

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
  'csd-wacom-manager.c',
  'csd-wacom-oled.c',
  'main.c'
)

deps = plugins_deps + [
  gtk_dep,
  libcommon_dep,
  m_dep,
  pango_dep
]

if enable_wacom
  deps += libwacom_dep
endif

cflags += ['-DLIBEXECDIR="@0@"'.format(csd_libexecdir)]

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

if enable_gudev
  deps = [
    gudev_dep,
    m_dep
  ]

  executable(
    'csd-wacom-oled-helper',
    'csd-wacom-oled-helper.c',
    include_directories: top_inc,
    dependencies: deps,
    install: true,
    install_rpath: csd_pkglibdir,
    install_dir: csd_libexecdir
  )
endif
