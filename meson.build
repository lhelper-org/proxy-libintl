project('proxy-libintl', 'c',
  version : '1',
  meson_version : '>= 0.48.0',
  default_options : [ 'warning_level=1',
                      'c_std=gnu99',
                      'buildtype=debugoptimized' ])

pkg = import('pkgconfig')

# Flags only needed internally for compilation
intl_priv_c_args = ['-DSTUB_ONLY']
# Flags that needs to be publicly visible
intl_c_args = []
if get_option('default_library') == 'static'
  intl_c_args += ['-DG_INTL_STATIC_COMPILATION']
endif

intl_lib = library('intl',
  'libintl.c',
  c_args: intl_c_args + intl_priv_c_args,
  soversion : 8,
  darwin_versions : ['10', '10.5'],
  install : true)

intl_dep = declare_dependency(link_with : intl_lib,
  compile_args: intl_c_args,
  include_directories : include_directories('.'))

install_headers('libintl.h')

pkg.generate(intl_lib,
  filebase: 'proxy-libintl',
  name: 'proxy-libintl',
  extra_cflags: intl_c_args,
  description: 'A stub replacement for libintl')
