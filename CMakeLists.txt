cmake_minimum_required(VERSION 3.10)

project(lua)

if(WIN32)
        add_definitions( -D_CRT_SECURE_NO_WARNINGS )
endif()

if (MSVC)
        set(CompilerFlags
                CMAKE_CXX_FLAGS
                CMAKE_CXX_FLAGS_DEBUG
                CMAKE_CXX_FLAGS_RELEASE
                CMAKE_C_FLAGS
                CMAKE_C_FLAGS_DEBUG
                CMAKE_C_FLAGS_RELEASE
        )
        foreach(CompilerFlag ${CompilerFlags})
                string(REPLACE "/MD" "/MT" ${CompilerFlag} "${${CompilerFlag}}")
        endforeach()
endif(MSVC)

add_subdirectory(lua)

include_directories(${PROJECT_SOURCE_DIR}/lua)

add_executable (lua lua.c)

set_target_properties(lua PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/bin"
)
target_link_libraries (lua lualib)

add_executable (luac luac.c)
set_target_properties(lua PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${PROJECT_BINARY_DIR}/bin"
)
target_link_libraries (luac lualib)

install(
        TARGETS lua luac
        RUNTIME DESTINATION ${PROJECT_SOURCE_DIR}/dist
)
