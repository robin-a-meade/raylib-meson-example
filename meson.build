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
#
#   'buildtype=release'
#
# See full list of options: https://mesonbuild.com/Builtin-options.html

# Retrieve the raylib library dependency from one of the wrapped raylib
# dependencies we set up in the subprojects folder. We want the one that
# is proper for the host machine's OS and cpu architecture.
assert(host_machine.system() in ['linux'], 'Unsupported system: ' + host_machine.system())
assert(host_machine.cpu_family() in ['x86', 'x86_64'], 'Unsupported cpu_family: ' + host_machine.cpu_family())
if host_machine.system() == 'linux'
  if host_machine.cpu_family() == 'x86'
    raylib_dep = dependency('raylib_linux_x86_dep')
  elif host_machine.cpu_family() == 'x86_64'
    raylib_dep = dependency('raylib_linux_x86_64_dep')
  endif
# We haven't prepared wrapped dependencies for these yet:
# elif host_machine.system() == 'windows'
#   if host_machine.cpu_family() == 'x86'
#     raylib_dep = dependency('raylib_windows_ming_x86_dep')
#   elif host_machine.cpu_family() == 'x86_64'
#     raylib_dep = dependency('raylib_windows_ming_x86_64_dep')
#   endif
# elif host_machine.system() == 'darwin'
#   raylib_dep = dependency('raylib_darwin_dep')
endif

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
