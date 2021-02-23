cmake_minimum_required (VERSION 3.12)

if(NOT SOS_SDK_PATH)
	set(SOS_SDK_PATH $ENV{SOS_SDK_PATH})
endif()

set(CMAKE_MODULE_PATH ${SOS_SDK_PATH}/cmake)
set(CMAKE_TOOLCHAIN_FILE ${SOS_SDK_PATH}/cmake/sos-toolchain.cmake)
include(sos-sdk)

project(SdkAPI)

set(API_IS_SDK TRUE CACHE INTERNAL "Build SDK projects")
option(IS_PULL "Pull SDK projects" OFF)

set(BASE_DIRECTORY ${CMAKE_SOURCE_DIR}/..)
message(STATUS "Base directory ${BASE_DIRECTORY}")

function(clone_or_pull NAME REPOSITORY BRANCH)
	message(STATUS "Checking existence of ${BASE_DIRECTORY}/${NAME}")
	if(NOT EXISTS ${BASE_DIRECTORY}/${NAME})
		message(STATUS "Need to clone manually for the first call to cmake")
		execute_process(
			COMMAND git clone --branch ${BRANCH} ${REPOSITORY}
			WORKING_DIRECTORY ${BASE_DIRECTORY}
			)
	else()
		if(IS_PULL)
			message(STATUS "Using git pull for ${BASE_DIRECTORY}/${NAME}")
			execute_process(
				COMMAND git pull
				WORKING_DIRECTORY ${BASE_DIRECTORY}/${NAME}
				)
		endif()
	endif()
endfunction()


macro(sdk_add_subdirectory NAME BRANCH)
	clone_or_pull(${NAME} https://github.com/StratifyLabs/${NAME}.git ${BRANCH})
	add_subdirectory(${BASE_DIRECTORY}/${NAME} ${NAME})
endmacro()

set(STRATIFYOS_LWIP_PATH
	${CMAKE_CURRENT_SOURCE_DIR}/../InetAPI/lwip/include
	${CMAKE_CURRENT_SOURCE_DIR}/../InetAPI/lwip/lwip-2.1.2/src/include
	CACHE INTERNAL "LWIP INCLUDE PATHS")

include(CTest)

clone_or_pull(API https://github.com/StratifyLabs/API.git main)
add_subdirectory(${BASE_DIRECTORY}/API API)
include(${BASE_DIRECTORY}/API/libraries/API.cmake)

sdk_add_subdirectory(StratifyOS main)

sdk_add_subdirectory(InetAPI main)
sdk_add_subdirectory(CryptoAPI main)
sdk_add_subdirectory(JsonAPI main)
sdk_add_subdirectory(DspAPI main)
sdk_add_subdirectory(AudioAPI main)





