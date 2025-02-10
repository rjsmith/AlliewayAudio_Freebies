cmake_minimum_required(VERSION 3.24)

if(NOT "${METAMODULE_SDK_DIR}" STREQUAL "")
    #set(METAMODULE_SDK_DIR "$ENV{METAMODULE_SDK_DIR}")
    message("METAMODULE_SDK_DIR set by CMake variable ${METAMODULE_SDK_DIR}")
elseif (DEFINED ENV{METAMODULE_SDK_DIR})
    set(METAMODULE_SDK_DIR "$ENV{METAMODULE_SDK_DIR}")
    message("METAMODULE_SDK_DIR set by environment variable ${METAMODULE_SDK_DIR}")
else()
    set(METAMODULE_SDK_DIR "${CMAKE_CURRENT_LIST_DIR}/../../Projects/metamodule-plugin-sdk")
    message("METAMODULE_SDK_DIR set to default: ${METAMODULE_SDK_DIR}")
endif()
include(${METAMODULE_SDK_DIR}/plugin.cmake)

########################################################################################


project(AlliewayAudio_Freebies VERSION 2.0.8 DESCRIPTION "AlliewayAudio_Freebies for 4MS MetaModule" LANGUAGES C CXX ASM)

add_library(AlliewayAudio_Freebies STATIC)

# Add sources from the Rack source repo
set(SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/../AlliewayAudio_Freebies)

target_sources(AlliewayAudio_Freebies PRIVATE
    ${SOURCE_DIR}/src/plugin.cpp                    # Note: this file contains init(rack::Plugin*)
    ${SOURCE_DIR}/src/chilly_cheese.cpp
)

# Add includes and compile options for source repo
target_include_directories(AlliewayAudio_Freebies PRIVATE ${SOURCE_DIR}/src)

# Call this to link and create the plugin file
create_plugin(
    SOURCE_LIB      AlliewayAudio_Freebies                            # The cmake target name (defined in add_target)
    PLUGIN_NAME     AlliewayAudio_Freebies                            # This must match the brand "slug" used in VCV Rack
    PLUGIN_JSON     ${SOURCE_DIR}/plugin.json                         # Path to the plugin.json file used by VCV Rack
    SOURCE_ASSETS   ${CMAKE_CURRENT_LIST_DIR}/assets                  # Path to the assets/ dir containing the PNGs
    DESTINATION     ${CMAKE_CURRENT_LIST_DIR}/../metamodule-plugins   # Path to where you want the plugin file output
)