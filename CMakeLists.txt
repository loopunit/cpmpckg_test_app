cmake_minimum_required( VERSION 3.12 )

project(test_app
	VERSION 1.7.8)

include(cmake/CPM.cmake)

####

CPMAddPackage(
  NAME cpmpckg
  GITHUB_REPOSITORY loopunit/cpmpckg
  GIT_TAG 5afe7abc5d22b6ae2504a91bc857b159963f2a88)

CPMAddBaseModule(glslang)
CPMAddBaseModule(basis_universal)
CPMAddBaseModule(glfw)
CPMAddBaseModule(framegraph)
CPMAddBaseModule(imgui)

####

CPMAddPackage(
  NAME imgui_app_fw
  GITHUB_REPOSITORY loopunit/imgui_app_fw.cpmpckg
  GIT_TAG 10d8b8a189e383f33916bd4c557ea6ca27ca6667
  DOWNLOAD_ONLY true)

CPMAddModule(imgui_app_fw)

####

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

