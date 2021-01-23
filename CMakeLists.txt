cmake_minimum_required( VERSION 3.12 )

project(test_app
	VERSION 1.7.8)

include(cmake/CPM.cmake)

####

CPMAddPackage(
  NAME cpmpckg
  GITHUB_REPOSITORY loopunit/cpmpckg
  GIT_TAG 3f9b7a914bd99fce0b539dd96afbca624eb0fde6)

CPMAddBaseModule(glslang)
CPMAddBaseModule(basis_universal)
CPMAddBaseModule(glfw)
CPMAddBaseModule(framegraph)
CPMAddBaseModule(imgui)

####

CPMAddPackage(
  NAME imgui_app_fw
  GITHUB_REPOSITORY loopunit/imgui_app_fw.cpmpckg
  GIT_TAG fc1de32db22a1257373ed9b97d6ca6817d457491
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

