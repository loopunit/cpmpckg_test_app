cmake_minimum_required( VERSION 3.12 )

project(test_app
	VERSION 1.7.8)

include(cmake/CPM.cmake)

####

CPMAddPackage(
  NAME cpmpckg
  GITHUB_REPOSITORY loopunit/cpmpckg
  GIT_TAG 1689da7f9c654e28f2206f4b3a9458dd8b84f394
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
