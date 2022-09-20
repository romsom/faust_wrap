project('faust_wrap', 'cpp', default_options : ['warning_level=3', 'cpp_std=c++17'])
inc_dir_strings = []
if meson.is_cross_build()
  compiler = meson.get_compiler('cpp', native: false)
  faust_lib_dir = meson.get_cross_property('faust_lib_dir')
  faust_include_dir = meson.get_cross_property('faust_include_dir')
  inc_dir_strings += [faust_include_dir]
  
  faust = compiler.find_library('faust', dirs: [faust_lib_dir])
else
  compiler = meson.get_compiler('cpp', native: true)
  faust = compiler.find_library('faust')
endif
add_project_arguments('-Wfatal-errors', '-Wno-unused', language : 'cpp')

sources = ['faust_wrap/dsp/llvm-dsp.cpp', 'faust_wrap/dsp/libfaust.cpp']
inc_dirs = include_directories(inc_dir_strings)
libfaust_wrap = static_library('faust_wrap', sources : sources, dependencies : [faust], include_directories: inc_dirs)
libfaust_wrap = shared_library('faust_wrap', sources : sources, dependencies : [faust], include_directories: inc_dirs)
libfaust_wrap_dep = declare_dependency(include_directories : '.', link_with : libfaust_wrap)
