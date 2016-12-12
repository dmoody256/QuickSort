# This file is licensed under the MIT License.
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.

import os
import json
import sys
import glob
import re
from sys import platform

def CreateNewEnv():

    env = Environment();

    env.VariantDir('build', 'src', duplicate=0)
    sourceFiles = ["build/main.cpp",  "build/QuickSort.cpp"]
    includeFiles = ["src/QuickSort.hpp"]
    env = ConfigPlatformEnv(env)
    prog = env.Program("build/QuickSortTest", sourceFiles)

    env = ConfigPlatformIDE(env, sourceFiles, includeFiles, prog)

    return env

def ConfigPlatformEnv(env):

    if platform == "linux" or platform == "linux2":
        print("Eclipse C++ project not implemented yet")
    elif platform == "darwin":
        print("XCode project not implemented yet")
    elif platform == "win32":

        degugDefine = 'DEBUG',
        debugFlag = "/Od"
        degug = '/DEBUG:FULL',
        debugRuntime = "/MDd",
        env.Append(CPPDEFINES=[
            'NOMINMAX',
            "WIN32",
            "_WINDOWS",
            degugDefine,
        ])

        env.Append(CCFLAGS= [
            "/analyze-",
            "/GS",
            "/Zc:wchar_t",
            "/W1",
            "/Z7",
            "/Gm-",
            debugFlag,
            "/WX-",
            '/FC',
            "/Zc:forScope",             # Force Conformance in for Loop Scope
            "/GR",                      # Enable Run-Time Type Information
            "/Oy-",                     # Disable Frame-Pointer Omission
            debugRuntime,               # Use Multithread DLL version of the runt-time library
            "/EHsc",
            "/nologo",
        ])

        env.Append(LINKFLAGS=[
            "/SUBSYSTEM:CONSOLE",
            "/ERRORREPORT:PROMPT",
            "/NOLOGO",
            "/SAFESEH:NO",
            degug
        ])

    return env

def ConfigPlatformIDE(env, sourceFiles, includeFiles, program):
    if platform == "linux" or platform == "linux2":
        print("Eclipse C++ project not implemented yet")
    elif platform == "darwin":
        print("XCode project not implemented yet")
    elif platform == "win32":
        files = []
        incFiles = []
        for file in sourceFiles:
            files.append(re.sub("^build", "../src", file))
        for file in includeFiles:
            incFiles.append(os.path.abspath(Dir('.').abspath) + "/"  + file)
        buildSettings = {
            'LocalDebuggerCommand':os.path.abspath(Dir('.').abspath).replace('\\', '/') + "/build/QuickSortTest.exe",
            'LocalDebuggerWorkingDirectory':os.path.abspath(Dir('.').abspath).replace('\\', '/')+'/test',
            'LocalDebuggerCommandArguments':'--break < testInput.txt'
        }
        env.MSVSProject(target = 'VisualStudio/QuickSortTest' + env['MSVSPROJECTSUFFIX'],
                    srcs = files,
                    incs = incFiles,
                    buildtarget = program,
                    DebugSettings = buildSettings,
                    variant = 'Debug|Win32')
    return env

CreateNewEnv()
