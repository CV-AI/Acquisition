cmake_minimum_required (VERSION 2.6)
set(name spinnaker_camera)
project ( ${name} )



# OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})


# pointgrey camera sdk
set(USE_PTGREY_CAMERA on)
if (USE_PTGREY_CAMERA)
	set(PTGREY_SDK_INCLUDE_DIR "C:/Program Files/Point Grey Research/Spinnaker/include")
	set(PTGREY_SDK_LIBRARY_DEBUG "C:/Program Files/Point Grey Research/Spinnaker/lib64/vs2015/Spinnakerd_v140.lib")
	set(PTGREY_SDK_LIBRARY_RELEASE "C:/Program Files/Point Grey Research/Spinnaker/lib64/vs2015/Spinnaker_v140.lib")
endif()
include_directories(${PTGREY_SDK_INCLUDE_DIR})



set(MY_HEADER_FILES
	# C++ header file
	include/resource.h
	include/stdafx.h
	include/targetver.h
)

set(MY_SOURCE_FILES 
	# C++ source file
	src/main.cpp
	src/stdafx.cpp
)

include_directories(
	${PROJECT_SOURCE_DIR}/include	
)

add_executable(${name}
	${MY_HEADER_FILES}
	${MY_SOURCE_FILES}
)

if (USE_LIB)
	target_link_libraries(${name}
		${OpenCV_LIBS}
		debug ${PTGREY_SDK_LIBRARY_DEBUG}
		optimized ${PTGREY_SDK_LIBRARY_RELEASE}
	)
else()
	target_link_libraries(${name}
		${OpenCV_LIBS}
		debug ${PTGREY_SDK_LIBRARY_DEBUG}
		optimized ${PTGREY_SDK_LIBRARY_RELEASE}
	)
endif(USE_LIB)