cmake_minimum_required(VERSION 3.17...3.31)
project(testrepo NONE)

enable_testing()

set(CTEST_PARALLEL_LEVEL "PARALLEL_LEVEL 5")

configure_file(
  "CTestScript.cmake.in" "${CMAKE_BINARY_DIR}/CTestScript.cmake" @ONLY
)

foreach(test_num RANGE 20)
  add_test(NAME test_${test_num} COMMAND sleep 1)
endforeach()

add_test(NAME long:five COMMAND sleep 5)
add_test(NAME long:ten COMMAND sleep 10)

set_tests_properties(long:five PROPERTIES COST 5.0)
set_tests_properties(long:ten PROPERTIES COST 10.0)
