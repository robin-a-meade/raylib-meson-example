project('raylib', 'c', version: '4.0.0')

compiler = meson.get_compiler('c')

inc_dirs = include_directories('include')

# Why not just say 'lib' and avoid meson.current_source_dir()?
# The documentation says meson.current_source_dir() is not needed.
# https://mesonbuild.com/Reference-manual_builtin_meson.html#mesoncurrent_source_dir
# I guess it is needed. Seen in examples here:
# https://stackoverflow.com/a/67963076
# https://github.com/YamanQD/AntWare/blob/72a2dacfff5c601ef5ce86cd8f3c04734d9dc2fb/subprojects/packagefiles/sfml_win-2.5.1/meson.build
# Try:
#   lib_dirs = [join_paths('.', 'lib')]
# or simply:
#   lib_dirs = ['lib']
# Result: ERROR: Search directory lib is not an absolute path.
# Try:
#   lib_dirs = files('lib')
# Result: ERROR: File lib does not exist.
# Maybe we'd need a dirs(...) function, but there is none.
# CONCLUSION: meson.current_source_dir() is needed to make it an absolute path.
lib_dirs = [join_paths(meson.current_source_dir(), 'lib')]

# https://mesonbuild.com/Reference-manual_returned_compiler.html#compilerfind_library
#
# Is this the right way to indicate what I want a statically linked executable?
# Do I really need to do so on a library-by-library basis?
# Can't I just say "statically link all libraries except platform libraries"?
# See these release notes for an explanation what setting the keyword argument
# 'static' to true does and how it differs from the default behavior:
# https://mesonbuild.com/Release-notes-for-0-51-0.html#add-keyword-static-to-find_library
raylib_lib = compiler.find_library('raylib', dirs: lib_dirs, static: true)

raylib_linux_amd64_dep = declare_dependency(
  dependencies: [
    raylib_lib,
    ],
  include_directories: inc_dirs,
)
