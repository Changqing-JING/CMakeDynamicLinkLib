project(lib1)

if(MSVC)
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
    set(BUILD_SHARED_LIBS TRUE)
endif()

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR} libSource)

add_library(${PROJECT_NAME} SHARED ${libSource})

target_include_directories(${PROJECT_NAME} PUBLIC
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
)

file(GLOB headerFiles include/*.h)

set_target_properties(${PROJECT_NAME} PROPERTIES PUBLIC_HEADER "${headerFiles}")

INSTALL(TARGETS ${PROJECT_NAME} 
        EXPORT ${PROJECT_NAME}
        LIBRARY DESTINATION lib
)

INSTALL (
    DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    DESTINATION include
    FILES_MATCHING PATTERN "*.h"
)

configure_file(./cmake/lib1Config.cmake ${PROJECT_BINARY_DIR}/lib1Config.cmake @ONLY)
install(EXPORT ${PROJECT_NAME} DESTINATION lib/cmake/${PROJECT_NAME})
install(FILES ${PROJECT_BINARY_DIR}/lib1Config.cmake DESTINATION lib/cmake/${PROJECT_NAME})