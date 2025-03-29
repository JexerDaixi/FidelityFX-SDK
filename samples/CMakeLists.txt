# This file is part of the FidelityFX SDK.
# 
# Copyright (C) 2024 Advanced Micro Devices, Inc.
# 
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files(the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and /or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions :
# 
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
# THE SOFTWARE.

# Pull in all the of the samples available and put them in a sample folder

set(FFX_SC_EXECUTABLE ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/tools/binary_store/FidelityFX_SC.exe)
set(FFX_INCLUDE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/include)
set(FFX_LIB_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/libs)
set(FFX_BIN_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/bin/ffx_sdk)
set(FFX_SHARED_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/src/shared)
set(FFX_HOST_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/include/FidelityFX/host)
set(FFX_GPU_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/include/FidelityFX/gpu)
set(FFX_COMPONENTS_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/src/components)
set(FFX_HOST_BACKENDS_PATH ${FFX_HOST_PATH}/../sdk/backends)
set(FFX_SRC_BACKENDS_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../sdk/src/backends)

file(GLOB FFX_SHARED_SOURCES
    "${FFX_SHARED_PATH}/*.cpp"
    "${FFX_SHARED_PATH}/*.h")

set(FFX_PUBLIC_SOURCES
    "${FFX_HOST_PATH}/ffx_assert.h"
    "${FFX_HOST_PATH}/ffx_error.h"
	"${FFX_HOST_PATH}/ffx_fx.h"
	"${FFX_HOST_PATH}/ffx_interface.h"
    "${FFX_HOST_PATH}/ffx_types.h"
    "${FFX_HOST_PATH}/ffx_util.h")

# Init shader sources (for easy viewing)
set(FFX_PUBLIC_SHADER_SOURCES
    "${FFX_GPU_PATH}/ffx_common_types.h"
    "${FFX_GPU_PATH}/ffx_core.h"
    "${FFX_GPU_PATH}/ffx_core_cpu.h"
    "${FFX_GPU_PATH}/ffx_core_glsl.h"
    "${FFX_GPU_PATH}/ffx_core_gpu_common.h"
    "${FFX_GPU_PATH}/ffx_core_gpu_common_half.h"
    "${FFX_GPU_PATH}/ffx_core_hlsl.h"
    "${FFX_GPU_PATH}/ffx_core_portability.h")


# FidelityFX Samples
if (FFX_BREADCRUMBS OR FFX_ALL)
	add_subdirectory(breadcrumbs)
	set(START_PROJECT FFX_BREADCRUMBS PARENT_SCOPE)
endif()

if (FFX_FSR OR FFX_ALL)
	add_subdirectory(fsrapi)
	set(START_PROJECT FFX_API_FSR PARENT_SCOPE)
endif()

if ((FFX_SPD AND (NOT FFX_HYBRIDREFLECTIONS)) OR FFX_ALL)
	add_subdirectory(spd)
	set(START_PROJECT FFX_SPD PARENT_SCOPE)
endif()

if (FFX_CACAO OR FFX_ALL)
	add_subdirectory(cacao)
	set(START_PROJECT FFX_CACAO PARENT_SCOPE)
endif()

if (FFX_LPM OR FFX_ALL)
	add_subdirectory(lpm)
	set(START_PROJECT FFX_LPM PARENT_SCOPE)
endif()

if (FFX_BLUR OR FFX_ALL)
	add_subdirectory(blur)
	set(START_PROJECT FFX_BLUR PARENT_SCOPE)
endif()

if (FFX_PARALLEL_SORT OR FFX_ALL)
	add_subdirectory(parallelsort)
	set(START_PROJECT FFX_PARALLEL_SORT PARENT_SCOPE)
endif()

if (FFX_VRS OR FFX_ALL)
	add_subdirectory(vrs)
	set(START_PROJECT FFX_VRS PARENT_SCOPE)
endif()

if (FFX_CAS OR FFX_ALL)
	add_subdirectory(cas)
	set(START_PROJECT FFX_CAS PARENT_SCOPE)
endif()

if (FFX_SSSR OR FFX_ALL)
	add_subdirectory(sssr)
	set(START_PROJECT FFX_SSSR PARENT_SCOPE)
endif()

if (FFX_DOF OR FFX_ALL)
	add_subdirectory(dof)
	set(START_PROJECT FFX_DOF PARENT_SCOPE)
endif()

if (FFX_LENS OR FFX_ALL)
	add_subdirectory(lens)
	set(START_PROJECT FFX_LENS PARENT_SCOPE)
endif()

if (FFX_HYBRIDSHADOWS OR FFX_ALL)
	add_subdirectory(hybridshadows)
	set(START_PROJECT FFX_HYBRIDSHADOWS PARENT_SCOPE)
endif()

if (FFX_HYBRIDREFLECTIONS OR FFX_ALL)
	add_subdirectory(hybridreflections)
	set(START_PROJECT FFX_HYBRIDREFLECTIONS PARENT_SCOPE)
endif()

if (FFX_BRIXELIZER_GI OR FFX_ALL)
	add_subdirectory(brixelizergi)
	set(START_PROJECT FFX_BRIXELIZER_GI PARENT_SCOPE)
endif()

# If we are building everything, default FFX_API_FSR as the startup project
if (FFX_ALL)
    set(START_PROJECT FFX_API_FSR PARENT_SCOPE)
endif()
