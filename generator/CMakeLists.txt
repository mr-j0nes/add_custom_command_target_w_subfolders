cmake_minimum_required(VERSION 2.4)

# Directory where the generated code is created
set(OUT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/out_gen)

# Name of our generated code. Also make the variable to be seen by our parent CMakeLists.txt
set(OUTPUT_SOURCE ${OUT_DIR}/output.cpp)
set(OUTPUT_SOURCE ${OUTPUT_SOURCE} PARENT_SCOPE)

# Generate our code. This is called because the executable has as dependency
# the variable GENERATOR_PARSER. And in turn that variable has as dependency
# the name of our generated code
ADD_CUSTOM_COMMAND(
    OUTPUT ${OUTPUT_SOURCE}
    COMMAND bash generator.sh ${CMAKE_CURRENT_SOURCE_DIR}/${INPUT_TEMPLATE} ${OUTPUT_SOURCE}
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/${INPUT_TEMPLATE}
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    )

# Link dependency with our generated code
ADD_CUSTOM_TARGET(GENERATOR_PARSER ALL
    DEPENDS ${OUTPUT_SOURCE}
)
