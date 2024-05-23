# CMakeList.txt : CMake project for Hello, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("Hello")

# Add source to this project's executable.
add_executable( Hello Hello.cpp )

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET Hello PROPERTY CXX_STANDARD 20)
endif()

# Install command
install( TARGETS Hello CONFIGURATIONS Debug RUNTIME DESTINATION debug )
install( CODE "MESSAGE( \"Installed to 'Debug' Configuration location\" )" )

install( TARGETS Hello CONFIGURATIONS Release RUNTIME DESTINATION release )
install( TARGETS Hello CONFIGURATIONS RelWithDebInfo RUNTIME DESTINATION relwdebug )
install( TARGETS Hello CONFIGURATIONS MinSizeRel RUNTIME DESTINATION minsizerel )

# enable testing functionality
enable_testing()

# Test command
add_test( NAME Hello_Test COMMAND Hello )
