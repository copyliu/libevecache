#!/usr/bin/env python
import distutils.sysconfig
import os
import re
import sys

lenv = Environment(TARGET_ARCH="x86", CPPPATH = ['lib/'], tools=["mingw"])
env = Environment(TARGET_ARCH="x86", CPPPATH = ['lib/'], tools=["mingw"])
pyenv = Environment(TARGET_ARCH="x86", SWIGFLAGS=['-c++', '-python', '-classic'], CPPPATH = ['lib/', distutils.sysconfig.get_python_inc()], SHLIBPREFIX="", tools=["mingw"])
platform = ARGUMENTS.get('OS', Platform())


if platform.name == "win32":
   #env = Environment(TARGET_ARCH="x86", CPPPATH = ['lib/'], MSVC_VERSION='10.0')
   #lenv = Environment(TARGET_ARCH="x86", CPPPATH = ['lib/'], MSVC_VERSION='10.0')
   #lenv.Append(CPPFLAGS=["/EHsc", "/MD", "/O2", "/GF", "/GR"])
   #pyenv.Append(CPPFLAGS=["/EHsc", "/MD", "/O2", "/GF", "/GR"])
   #env.Append(CPPFLAGS=["/EHsc", "/MD", "/O2", "/GF", "/GR"])
   lenv.Append(CPPDEFINES=["EVECACHE_DLL", "EVECACHE_EXPORT", "WIN32"])
   env.Append(CPPDEFINES=["EVECACHE_DLL", "EVECACHE_EXPORT", "WIN32"])
   pyenv.Append(CPPDEFINES=["EVECACHE_DLL", "EVECACHE_EXPORT", "WIN32", "__WIN32__"])
   pyenv.Append(LIBPATH=['c:/python27/libs/'])

else:
   lenv.Append(CPPFLAGS=["-g3", "-Wall"])
   env.Append(CPPFLAGS=["-g3", "-Wall"])
   #pyenv.Append(LIBPATH=['c:/python27/libs/'])
lib = lenv.SharedLibrary('evecache', Glob('lib/*cpp'))

# SCONS whacky issue with Windows. I sometimes really dislike scons...
if platform.name != "win32" or 1:
   pyext = pyenv.SharedLibrary('_evecache', ['lib/libevecache_wrap.cc'], LIBS=[lib, 'python27'])

if platform.name == "win32" and 0:
   env.Program('util/dumper.cpp', LIBS='evecache') # try to link with .lib, not .dll
else:
   env.Program('util/dumper.cpp', LIBS=lib)
