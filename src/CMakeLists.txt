
# Source Files
#
# If you add any new files, remember to add them here
SET(sources
  ex1.hpp
  ex1.cpp

  mesh_generator.hpp
  mesh_generator.cpp

  castle_generator.hpp
  castle_generator.cpp

  opengl.hpp
  main.cpp
)

add_executable(${CGRA_PROJECT} ${sources})

add_subdirectory(cgra)
add_subdirectory(noise)
add_subdirectory(triangulation)

target_source_group_tree(${CGRA_PROJECT})

target_link_libraries(${CGRA_PROJECT} PRIVATE ${OPENGL_LIBRARY})
target_link_libraries(${CGRA_PROJECT} PRIVATE glfw ${GLFW_LIBRARIES})
target_link_libraries(${CGRA_PROJECT} PRIVATE glew glm imgui libnoise)

target_include_directories(${CGRA_PROJECT} PRIVATE "${PROJECT_SOURCE_DIR}/src")

# Set the source directory as a preprocessor define, used to make sure that the relative paths
# work correctly, regardless of where the project is run fron (as long as it's run on the same
# machine it was built on).
target_compile_definitions(${CGRA_PROJECT} PRIVATE "-DCGRA_SRCDIR=\"${PROJECT_SOURCE_DIR}\"")