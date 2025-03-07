cmake_minimum_required(VERSION 3.8)
project(via_description)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

install(
  DIRECTORY urdf meshes
  DESTINATION share/${PROJECT_NAME}/
)

link_directories(
  ${GAZEBO_LIBRARY_DIRS}
)

include_directories(
  ${GAZEBO_INCLUDE_DIRS}
)

set(GAZEBO_MODEL_PATH $ENV{HOME}/.gazebo/models/${PROJECT_NAME})

add_custom_target(COMMAND cmake -E make_directory ${GAZEBO_MODEL_PATH})

install(DIRECTORY
  meshes
  DESTINATION ${GAZEBO_MODEL_PATH}
)

ament_package()
