cmake_minimum_required(VERSION 3.0)

project(Test)

enable_language(NONE)

include(CTest)

find_package(PythonInterp REQUIRED)

#-----------------------------------------------------------------------------
add_test(
  NAME ExpectedPass
  COMMAND ${PYTHON_EXECUTABLE} -c "print('hello')"
  )

#-----------------------------------------------------------------------------
add_test(
  NAME ExpectedFail
  COMMAND ${PYTHON_EXECUTABLE} -c "print('hello');raise Exception('fail')"
  )

#-----------------------------------------------------------------------------
add_test(
  NAME RegexCheckExpectedPass
  COMMAND ${PYTHON_EXECUTABLE} -c "print('hello')"
  )
set_tests_properties(RegexCheckExpectedPass PROPERTIES
  PASS_REGULAR_EXPRESSION "hello"
  )

#-----------------------------------------------------------------------------
add_test(
  NAME RegexCheckExpectedFail
  COMMAND ${PYTHON_EXECUTABLE} -c "print('hello');raise Exception('fail')"
  )
set_tests_properties(RegexCheckExpectedFail PROPERTIES
  PASS_REGULAR_EXPRESSION "hello"
  )

