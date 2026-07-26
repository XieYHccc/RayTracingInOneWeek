# ------------------------------------------------------------------
# 公共框架：framework/ 下的所有 .cpp 打包成 framework 库
# 新增 .h / .cpp（含子目录）后直接 build 即可，无需改动本文件
# ------------------------------------------------------------------
file(GLOB_RECURSE FRAMEWORK_SOURCES CONFIGURE_DEPENDS
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
)

if(FRAMEWORK_SOURCES)
    add_library(framework STATIC ${FRAMEWORK_SOURCES})
    set(FRAMEWORK_SCOPE PUBLIC)
else()
    # 还没有 .cpp 时退化成 header-only 库，保证 CMake 不报错
    add_library(framework INTERFACE)
    set(FRAMEWORK_SCOPE INTERFACE)
endif()

# 章节代码用 #include "vec3.h" 引用框架头文件
target_include_directories(framework ${FRAMEWORK_SCOPE}
    ${CMAKE_CURRENT_SOURCE_DIR}
)
