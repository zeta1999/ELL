#
# cmake file
#

if(${PYTHON_ENABLED})
  set(test_name wrap-test)

  file(GLOB test_src RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.py *.cpp tutorialCMakeLists.txt)

  add_custom_target(${test_name} ALL DEPENDS ${test_src} SOURCES ${test_src})
  add_dependencies(${test_name} wrap _ELL_python)
  set_property(TARGET ${test_name} PROPERTY FOLDER "tests")

  # copy the contents of the test directory to build/interfaces/python
  copy_newer_files(${test_name} test_src)

  # add this test to the cmake suite of tests
  add_test(NAME ${test_name}
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    COMMAND ${PYTHON_EXECUTABLE} test.py)
  set_property(TARGET ${test_name} PROPERTY FOLDER "tests")

endif()  # PYTHON_ENABLED
