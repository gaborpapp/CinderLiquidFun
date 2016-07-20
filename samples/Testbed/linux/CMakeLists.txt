cmake_minimum_required( VERSION 3.0 FATAL_ERROR )
set( CMAKE_VERBOSE_MAKEFILE on )

project( Testbed )

get_filename_component( SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../src" ABSOLUTE )
get_filename_component( INC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../src" ABSOLUTE )

get_filename_component( CINDER_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../../../../.." ABSOLUTE )

include( "${CINDER_PATH}/proj/cmake/modules/cinderMakeApp.cmake" )

set( TESTBED_SRCS
	${SRC_DIR}/Tests/TestEntries.cpp
	${SRC_DIR}/Framework/Arrow.cpp
	${SRC_DIR}/Framework/FullscreenUI.cpp
	${SRC_DIR}/Framework/Main.cpp
	${SRC_DIR}/Framework/ParticleParameter.cpp
	${SRC_DIR}/Framework/Render.cpp
	${SRC_DIR}/Framework/Test.cpp
)

get_filename_component( BOX2D_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../.." ABSOLUTE)
get_filename_component( BOX2D_INC_DIR "${BOX2D_DIR}/include" ABSOLUTE )

file( GLOB_RECURSE BOX2D_SRCS "${BOX2D_DIR}/src/Box2D/*.cpp" )

ci_make_app(
	APP_NAME "Testbed"
	INCLUDES ${INC_DIR} ${BOX2D_INC_DIR}
	SOURCES ${TESTBED_SRCS} ${BOX2D_SRCS}
	CINDER_PATH ${CINDER_PATH}
)
