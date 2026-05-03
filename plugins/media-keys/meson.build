sources = files(
  'bus-watch-namespace.c',
  'scsd-media-keys-manager.c',
  'scsd-screenshot-utils.c',
  'main.c',
  'mpris-controller.c'
)

marshal = 'scsd-marshal'

sources += gnome.genmarshal(
  marshal,
  sources: marshal + '.list',
  prefix: marshal.underscorify(),
  internal: true
)

sources += gnome.gdbus_codegen(
  'shell-key-grabber',
  'io.github.scarecrow_de.ShellKeyGrabber.xml',
  interface_prefix: 'io.github.scarecrow_de.',
  namespace: 'Shell'
)

deps = plugins_deps + [
  gio_unix_dep,
  gsettings_desktop_dep,
  libcanberra_gtk_dep,
  libcommon_dep,
  gnome_desktop_dep,
  libgvc_dep,
  libpulse_mainloop_glib_dep,
  m_dep,
  upower_glib_dep
]

if enable_gudev
  deps += gudev_dep
endif

executable(
  'scsd-' + plugin_name,
  sources,
  include_directories: [top_inc, data_inc],
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_rpath: gsd_pkglibdir,
  install_dir: gsd_libexecdir
)

program = 'audio-selection-test'

executable(
  program,
  program + '.c',
  include_directories: top_inc,
  dependencies: deps
)
