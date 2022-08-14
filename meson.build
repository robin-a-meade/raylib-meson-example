project('raylib-meson-example', 'c',
  version : '0.1',
  default_options : ['warning_level=3'])

# Explanation of default_options used:
#
# A warning_level of 3 is the highest level.
#
# We didn't specify buildtype, so the default of 'debug' is assumed.
#
# I wondered if a adding 'default_library=static' to default_options would build a
# statically linked executable. Hinted at here:
# https://github.com/mesonbuild/meson/issues/5385#issuecomment-491628333
# https://github.com/mesonbuild/meson/discussions/9830#discussioncomment-1976373
# It didn't in my testing. Maybe I did it wrong or misunderstood.
#
# See full list of options: https://mesonbuild.com/Builtin-options.html

# Retrieve the raylib dependency from one of wrapped raylib dependencies we've
# set up in the subprojects folder. We want the one that is suitable to the
# host machine's OS and cpu.
if host_machine.system() == 'linux'
  if host_machine.cpu_family() == 'x86'
    raylib_dep = dependency('raylib_linux_x86_dep')
  elif host_machine.cpu_family() == 'x86_64'
    raylib_dep = dependency('raylib_linux_x86_64_dep')
  else
    assert(false, 'Unsupported system/cpu compilation: ' + host_machine.system() + '/' + host_machine.cpu_family())
  endif
elif host_machine.system() == 'windows'
  if host_machine.cpu_family() == 'x86'
    raylib_dep = dependency('raylib_win32_mingw_dep')
  elif host_machine.cpu_family() == 'x86_64'
    raylib_dep = dependency('raylib_win64_mingw_dep')
  endif
# We haven't prepared wrapped dependencies for these yet:
# elif host_machine.system() == 'darwin'
#   raylib_dep = dependency('raylib_darwin_dep')
else
  assert(false, 'Unsupported system/cpu compilation: ' + host_machine.system() + '/' + host_machine.cpu_family())
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
