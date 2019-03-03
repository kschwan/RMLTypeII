cmake_minimum_required(VERSION 3.1)
project(RMLTypeII VERSION 1.2.7)

option(BUILD_EXAMPLES "Build example applications" OFF)

# Library
set(LIB_SOURCES
  src/TypeIIRML/ReflexxesAPI.cpp
  src/TypeIIRML/TypeIIRMLCalculatePositionalExtrems.cpp
  src/TypeIIRML/TypeIIRMLDecisions.cpp
  src/TypeIIRML/TypeIIRMLDecisionTree1A.cpp
  src/TypeIIRML/TypeIIRMLDecisionTree1B.cpp
  src/TypeIIRML/TypeIIRMLDecisionTree1C.cpp
  src/TypeIIRML/TypeIIRMLDecisionTree2.cpp
  src/TypeIIRML/TypeIIRMLFallBackStrategy.cpp
  src/TypeIIRML/TypeIIRMLIsPhaseSynchronizationPossible.cpp
  src/TypeIIRML/TypeIIRMLPolynomial.cpp
  src/TypeIIRML/TypeIIRMLPosition.cpp
  src/TypeIIRML/TypeIIRMLQuicksort.cpp
  src/TypeIIRML/TypeIIRMLSetupModifiedSelectionVector.cpp
  src/TypeIIRML/TypeIIRMLStep1.cpp
  src/TypeIIRML/TypeIIRMLStep1IntermediateProfiles.cpp
  src/TypeIIRML/TypeIIRMLStep1Profiles.cpp
  src/TypeIIRML/TypeIIRMLStep2.cpp
  src/TypeIIRML/TypeIIRMLStep2IntermediateProfiles.cpp
  src/TypeIIRML/TypeIIRMLStep2PhaseSynchronization.cpp
  src/TypeIIRML/TypeIIRMLStep2Profiles.cpp
  src/TypeIIRML/TypeIIRMLStep2WithoutSynchronization.cpp
  src/TypeIIRML/TypeIIRMLStep3.cpp
  src/TypeIIRML/TypeIIRMLVelocityCalculatePositionalExtrems.cpp
  src/TypeIIRML/TypeIIRMLVelocity.cpp
  src/TypeIIRML/TypeIIRMLVelocityFallBackStrategy.cpp
  src/TypeIIRML/TypeIIRMLVelocityIsPhaseSynchronizationPossible.cpp
  src/TypeIIRML/TypeIIRMLVelocityMethods.cpp
  src/TypeIIRML/TypeIIRMLVelocitySetupPhaseSyncSelectionVector.cpp
)
add_library(ReflexxesTypeII SHARED ${LIB_SOURCES})
target_include_directories(ReflexxesTypeII PUBLIC include)
target_compile_options(ReflexxesTypeII PRIVATE -Wall)
set_target_properties(ReflexxesTypeII PROPERTIES SOVERSION ${PROJECT_VERSION})

# Examples
if(BUILD_EXAMPLES)
  add_executable(01_RMLPositionSampleApplication src/RMLPositionSampleApplications/01_RMLPositionSampleApplication.cpp)
  add_executable(02_RMLPositionSampleApplication src/RMLPositionSampleApplications/02_RMLPositionSampleApplication.cpp)
  add_executable(03_RMLPositionSampleApplication src/RMLPositionSampleApplications/03_RMLPositionSampleApplication.cpp)
  add_executable(04_RMLVelocitySampleApplication src/RMLVelocitySampleApplications/04_RMLVelocitySampleApplication.cpp)
  add_executable(05_RMLVelocitySampleApplication src/RMLVelocitySampleApplications/05_RMLVelocitySampleApplication.cpp)
  add_executable(06_RMLVelocitySampleApplication src/RMLVelocitySampleApplications/06_RMLVelocitySampleApplication.cpp)
  add_executable(07_RMLPositionSampleApplication src/RMLPositionSampleApplications/07_RMLPositionSampleApplication.cpp)
  add_executable(08_RMLVelocitySampleApplication src/RMLVelocitySampleApplications/08_RMLVelocitySampleApplication.cpp)
  target_link_libraries(01_RMLPositionSampleApplication ReflexxesTypeII)
  target_link_libraries(02_RMLPositionSampleApplication ReflexxesTypeII)
  target_link_libraries(03_RMLPositionSampleApplication ReflexxesTypeII)
  target_link_libraries(04_RMLVelocitySampleApplication ReflexxesTypeII)
  target_link_libraries(05_RMLVelocitySampleApplication ReflexxesTypeII)
  target_link_libraries(06_RMLVelocitySampleApplication ReflexxesTypeII)
  target_link_libraries(07_RMLPositionSampleApplication ReflexxesTypeII)
  target_link_libraries(08_RMLVelocitySampleApplication ReflexxesTypeII)
endif()
