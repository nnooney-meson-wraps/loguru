project('loguru', 'cpp',
  version: '2.1.0',
  license: 'Public Domain')

cxx = meson.get_compiler('cpp')
compile_opts = [
  '-DLOGURU_SCOPE_TEXT_SIZE=@0@'.format(get_option('loguru_scope_text_size')),
  '-DLOGURU_FILENAME_WIDTH=@0@'.format(get_option('loguru_filename_width')),
  '-DLOGURU_THREADNAME_WIDTH=@0@'.format(get_option('loguru_threadname_width')),
  '-DLOGURU_SCOPE_TIME_PRECISION=@0@'.format(get_option('loguru_scope_time_precision')),
]
loguru_deps = [dependency('threads')]

if get_option('loguru_export') != ''
  compile_opts += ['-DLOGURU_EXPORT=' + get_option('loguru_export')]
endif
if get_option('loguru_debug_logging')
  compile_opts += ['-DLOGURU_DEBUG_LOGGING=1']
endif
if get_option('loguru_debug_checks')
  compile_opts += ['-DLOGURU_DEBUG_CHECKS=1']
endif
if get_option('loguru_catch_sigabrt')
  compile_opts += ['-DLOGURU_CATCH_SIGABRT=1']
endif
if get_option('loguru_redefine_assert')
  compile_opts += ['-DLOGURU_REDEFINE_ASSERT=1']
endif
if get_option('loguru_with_streams')
  compile_opts += ['-DLOGURU_WITH_STREAMS=1']
endif
if get_option('loguru_replace_glog')
  compile_opts += ['-DLOGURU_REPLACE_GLOG=1']
endif
if get_option('loguru_with_fileabs')
  compile_opts += ['-DLOGURU_WITH_FILEABS=1']
endif
if get_option('loguru_stacktraces')
  loguru_deps += cxx.find_library('dl')
  compile_opts += ['-DLOGURU_STACKTRACES=1']
endif
if get_option('loguru_rtti')
  compile_opts += ['-DLOGURU_RTTI=1']
endif
if get_option('loguru_verbose_scope_endings')
  compile_opts += ['-DLOGURU_VERBOSE_SCOPE_ENDINGS=1']
endif

if get_option('loguru_use_fmtlib').enabled()
  loguru_deps += dependency('fmt', required: true)
endif
flags = cxx.get_supported_arguments(compile_opts)

loguru_lib = library(
  'loguru',
  files(
    'loguru.cpp'
  ),
  include_directories: include_directories('.'),
  cpp_args: flags,
  dependencies: loguru_deps,
)
loguru_dep = declare_dependency(
  include_directories: include_directories('.'),
  link_with: loguru_lib,
  compile_args: flags,
)
