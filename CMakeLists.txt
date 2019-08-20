cmake_minimum_required(VERSION 2.4)

SET (INPUT_TEMPLATE "input.tmpl")

PROJECT (test C CXX)

# Here we generate the output. The variable OUTPUT_SOURCE is set. This should
# be done before defining the executaable
ADD_SUBDIRECTORY( generator )

# ADD_CUSTOM_COMMAND marks files as GENERATED automatically, but only in same
# scope (that is done in generator/CMakeLists.txt) once the cmake process comes
# back to this scope that flag disappears, so we need to do it explicitely
# again, otherwise we'll get a "Cannot find source file" error
set_source_files_properties(
    ${OUTPUT_SOURCE}
    PROPERTIES GENERATED TRUE )

# Define our executable and set what source files to use (our generated one)
ADD_EXECUTABLE (test ${OUTPUT_SOURCE})

# Dependecies has to be set after defined executale
ADD_DEPENDENCIES(test GENERATOR_PARSER)
