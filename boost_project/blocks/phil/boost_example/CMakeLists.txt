# Define block variables
INIT_BIICODE_BLOCK() 

set(Boost_USE_STATIC_LIBS ON)
find_package(Boost REQUIRED COMPONENTS system)
# Actually create targets: EXEcutables, STATIC libraries.
ADD_BIICODE_TARGETS()

if(Boost_FOUND)
	target_include_directories(${BII_BLOCK_TARGET} INTERFACE ${Boost_INCLUDE_DIRS})
	IF(APPLE)
		set(CPP_11_FLAGS "-std=c++11 -stdlib=libc++")
	    target_compile_options(${BII_BLOCK_TARGET} INTERFACE ${CPP_11_FLAGS})
	ELSEIF (WIN32 OR UNIX)
		set(CPP_11_FLAGS "-std=c++11")
		target_compile_options(${BII_BLOCK_TARGET} INTERFACE ${CPP_11_FLAGS})
	ENDIF(APPLE)

	IF (WIN32)
		TARGET_LINK_LIBRARIES(${BII_BLOCK_TARGET} INTERFACE "ws2_32" "wsock32" ${Boost_LIBRARIES})
	ELSEIF(APPLE OR UNIX)
		TARGET_LINK_LIBRARIES(${BII_BLOCK_TARGET} INTERFACE ${Boost_LIBRARIES})
	ENDIF(WIN32)
endif()
