# build the project
set(BUILD_EXECUTABLE False)
if(BUILD_EXECUTABLE)
    set(SRC_FILES MatlabIO.cpp main.cpp)
    add_executable(${PROJECT_NAME} ${SRC_FILES})
else()
    set(SRC_FILES MatlabIO.cpp)
    add_library(${PROJECT_NAME} ${SRC_FILES})
endif()

#link
target_link_libraries(${PROJECT_NAME}   ${Boost_LIBRARIES} 
                                        ${OpenCV_LIBS} 
                                        ${ZLIB_LIBRARIES}
)

# install
install(TARGETS ${PROJECT_NAME} 
        EXPORT ${PROJECT_NAME}-targets
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        )
                                
install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/../include/EFStream.hpp
              ${CMAKE_CURRENT_SOURCE_DIR}/../include/MatlabIO.hpp
              ${CMAKE_CURRENT_SOURCE_DIR}/../include/MatlabIOContainer.hpp
              ${CMAKE_CURRENT_SOURCE_DIR}/../include/typetraits.hpp
        DESTINATION include
        )
        
set(CVMATIO_VERSION 0.1)
include(CMakePackageConfigHelpers)

set(INSTALL_INCLUDE_DIR include)
configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/../cmake/package-config.cmakein ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
                              INSTALL_DESTINATION CMake
                              PATH_VARS INSTALL_INCLUDE_DIR
                              )
       
write_basic_package_version_file( ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake VERSION ${CVMATIO_VERSION} COMPATIBILITY SameMajorVersion )

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
        DESTINATION CMake )


install(EXPORT ${PROJECT_NAME}-targets DESTINATION CMake)

