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
install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin
                                LIBRARY DESTINATION lib
                                ARCHIVE DESTINATION lib
        )
                                
install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/../include/EFStream.hpp
              ${CMAKE_CURRENT_SOURCE_DIR}/../include/MatlabIO.hpp
              ${CMAKE_CURRENT_SOURCE_DIR}/../include/MatlabIOContainer.hpp
              ${CMAKE_CURRENT_SOURCE_DIR}/../include/typetraits.hpp
        DESTINATION include
        )

