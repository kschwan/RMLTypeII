cmake_minimum_required(VERSION 3.1)
project(RMLTypeII VERSION 1.2.7)

option(BUILD_EXAMPLES "Build example applications" OFF)

# Use C++14
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 14)

# Library
set(LIB_SOURCES
  src/ReflexxesAPI.cpp
  src/TypeIIRMLCalculatePositionalExtrems.cpp
  src/TypeIIRMLDecisions.cpp
  src/TypeIIRMLDecisionTree1A.cpp
  src/TypeIIRMLDecisionTree1B.cpp
  src/TypeIIRMLDecisionTree1C.cpp
  src/TypeIIRMLDecisionTree2.cpp
  src/TypeIIRMLFallBackStrategy.cpp
  src/TypeIIRMLIsPhaseSynchronizationPossible.cpp
  src/TypeIIRMLPolynomial.cpp
  src/TypeIIRMLPosition.cpp
  src/TypeIIRMLQuicksort.cpp
  src/TypeIIRMLSetupModifiedSelectionVector.cpp
  src/TypeIIRMLStep1.cpp
  src/TypeIIRMLStep1IntermediateProfiles.cpp
  src/TypeIIRMLStep1Profiles.cpp
  src/TypeIIRMLStep2.cpp
  src/TypeIIRMLStep2IntermediateProfiles.cpp
  src/TypeIIRMLStep2PhaseSynchronization.cpp
  src/TypeIIRMLStep2Profiles.cpp
  src/TypeIIRMLStep2WithoutSynchronization.cpp
  src/TypeIIRMLStep3.cpp
  src/TypeIIRMLVelocityCalculatePositionalExtrems.cpp
  src/TypeIIRMLVelocity.cpp
  src/TypeIIRMLVelocityFallBackStrategy.cpp
  src/TypeIIRMLVelocityIsPhaseSynchronizationPossible.cpp
  src/TypeIIRMLVelocityMethods.cpp
  src/TypeIIRMLVelocitySetupPhaseSyncSelectionVector.cpp
)

add_library(ReflexxesTypeII SHARED ${LIB_SOURCES})
target_include_directories(ReflexxesTypeII
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/RMLTypeII>
    $<INSTALL_INTERFACE:include/RMLTypeII>  # <prefix>/include/mylib
)
target_compile_options(ReflexxesTypeII PRIVATE -Wall)
set_target_properties(ReflexxesTypeII PROPERTIES SOVERSION ${PROJECT_VERSION})
add_library(RMLTypeII::ReflexxesTypeII ALIAS ReflexxesTypeII)

# Examples
if(BUILD_EXAMPLES)
  set(EXAMPLE_SOURCES
    examples/01_RMLPositionSampleApplication.cpp
    examples/02_RMLPositionSampleApplication.cpp
    examples/03_RMLPositionSampleApplication.cpp
    examples/04_RMLVelocitySampleApplication.cpp
    examples/05_RMLVelocitySampleApplication.cpp
    examples/06_RMLVelocitySampleApplication.cpp
    examples/07_RMLPositionSampleApplication.cpp
    examples/08_RMLVelocitySampleApplication.cpp
  )

  # Add target for each file
  foreach(FILE_NAME ${EXAMPLE_SOURCES})
    get_filename_component(APP_NAME ${FILE_NAME} NAME_WE)
    add_executable(${APP_NAME} ${FILE_NAME})
    target_link_libraries(${APP_NAME} ReflexxesTypeII)
  endforeach()
endif()

# Install
include(GNUInstallDirs)

set(INSTALL_CMAKE_CONFIG_DIR ${CMAKE_INSTALL_LIBDIR}/cmake/RMLTypeII)

install(TARGETS ReflexxesTypeII
  EXPORT RMLTypeIITargets
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
install(DIRECTORY include/RMLTypeII DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

export(EXPORT RMLTypeIITargets
  NAMESPACE RMLTypeII::
  FILE ${CMAKE_CURRENT_BINARY_DIR}/RMLTypeIITargets.cmake
)

# Write CMake config files
include(CMakePackageConfigHelpers)

write_basic_package_version_file(${CMAKE_CURRENT_BINARY_DIR}/RMLTypeIIConfigVersion.cmake
  COMPATIBILITY SameMajorVersion
)
configure_package_config_file(cmake/RMLTypeIIConfig.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/RMLTypeIIConfig.cmake
  INSTALL_DESTINATION ${INSTALL_CMAKE_CONFIG_DIR}
)

install(FILES
  ${CMAKE_CURRENT_BINARY_DIR}/RMLTypeIIConfig.cmake
  ${CMAKE_CURRENT_BINARY_DIR}/RMLTypeIIConfigVersion.cmake
  DESTINATION ${INSTALL_CMAKE_CONFIG_DIR}
)
install(EXPORT RMLTypeIITargets
  NAMESPACE RMLTypeII::
  DESTINATION ${INSTALL_CMAKE_CONFIG_DIR}
)
