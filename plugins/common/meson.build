common_inc = include_directories('.')

sources = files(
  'csd-input-helper.c',
  'csd-settings-migrate.c',
  'csd-shell-helper.c'
)

resource_data = files('gtk.css')

sources += gnome.compile_resources(
  'csd-resources',
  'csd.gresources.xml',
  c_name: 'csd',
  dependencies: resource_data
)

deps = plugins_deps + [
  gnome_desktop_dep,
  gtk_x11_dep,
  x11_dep,
  dependency('kbproto'),
  dependency('xi')
]

ldflags = []
if host_is_darwin
  ldflags += ['-Wl,-bundle_loader,@0@'.format(join_paths(), meson.build_root(), meson.project_name(), meson.project_name())]
endif

libcommon = static_library(
  plugin_name,
  sources: sources,
  include_directories: [top_inc, data_inc],
  dependencies: deps,
  c_args: cflags,
  link_args: ldflags
)

libcommon_dep = declare_dependency(
  include_directories: common_inc,
  link_with: libcommon
)
