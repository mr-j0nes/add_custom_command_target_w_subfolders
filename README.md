add_custom_command add_custom_target with sub-folders full example
==================================================================

This provides a full example on how to use cmake's add_custom_command and add_custom_target with different CMakeLists.txt in diferent folders.

**Usage**
- clone the repository
- cd add_custom_command_target_w_subfolders
- mkdir build; cd build
- cmake ..
- make (Here you see the comment "Generating ../../generator/out_gen/output.cpp"
- rm test
- make (Here you don't see the comment anymore)

**Way it works**
- Within the folder "generator" the corresponding CMakeLists.txt is called by the main one
- generate.sh takes the template "input.tmpl" file and generates the "output.cpp" within the "out_gen" folder
- Whenever "input.tmpl" is modified or "output.cpp" does not exist, the generte.sh command is called.
- A binary called "test" is created from "output.cpp"

**Info**
- The generate.sh script just copies input to output file.
- "input.tmpl" already has the source code that will go into "output.cpp"
