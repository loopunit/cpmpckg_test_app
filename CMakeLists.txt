cmake_minimum_required( VERSION 3.12 )

project(test_app
	VERSION 1.7.8)

include(cmake/CPM.cmake)

####

CPMAddPackage(
  NAME cpmpckg
  GITHUB_REPOSITORY loopunit/cpmpckg
  GIT_TAG 1b6245fc7aa5041ca185a64b3385fb998a996c3f
  DOWNLOAD_ONLY true)

include(${cpmpckg_SOURCE_DIR}/cmake/add_cpm_module.cmake)

####

CPMAddBaseModule(imgui_app)

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
		cpm_runtime::imgui_app)
