project('raylib-meson-example', 'c',
  version : '0.1',
  default_options : ['warning_level=3'])

# Explanation of default_options used:
#
# A warning_level of 3 is the highest level.
#
# We didn't specify buildtype, so a default of 'debug' is assumed.
#
# Other default options to try:
#   'buildtype=release'
#   'default_library=static'
#
# NOTE: As far as I can tell, 'default_library=static' doesn't mean that the
# executable we are building has all its libraries statically linked. It means
# any libraries we build are static libraries, not shared libraries. To build a
# statically linked executable we must add the keyword argument `static: true`
# to each library depedency that we declare.  I'm still looking for a way to
# control this from the top-level meson-build file, so that wrapped
# dependencies in subprojects know that we are trying to build a statically
# linked executable.
#
# See full list of options: https://mesonbuild.com/Builtin-options.html

# Retrieve the raylib library dependency from the wrapped raylib dependency we
# set up in the subprojects folder
#
# If you inspect the .wrap file, you'll notice that it provides a dependency
# named 'raylib_linux_amd64_dep'.
#
# TODO: We should add some if/elif logic based on host_machine.system() and
# target_machine.cpu_family() to set raylib_dep suitably for the OS and cpu
# architecture of the host machine. Example of the general approach:
# https://github.com/YamanQD/AntWare/blob/72a2dacfff5c601ef5ce86cd8f3c04734d9dc2fb/meson.build
#
# Question: Should the above linked example use target_machine.system() instead
# of host_machine.system()?  No, it's probably intentially that way. The option
# of targeting win32 vs win64 is only available on Windows. The build isn't
# attempting full cross-compilation, though that is possible (see for instance:
# https://www.linkedin.com/pulse/multi-platform-c-development-meson-frederik-hertzum
# )
#
# For the moment, I'm keeping things simple and assuming linux on amd64, a.k.a.
# x86_64.
raylib_dep = dependency('raylib_linux_amd64_dep')

# We need to link to the math library
# https://stackoverflow.com/a/1033940 <== Explains why libm is separate from libc
# https://mesonbuild.com/howtox.html#add-math-library-lm-portably
cc = meson.get_compiler('c')
m_dep = cc.find_library('m', required: false)

deps = [raylib_dep, m_dep]

exe = executable('shapes_bouncing_ball', 'shapes_bouncing_ball.c',
  install : true, dependencies: deps)

test('basic', exe)

# We compile a 2nd executable, just to show how easy it is.

exe = executable('shapes_easings_ball_anim', 'shapes_easings_ball_anim.c',
  install : true, dependencies: deps)

test('basic', exe)

# NEXT STEP:
# We'll take this a step further by using a forEach loop to build all the raylib examples.
