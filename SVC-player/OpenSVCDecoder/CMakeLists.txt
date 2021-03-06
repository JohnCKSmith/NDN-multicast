# CMake projet of OpenSVCDecoder
cmake_minimum_required (VERSION 2.6)
project (OpenSVCDecoder)

find_package(SDL REQUIRED)

# Add libraries
add_subdirectory(AVC/h264_baseline_decoder/lib_baseline)
add_subdirectory(AVC/h264_main_decoder/lib_main)
add_subdirectory(CommonFiles/src)
add_subdirectory(SVC/lib_svc)
add_subdirectory(SVC/libview)

# Include directories
include_directories(AVC/h264_baseline_decoder/lib_baseline AVC/h264_main_decoder/lib_main CommonFiles/src SVC/lib_svc SVC/libview/include)

 # Library
add_library(OpenSVCDecoder SHARED SVC/build/PC.c)

target_link_libraries(OpenSVCDecoder ${SDL_LIBRARY} SVC_baseline AVC_main AVC_baseline DisplaySDL OpenSVCDec)

set_property(TARGET SVC_baseline PROPERTY POSITION_INDEPENDENT_CODE ON)
set_property(TARGET AVC_baseline PROPERTY POSITION_INDEPENDENT_CODE ON)
set_property(TARGET AVC_main PROPERTY POSITION_INDEPENDENT_CODE ON)

INSTALL(TARGETS OpenSVCDecoder
LIBRARY DESTINATION /usr/lib
PERMISSIONS
OWNER_READ OWNER_WRITE OWNER_EXECUTE
GROUP_READ GROUP_EXECUTE
WORLD_READ WORLD_EXECUTE
)

