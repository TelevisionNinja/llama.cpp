# dependencies

find_package(Threads REQUIRED)

# third-party

if (WHISPER_SDL2)
    # SDL2
    find_package(SDL2 REQUIRED)

    string(STRIP "${SDL2_LIBRARIES}" SDL2_LIBRARIES)

    message(STATUS "SDL2_INCLUDE_DIRS = ${SDL2_INCLUDE_DIRS}")
    message(STATUS "SDL2_LIBRARIES = ${SDL2_LIBRARIES}")
endif()

if (WHISPER_CLBLAST)
    find_package(CLBlast REQUIRED)
endif()

# common

set(TARGET common)

add_library(${TARGET} STATIC
    common-talk.h
    common-talk.cpp
    common-ggml.h
    common-ggml.cpp
    grammar-parser.h
    grammar-parser.cpp
    )

include(DefaultTargetOptions)

target_link_libraries(${TARGET} PRIVATE whisper)

set_target_properties(${TARGET} PROPERTIES POSITION_INDEPENDENT_CODE ON)
set_target_properties(${TARGET} PROPERTIES FOLDER "libs")

if (WHISPER_SDL2)
    # common-sdl

    set(TARGET common-sdl)

    add_library(${TARGET} STATIC
        common-sdl.h
        common-sdl.cpp
        )

    include(DefaultTargetOptions)

    target_include_directories(${TARGET} PUBLIC ${SDL2_INCLUDE_DIRS})
    target_link_libraries(${TARGET} PRIVATE ${SDL2_LIBRARIES})

    set_target_properties(${TARGET} PROPERTIES POSITION_INDEPENDENT_CODE ON)
    set_target_properties(${TARGET} PROPERTIES FOLDER "libs")
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

if (WHISPER_SDL2)
    add_subdirectory(talk)
    set_target_properties(talk PROPERTIES FOLDER "talk")
endif (WHISPER_SDL2)
