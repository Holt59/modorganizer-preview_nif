cmake_minimum_required(VERSION 3.16)

set(GLI_TEST_ENABLE OFF CACHE BOOL "Build gli unit tests")
add_subdirectory(external/gli)
add_subdirectory(external/nifly)

# those are not used for this plugin
set(BOOST_ROOT "")
set(FMT_ROOT "")
set(PYTHON_ROOT "")
set(CMAKE_INSTALL_PREFIX "")

include(${CMAKE_CURRENT_LIST_DIR}/cmake_common/mo2.cmake)

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/fmt)
add_library(mo2-fmt ALIAS fmt)
add_library(mo2::fmt ALIAS fmt)

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/libbsarch)
target_include_directories(libbsarch PUBLIC ${CMAKE_CURRENT_LIST_DIR}/libbsarch/src)
add_library(mo2-libbsarch ALIAS libbsarch)
add_library(mo2::libbsarch ALIAS libbsarch)

FetchContent_Declare(
  uibase
  URL      https://github.com/ModOrganizer2/modorganizer/releases/download/v2.5.0rc1/Mod.Organizer-2.5.0rc1-uibase.7z
  URL_HASH MD5=0E5829A6A5100B85D0360C9B2B7591ED
)

FetchContent_MakeAvailable(uibase)

add_library(mo2-uibase IMPORTED SHARED)
set_target_properties(mo2-uibase PROPERTIES
	IMPORTED_LOCATION "${uibase_SOURCE_DIR}/uibase.lib"
)
set_target_properties(mo2-uibase PROPERTIES
	IMPORTED_IMPLIB "${uibase_SOURCE_DIR}/uibase.lib"
)
target_include_directories(mo2-uibase INTERFACE
	${uibase_SOURCE_DIR} ${uibase_SOURCE_DIR}/game_features)
add_library(mo2::uibase ALIAS mo2-uibase)

project(preview_nif)

add_subdirectory(src)

target_link_libraries(${PROJECT_NAME} PRIVATE nifly gli)
