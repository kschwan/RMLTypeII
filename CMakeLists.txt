cmake_minimum_required(VERSION 3.1)
project(RMLTypeII VERSION 1.2.7)

option(BUILD_EXAMPLES "Build example applications" OFF)

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
target_include_directories(ReflexxesTypeII PUBLIC include/RMLTypeII)
target_compile_options(ReflexxesTypeII PRIVATE -Wall)
set_target_properties(ReflexxesTypeII PROPERTIES SOVERSION ${PROJECT_VERSION})

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
