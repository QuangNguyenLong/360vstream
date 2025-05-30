cmake_minimum_required(VERSION 3.21)

project(vstreamExamples C)

include(../cmake/folders.cmake)

if(PROJECT_IS_TOP_LEVEL)
  find_package(vstream REQUIRED)
endif()

add_custom_target(run-examples)

function(add_example NAME)
  add_executable("${NAME}" "${NAME}.c")
  target_link_libraries("${NAME}" PRIVATE vstream::vstream)
  target_compile_features("${NAME}" PRIVATE c_std_17)
  add_custom_target("run_${NAME}" COMMAND "${NAME}" VERBATIM)
  add_dependencies("run_${NAME}" "${NAME}")
  add_dependencies(run-examples "run_${NAME}")
endfunction()

add_example(empty_example)
add_example(my_program)

add_folders(Example)
