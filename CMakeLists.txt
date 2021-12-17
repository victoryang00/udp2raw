cmake_minimum_required(VERSION 3.7)
project(udp2raw_tunnel)

set(CMAKE_CXX_STANDARD 20)
set(SOURCE_FILES
		lib/aes_faster_c/aes.cpp
		lib/aes_faster_c/wrapper.cpp
		lib/md5.cpp
		common.cpp
		encrypt.cpp
		log.cpp
		main.cpp
		network.cpp
		)

set(CMAKE_CXX_FLAGS "-Wall -Wextra -Wno-unused-variable -Wno-unused-parameter -Wno-missing-field-initializers  -static")
add_executable(udp2raw_cmake ${SOURCE_FILES})
target_link_libraries(udp2raw_cmake rt)
target_link_libraries(udp2raw_cmake pthread)
if (${APPLE})
	target_compile_definitions(udp2raw_cmake PUBLIC UDP2RAW_LINUX=0)
	target_compile_definitions(udp2raw_cmake PUBLIC UDP2RAW_BSD=1)
endif()
