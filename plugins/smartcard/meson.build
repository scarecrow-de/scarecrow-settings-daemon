sources = files(
  'csd-smartcard-manager.c',
  'csd-smartcard-service.c',
  'csd-smartcard-utils.c',
  'main.c'
)

enum_headers = files(
  'csd-smartcard-manager.h',
  'csd-smartcard-utils.h'
)

enum_types = 'csd-smartcard-enum-types'

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
  'csd-' + plugin_name,
  sources,
  include_directories: [top_inc, common_inc],
  dependencies: deps,
  c_args: cflags,
  install: true,
  install_rpath: csd_pkglibdir,
  install_dir: csd_libexecdir
)
