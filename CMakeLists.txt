cmake_minimum_required(VERSION 3.2.2)
project(guislice C CXX)
set(EXECUTABLE_BUILD_TYPE Release)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

option(USE_SDL1_DRV "Use SDL1 driver" ON)

find_package(SDL REQUIRED)
find_package(SDL_ttf REQUIRED)

add_compile_options(-Wall -Wextra)

add_library(guislice external/guislice/src/GUIslice.c
            external/guislice/src/GUIslice_ex.c
            external/guislice/src/GUIslice_drv_sdl.c)
target_include_directories(guislice PUBLIC "external/guislice/src/")

if (USE_SDL1_DRV)
    target_link_libraries(guislice PUBLIC ${SDL_LIBRARY})
    target_link_libraries(guislice PUBLIC ${SDL_TTF_LIBRARIES})
    target_include_directories(guislice PUBLIC ${SDL_INCLUDE_DIR})
    target_include_directories(guislice PUBLIC ${SDL_TTF_INCLUDE_DIRS})
    target_include_directories(guislice PUBLIC -lts)
ENDIF()
