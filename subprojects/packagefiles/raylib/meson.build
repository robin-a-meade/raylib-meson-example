project('raylib', 'c', version: '4.2.0')

compiler = meson.get_compiler('c')

inc_dirs = include_directories('include')

# NOTE: meson.current_source_dir() is needed to make it an absolute path.
lib_dirs = [join_paths(meson.current_source_dir(), 'lib')]

raylib_lib = compiler.find_library('raylib', dirs: lib_dirs, static: true)

raylib_dep = declare_dependency(
  dependencies: [
    raylib_lib,
    ],
  include_directories: inc_dirs,
)
