cmake_minimum_required( VERSION 3.12 )

project(test_app
	VERSION 1.7.8)

include(cmake/CPM.cmake)

####

CPMAddPackage(
  NAME cpmpckg_t0
  GITHUB_REPOSITORY loopunit/cpmpckg_t0
  GIT_TAG 0a13162fd171b35ffe3e96b408f06c64cb55a265)

####

CPMAddT0Module(imgui_app_fw)

#####

file(GLOB example_sources 
	${CMAKE_CURRENT_LIST_DIR}/src/main.cpp)

add_executable(test_app
	${example_sources})

set_target_properties(test_app PROPERTIES CXX_STANDARD 17)

target_include_directories(test_app 
	PRIVATE 
		${imgui_SOURCE_DIR}/src)

target_link_libraries(test_app
	PUBLIC
		cpm_runtime::imgui_app_fw)
