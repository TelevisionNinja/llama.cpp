# dependencies

find_package(Threads REQUIRED)

# third-party

# ...

# examples

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

if (WHISPER_SDL2)
    add_subdirectory(talk)
    set_target_properties(talk PROPERTIES FOLDER "talk")
endif (WHISPER_SDL2)
