################################################################################
# File generated by HDevelop Version 18.11
#
# Do not modify!
################################################################################

cmake_minimum_required(VERSION 3.3 FATAL_ERROR)

project(defect CXX)
set(CMAKE_CXX_FLAGS "-fPIC")

set(HALCONROOT /opt/halcon)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

message(thehalconrootpath ${HALCONROOT})

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/defect)
FILE(GLOB DEFECT_LISTS "defect/*.cpp")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/base64)
FILE(GLOB BASE64_LISTS "defect/*.cpp")
message(${DEFECT_LISTS}})
SET(SOURCE ${DEFECT_LISTS}
	   ${BASE64_LISTS}
		)


# ==================================================
#  Halcon
# ==================================================
find_package(Halcon)

set (INC_DIRS ${INC_DIRS} ${HALCON_INC_DIRS})
set (LIBS ${LIBS} ${HALCON_LIBS})
message(**********************)
message(${INC_DIRS})
message(${HALCON_INC_DIRS})
message(${SOURCE}})
message(**********************)
message(**********************)

add_library(${PROJECT_NAME} SHARED ${SOURCE} ${HEADER})
set (INC_DIRS ${INC_DIRS} ${CMAKE_CURRENT_SOURCE_DIR}/source)
target_include_directories(${PROJECT_NAME} PUBLIC ${INC_DIRS})
message(${INC_DIRS})
message(${CMAKE_CURRENT_SOURCE_DIR}/source)

target_link_libraries(${PROJECT_NAME} PUBLIC ${LIBS})
message(${INC_DIRS})

message(*********base64*************)
message(${CMAKE_CURRENT_SOURCE_DIR}/base64)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/base64/base64.h})
target_link_libraries(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/base64/base64.cpp)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)

add_executable(testRun test.cpp )
target_include_directories(testRun PUBLIC ${INC_DIRS})
target_link_libraries(testRun PUBLIC ${LIBS})
target_link_libraries(testRun PUBLIC ${PROJECT_NAME})
set_property(TARGET testRun PROPERTY CXX_STANDARD 11)



