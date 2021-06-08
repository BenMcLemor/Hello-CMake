# the 3 first commands are the main commands to excute a cmake file
cmake_minimum_required (VERSION "3.20.3")

project("HelloWorld")

# the 1 parameter of the executable is its name. The second is the source code that is required to build the executable
add_executable("${PROJECT_NAME}" "Main.cpp")

# "${PROJECT_NAME}" is the project unterscore name variable. The value of this variable is set equal to "HelloWorld". but to get that value we need to dereference in cmake with dollar sign

# the next line Specify rules to run at install time. DESTINATION Specify the directory on disk to which a file will be installed.
#The TARGETS form specifies rules for installing targets from a project. There are five kinds of target files that may be installed: ARCHIVE, LIBRARY, RUNTIME, FRAMEWORK, and BUNDLE.
#Executables are treated as RUNTIME targets, except that those marked with the MACOSX_BUNDLE property are treated as BUNDLE targets on OS X.
install(TARGETS "${PROJECT_NAME}" DESTINATION bin) #${CMAKE_INSTALL_PREFIX}/bin 

# in the next line we are installing our main.cpp. We are installing our main.cpp in source folder. src is relative to the cmake install prefix
install(FILES "Main.cpp" DESTINATION src) #${CMAKE_INSTALL_PREFIX}/src

# to use CTest in a project we have to include the CTest module (following line): CTest Configure a project for testing with CTest/CDash
include(CTest)

# add_Test: the 1 parameter is the name of the test. The 2 parameter is the executable we want to run the test on. In our case the CMAKE_CURRENT_BINARY_DIR point to the buid directory.
# Now that we are in the build directory we need to specify the executable we want to run in. In this case that's HelloWorld. And we additonally we use the projet name variable PROJECT_NAME   
add_test("test1" "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}")

# the 3 optional parameter is for checking in the main function if there is a parameter. It does not matter what parameter there is, but it is checked if there is a parameter. (see main line 5 (if (argc > 1)))
## add_test("test2" "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}" "someparameter")