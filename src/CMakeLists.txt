# Build steps
#file(GLOB_RECURSE APP_SRC_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.c)
set(APP_SRC_FILES 
    main.cpp
    ml/audiodecoder.cpp
    ml/libavwrapper.cpp
    ml/SDLMovieAudioFactory.cpp
    ml/videoplayer.cpp
    ml/videostate.cpp
    ml/texture.cpp
    dict/youdao.cpp
	)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
#include_directories(${PROJECT_SOURCE_DIR}/ext/cpr/include)
include_directories(${PROJECT_SOURCE_DIR}/src)
include_directories(${PROJECT_SOURCE_DIR}/include)
include_directories(/usr/include/cairo)
add_executable(${APP_NAME} ${APP_SRC_FILES})
add_dependencies(${APP_NAME} nanogui)
add_dependencies(${APP_NAME} aeon_streams)
add_dependencies(${APP_NAME} cpr)
add_dependencies(${APP_NAME} tinyxml2)
add_dependencies(${APP_NAME} gumbo_query_static)
#target_include_directories(${APP_NAME} PUBLIC ../src)
target_link_libraries(${APP_NAME} LINK_PUBLIC nanogui cpr tinyxml2 gumbo_query_static aeon_streams m pthread z cairo X11 Xext x264 x265 glut -lGL GLU SDL2 avformat avdevice avcodec avutil avfilter swscale avresample)
#install(TARGETS ${APP_NAME} RUNTIME DESTINATION bin)
