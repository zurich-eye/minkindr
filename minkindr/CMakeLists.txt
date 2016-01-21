cmake_minimum_required(VERSION 2.8.3)
project(minkindr)

find_package(catkin_simple REQUIRED)
catkin_simple()

find_package (Threads)

# add_definitions(-DGTEST_USE_OWN_TR1_TUPLE=0)
catkin_add_gtest(${PROJECT_NAME}_tests 
  test/test-main.cc
  test/test-rotation.cc
  test/test-transformation.cc
)

set(INC_DIR ./include/kindr/minimal)
set(PUBLIC_HEADERS
  ${INC_DIR}/angle-axis.h
  ${INC_DIR}/common.h
  ${INC_DIR}/position.h
  ${INC_DIR}/quat-transformation.h
  ${INC_DIR}/rotation-quaternion.h
)

set(IMPL_HEADERS
  ${INC_DIR}/implementation/angle-axis-inl.h
  ${INC_DIR}/implementation/quat-transformation-inl.h
  ${INC_DIR}/implementation/rotation-quaternion-inl.h
)

## INSTALLATION
INSTALL(
  FILES ${PUBLIC_HEADERS}
  DESTINATION ${INC_DIR}
  )

INSTALL(
  FILES ${IMPL_HEADERS}
  DESTINATION ${INC_DIR}/implementation
  )

## TESTS
target_link_libraries(${PROJECT_NAME}_tests ${catkin_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})

# Add all files to show up in QtCreator.
add_custom_target(${PROJECT_NAME} SOURCES ${PUBLIC_HEADERS})

cs_install()
cs_export()

