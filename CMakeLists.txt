cmake_minimum_required(VERSION 3.13.4)
project(wyrm VERSION 0.0.1 LANGUAGES C CXX)

# find_package(LLVM REQUIRED CONFIG)

# This is intended to be the canoncial version requirement documentation. All
# other references to this version should key off of this setting, so that it
# doesn't have to be duplicated everywhere for up-to-date documentation.
set(WYRM_LLVM_VERSION_REQ 15.0.6 CACHE STRING "Wyrm required LLVM version.")

#if (NOT LLVM_PACKAGE_VERSION VERSION_EQUAL ${WYRM_LLVM_VERSION_REQ})
#  message(FATAL_ERROR "Wyrm requires LLVM version ${WYRM_LLVM_VERSION_REQ}, but detected version ${LLVM_PACKAGE_VERSION}")
#endif()

#message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
#message(STATUS "Using LLVMConfig.cmake in ${LLVM_DIR}")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED)

if(EXISTS "${CMAKE_SOURCE_DIR}/.git")
  execute_process(
      COMMAND git rev-parse --abbrev-ref HEAD
      WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
      OUTPUT_VARIABLE WYRM_GIT_BRANCH
      OUTPUT_STRIP_TRAILING_WHITESPACE
  )
  execute_process(
      COMMAND git log -1 --format=%h
      WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
      OUTPUT_VARIABLE WYRM_GIT_COMMIT_HASH
      OUTPUT_STRIP_TRAILING_WHITESPACE
  )
else()
  set(WYRM_GIT_BRANCH "not_a_git_checkout")
  set(WYRM_GIT_COMMIT_HASH "na")
endif()

message(STATUS "wyrm v${PROJECT_VERSION}, ${WYRM_GIT_BRANCH}@${WYRM_GIT_COMMIT_HASH}")
configure_file(README.md.in "${PROJECT_SOURCE_DIR}/README.md")

option(WYRM_DOCS "Build documentation using sphinx." ON)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

if (WYRM_DOCS)
  find_program(SPHINX_BUILD sphinx-build REQUIRED)
  if (NOT SPHINX_BUILD)
    message(FATAL_ERROR "Wyrm documentation requires Sphinx.")
  endif()

  file(MAKE_DIRECTORY "${PROJECT_BINARY_DIR}/docs/html")
  file(MAKE_DIRECTORY "${PROJECT_BINARY_DIR}/docs/cache")
  configure_file(docs/conf.py.in "${PROJECT_BINARY_DIR}/docs/conf.py")

  add_custom_target(wyrm_docs ALL
    COMMAND ${SPHINX_BUILD}
      -b html -d "${PROJECT_BINARY_DIR}/docs/cache"
      -j auto
      -c "${PROJECT_BINARY_DIR}/docs/"
      "${PROJECT_SOURCE_DIR}/docs/"
      "${PROJECT_BINARY_DIR}/docs/html"
    VERBATIM
  )
endif()