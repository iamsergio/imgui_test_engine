cmake_minimum_required(VERSION 3.10)

project(MyProject VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

find_package(SDL2 REQUIRED)

set(imgui_SOURCE_DIR ../../imgui)

set(SRCS
    app_minimal_main.cpp
    app_minimal_tests.cpp

    # imgui_test_engine
    ../shared/imgui_app.cpp
    ../imgui_test_engine/imgui_capture_tool.cpp
    ../imgui_test_engine/imgui_te_coroutine.cpp
    ../imgui_test_engine/imgui_te_exporters.cpp
    ../imgui_test_engine/imgui_te_ui.cpp
    ../imgui_test_engine/imgui_te_context.cpp
    ../imgui_test_engine/imgui_te_engine.cpp
    ../imgui_test_engine/imgui_te_perftool.cpp
    ../imgui_test_engine/imgui_te_utils.cpp

    # imgui
    ${imgui_SOURCE_DIR}/imgui_demo.cpp
    ${imgui_SOURCE_DIR}/imgui_draw.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_sdl2.cpp
    ${imgui_SOURCE_DIR}/imgui_tables.cpp
    ${imgui_SOURCE_DIR}/imgui_widgets.cpp
    ${imgui_SOURCE_DIR}/imgui.cpp
    ${imgui_SOURCE_DIR}/misc/cpp/imgui_stdlib.cpp
)

add_executable(example ${SRCS})

target_compile_definitions(example PRIVATE
    IMGUI_ENABLE_TEST_ENGINE
    IMGUI_TEST_ENGINE_ENABLE_COROUTINE_STDTHREAD_IMPL=1
)

target_include_directories(example PRIVATE
    ".."
    ${SDL2_INCLUDE_DIRS}
    ${imgui_SOURCE_DIR}
    ${imgui_SOURCE_DIR}/backends
)

target_link_libraries(example ${SDL2_LIBRARIES})
