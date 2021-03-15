cmake_minimum_required( VERSION 3.12 )

project(test_app
	VERSION 1.7.8)

include(cmake/CPM.cmake)

####

if (NOT DEFINED cpmpckg_SOURCE_DIR)
	include(cmake/CPM.cmake)

	# One frustrating part of this project setup is the circular dependency between cpmpckg and this repo.
	# GIT_TAG will always lag cpmpckg @ HEAD when this project is updated there.
	CPMAddPackage(
		NAME cpmpckg
		GITHUB_REPOSITORY loopunit/cpmpckg
		GIT_TAG 1092ae58669c7cd3568a142893348983f4b5f52d
		DOWNLOAD_ONLY true)

	include(${cpmpckg_SOURCE_DIR}/cmake/add_cpm_module.cmake)
else()
	set(CPM_SCRIPTS ${cpmpckg_SOURCE_DIR}/cmake)
	include(${cpmpckg_SOURCE_DIR}/cmake/CPM.cmake)
	include(${cpmpckg_SOURCE_DIR}/cmake/add_cpm_module.cmake)
endif()

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
		cpm_install::imgui_app)
