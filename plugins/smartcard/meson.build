sources = files(
  'scsd-smartcard-manager.c',
  'scsd-smartcard-service.c',
  'scsd-smartcard-utils.c',
  'main.c'
)

enum_headers = files(
  'scsd-smartcard-manager.h',
  'scsd-smartcard-utils.h'
)

enum_types = 'scsd-smartcard-enum-types'

sources += gnome.mkenums(
  enum_types,
  sources: enum_headers,
  c_template: enum_types + '.c.in',
  h_template: enum_types + '.h.in'
)

gdbus = 'io.github.scarecrow_de.SettingsDaemon.Smartcard'

sources += gnome.gdbus_codegen(
  gdbus,
  gdbus + '.xml',
  interface_prefix: gdbus + '.',
  namespace: 'GsdSmartcardService',
  object_manager: true
)

deps = plugins_deps + [
  gio_unix_dep,
  libnotify_dep,
  nss_dep
]

cflags += ['-DGSD_SMARTCARD_MANAGER_NSS_DB="@0@"'.format(system_nssdb_dir)]

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
