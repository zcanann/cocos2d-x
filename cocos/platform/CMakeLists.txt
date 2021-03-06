#/****************************************************************************
# Copyright (c) 2015-2017 Chukong Technologies Inc.
#
# http://www.cocos2d-x.org
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:

# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.

# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
# THE SOFTWARE.
# ****************************************************************************/

if(WINDOWS)
    set(COCOS_PLATFORM_SPECIFIC_HEADER
        platform/win32/compat/stdint.h
        platform/win32/CCApplication-win32.h
        platform/win32/CCGL-win32.h
        platform/win32/CCFileUtils-win32.h
        platform/win32/CCStdC-win32.h
        platform/win32/CCPlatformDefine-win32.h
        platform/win32/CCUtils-win32.h
        platform/desktop/CCGLViewImpl-desktop.h
        )
    set(COCOS_PLATFORM_SPECIFIC_SRC
        platform/win32/CCStdC-win32.cpp
        platform/win32/CCUtils-win32.cpp
        platform/win32/CCFileUtils-win32.cpp
        platform/win32/CCCommon-win32.cpp
        platform/win32/CCApplication-win32.cpp
        platform/win32/CCDevice-win32.cpp
        platform/desktop/CCGLViewImpl-desktop.cpp
        )

elseif(APPLE)
    set(COCOS_PLATFORM_SPECIFIC_HEADER
        platform/mac/CCFileUtils-apple.h
        platform/mac/CCLock-apple.h
        platform/mac/CCDevice-apple.h
        )
    set(COCOS_PLATFORM_SPECIFIC_SRC
        platform/mac/CCLock-apple.cpp
        platform/mac/CCFileUtils-apple.mm
        platform/mac/CCThread-apple.mm
        platform/mac/CCDevice-apple.mm
        )
    if(MACOSX)
        set(COCOS_PLATFORM_SPECIFIC_HEADER
            ${COCOS_PLATFORM_SPECIFIC_HEADER}
            platform/mac/CCStdC-mac.h
            platform/mac/CCPlatformDefine-mac.h
            platform/mac/CCApplication-mac.h
            platform/mac/CCGL-mac.h
            platform/desktop/CCGLViewImpl-desktop.h
            )
        set(COCOS_PLATFORM_SPECIFIC_SRC
            ${COCOS_PLATFORM_SPECIFIC_SRC}
            platform/mac/CCApplication-mac.mm
            platform/mac/CCCommon-mac.mm
            platform/mac/CCDevice-mac.mm
            platform/desktop/CCGLViewImpl-desktop.cpp
            )
    elseif(IOS)
        set(COCOS_PLATFORM_SPECIFIC_HEADER
            ${COCOS_PLATFORM_SPECIFIC_HEADER}
            platform/ios/CCGL-ios.h
            platform/ios/CCApplication-ios.h
            platform/ios/CCDirectorCaller-ios.h
            platform/ios/CCESRenderer-ios.h
            platform/ios/OpenGL_Internal-ios.h
            platform/ios/CCPlatformDefine-ios.h
            platform/ios/CCStdC-ios.h
            platform/ios/CCEAGLView-ios.h
            platform/ios/CCGLViewImpl-ios.h
            platform/ios/CCES2Renderer-ios.h
            )
        set(COCOS_PLATFORM_SPECIFIC_SRC
            ${COCOS_PLATFORM_SPECIFIC_SRC}
            platform/ios/CCApplication-ios.mm
            platform/ios/CCCommon-ios.mm
            platform/ios/CCDevice-ios.mm
            platform/ios/CCDirectorCaller-ios.mm
            platform/ios/CCEAGLView-ios.mm
            platform/ios/CCES2Renderer-ios.m
            platform/ios/CCGLViewImpl-ios.mm
            platform/ios/CCImage-ios.mm
            )
    endif()

elseif(LINUX)

    if(NOT CMAKE_CROSSCOMPILING)
        include_directories(
                /usr/include
                /usr/include/GLFW
                /usr/local/include/GLFW
        )
    endif(NOT CMAKE_CROSSCOMPILING)

    set(COCOS_PLATFORM_SPECIFIC_HEADER
        platform/linux/CCApplication-linux.h
        platform/linux/CCGL-linux.h
        platform/linux/CCStdC-linux.h
        platform/linux/CCFileUtils-linux.h
        platform/linux/CCPlatformDefine-linux.h
        platform/desktop/CCGLViewImpl-desktop.h
        )
    set(COCOS_PLATFORM_SPECIFIC_SRC
        platform/linux/CCStdC-linux.cpp
        platform/linux/CCFileUtils-linux.cpp
        platform/linux/CCCommon-linux.cpp
        platform/linux/CCApplication-linux.cpp
        platform/linux/CCDevice-linux.cpp
        platform/desktop/CCGLViewImpl-desktop.cpp
        )

endif()

#leave andatory external stuff here also

set(COCOS_PLATFORM_INCLUDE_PATHS
    ${PROJECT_SOURCE_DIR}/external
    ${PROJECT_SOURCE_DIR}/external/ConvertUTF
    ${PROJECT_SOURCE_DIR}/external/edtaa3func
    ${PROJECT_SOURCE_DIR}/external/poly2tri
    ${PROJECT_SOURCE_DIR}/external/poly2tri/common
    ${PROJECT_SOURCE_DIR}/external/poly2tri/sweep
    )

set(COCOS_PLATFORM_HEADER
    ${COCOS_PLATFORM_SPECIFIC_HEADER}
    platform/CCApplication.h
    platform/CCApplicationProtocol.h
    platform/CCCommon.h
    platform/CCDevice.h
    platform/CCFileUtils.h
    platform/CCGL.h
    platform/CCGLView.h
    platform/CCImage.h
    platform/CCPlatformConfig.h
    platform/CCPlatformDefine.h
    platform/CCPlatformMacros.h
    platform/CCSAXParser.h
    platform/CCStdC.h
    platform/CCThread.h
    )

set(COCOS_PLATFORM_SRC
    ${COCOS_PLATFORM_SPECIFIC_SRC}
    platform/CCSAXParser.cpp
    platform/CCThread.cpp
    platform/CCGLView.cpp
    platform/CCFileUtils.cpp
    platform/CCImage.cpp
    ../external/edtaa3func/edtaa3func.cpp
    ../external/ConvertUTF/ConvertUTFWrapper.cpp
    ../external/ConvertUTF/ConvertUTF.c
    ../external/poly2tri/common/shapes.cc
    ../external/poly2tri/sweep/advancing_front.cc
    ../external/poly2tri/sweep/cdt.cc
    ../external/poly2tri/sweep/sweep_context.cc
    ../external/poly2tri/sweep/sweep.cc
    )
