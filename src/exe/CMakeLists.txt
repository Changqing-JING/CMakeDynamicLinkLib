project(exe1)

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR} exeSource)

add_executable(${PROJECT_NAME} ${exeSource})

target_link_libraries(${PROJECT_NAME} lib1)