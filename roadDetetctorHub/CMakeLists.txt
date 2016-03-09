CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

SET(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/external/cmake-modules")
SET(CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING "Only do Release and Debug" FORCE )
MARK_AS_ADVANCED(CMAKE_CONFIGURATION_TYPES)

OPTION(DISABLE_CXX11_ABI "Disable GLIBCXX11 ABI." ON)
IF(DISABLE_CXX11_ABI)
   add_definitions("-D_GLIBCXX_USE_CXX11_ABI=0") # quick hack for new C++ ABI
ENDIF(DISABLE_CXX11_ABI)

PROJECT(libroadfollower)      #must be after setting cmake_configuration_types

#defines the core sources of rufus-roadrunner
SET(RoadFollower_CORE_SRC ${CMAKE_HOME_DIRECTORY}/src)
    
#defines the include of rufus-roadrunner
SET(RoadFollower_INCLUDE_DIR ${CMAKE_HOME_DIRECTORY}/include)

#defines where static libraries are stored
SET(LIBRARY_OUTPUT_PATH ${CMAKE_HOME_DIRECTORY}/lib)
   
#defines where the executables are stored
SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_HOME_DIRECTORY}/bin)
    
#defines where dynamic libraries (plugins) are stored
SET (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_HOME_DIRECTORY}/bin)

# search for cpp unit testing library
OPTION(USE_GTEST "Enable google test framework." ON)
IF(USE_GTEST)
    FIND_PACKAGE(GTest)
    IF (GTEST_FOUND)
      MESSAGE(STATUS "SUCCESSFUL: GTest found")
    ELSE (GTEST_FOUND)
      MESSAGE(STATUS "WARNING: GTest not found")
    ENDIF (GTEST_FOUND)
    
    INCLUDE(UseCodeCoverage) # for codecoverage tools with gcc (optional)
    # Note specyfy DEBUG as build target as debug symbols are needed.
    # Also spefify -coverage -lgcov for the linker
         
ENDIF(USE_GTEST)

#each generates one library or application	
ADD_SUBDIRECTORY(src)     
ADD_SUBDIRECTORY(examples)
###### NEW CODE
FIND_PACKAGE(GTest)
#ADD_SUBDIRECTORY(tests)
######

IF (GTEST_FOUND) 
    ADD_SUBDIRECTORY(tests)
ENDIF(GTEST_FOUND)
