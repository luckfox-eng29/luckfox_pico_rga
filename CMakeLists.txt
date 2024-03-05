cmake_minimum_required(VERSION 3.5)

set(SDK_PATH $ENV{LUCKFOX_SDK_PATH})
if(NOT SDK_PATH)
    message(WARNING "Please Set Luckfox-pico SDK Path. Such as:export LUCKFOX_SDK_PATH=/home/user/luckfox-pico")
    return()
endif()

set(CMAKE_C_COMPILER "${SDK_PATH}/tools/linux/toolchain/arm-rockchip830-linux-uclibcgnueabihf/bin/arm-rockchip830-linux-uclibcgnueabihf-gcc"
)
set(CMAKE_CXX_COMPILER "${SDK_PATH}/tools/linux/toolchain/arm-rockchip830-linux-uclibcgnueabihf/bin/arm-rockchip830-linux-uclibcgnueabihf-g++"
)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wl,--allow-shlib-undefined -ldl")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wl,--allow-shlib-undefined -ldl")

set(RGA_LIB ${CMAKE_SOURCE_DIR}/lib/librga.so)

project(luckfox_rga_demo)


include(${CMAKE_SOURCE_DIR}/utils/CMakeLists.txt)
include_directories(${CMAKE_SOURCE_DIR}/include)


add_executable(${PROJECT_NAME}
    ${CMAKE_SOURCE_DIR}/src/luckfox_rga_demo.cpp
)

target_link_libraries(${PROJECT_NAME}
    utils_obj
    ${RGA_LIB}
)
set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/${PROJECT_NAME})
install(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)
file(GLOB PIC_FILES "${CMAKE_SOURCE_DIR}/pic/*.bin")
install(FILES ${PIC_FILES} DESTINATION ${CMAKE_INSTALL_PREFIX}/pic)