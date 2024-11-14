cmake_minimum_required(VERSION 3.10)

project(peak VERSION 1.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# PortAudio
find_package(PkgConfig REQUIRED)
pkg_check_modules(PORTAUDIO REQUIRED portaudio-2.0)

# libsndfile
pkg_check_modules(SNDFILE REQUIRED sndfile)

# FFTW using pkg-config
pkg_check_modules(FFTW REQUIRED fftw3)

# SFML
find_package(SFML 2.5 COMPONENTS graphics audio REQUIRED)

# Executable
add_executable(peak src/main.cpp)

# Include directories
target_include_directories(peak 
    PRIVATE 
    ${PORTAUDIO_INCLUDE_DIRS} 
    ${SNDFILE_INCLUDE_DIRS} 
    ${FFTW_INCLUDE_DIRS} 
    ${SFML_INCLUDE_DIRS}
)

# Link directories
target_link_directories(peak 
    PRIVATE 
    ${PORTAUDIO_LIBRARY_DIRS} 
    ${SNDFILE_LIBRARY_DIRS} 
    ${FFTW_LIBRARY_DIRS} 
    ${SFML_LIBRARY_DIRS}
)

# Link libraries
target_link_libraries(peak 
    PRIVATE 
    ${PORTAUDIO_LIBRARIES} 
    ${SNDFILE_LIBRARIES} 
    ${FFTW_LIBRARIES} 
    sfml-graphics 
    sfml-audio
)
