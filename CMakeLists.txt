cmake_minimum_required(VERSION 3.15)

project(pigpio VERSION 0.71 
			DESCRIPTION "C lib for raspberry PI GPIO"
			LANGUAGES C)

find_package(Threads REQUIRED)
find_library(LIBRT rt) #apparently find package doesnt exists for RT, this is my work around.

# libpigpio.(so|a)
add_library(pigpio pigpio.c command.c custom.cext)
target_include_directories(pigpio PUBLIC pigpio.h)
target_link_libraries(pigpio ${LIBRT} Threads::Threads)

# libpigpiod_if.(so|a)
add_library(pigpiod_if pigpiod_if.c command.c)
target_include_directories(pigpiod_if PUBLIC pigpiod_if.h)
target_link_libraries(pigpiod_if ${LIBRT} Threads::Threads)

# libpigpiod_if2.(so|a)
add_library(pigpiod_if2 pigpiod_if2.c command.c)
target_include_directories(pigpiod_if2 PRIVATE pigpiod_if2.h)
target_link_libraries(pigpiod_if2 ${LIBRT} Threads::Threads)