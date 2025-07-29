cmake_minimum_required(VERSION 3.15)
project(nanobind_colcon)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake")

include(ExternalProject)
externalproject_add(nanobind_src
  GIT_REPOSITORY git@github.com:wjakob/nanobind.git
  GIT_TAG v2.8.0
  CONFIGURE_COMMAND cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX} ../nanobind_src
  BUILD_COMMAND make
  INSTALL_COMMAND make install
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION "include/${PROJECT_NAME}"
  FILES_MATCHING PATTERN "*.h"
)

install(DIRECTORY cmake/
  DESTINATION "share/${PROJECT_NAME}"
  FILES_MATCHING PATTERN "*.cmake"
)
