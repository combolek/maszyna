
file(GLOB_RECURSE src "*.hlsl*" "*.h")
list(APPEND src "project.manul")

get_target_property(dxil_path MaSzynaShaderCompiler dxil_path)

# OUTPUT_CONFIG makes the compiler follow the configuration being built.
# Without it the first COMMAND argument resolves in the "command config",
# i.e. the config of the build-<Config>.ninja in use, which under
# Ninja Multi-Config is Debug even for ninja all:Release.
add_custom_target(
        ${LIBMANUL_NAME}_shaders
        COMMAND $<OUTPUT_CONFIG:$<TARGET_FILE:MaSzynaShaderCompiler>>
                "${dxil_path}"
                "${CMAKE_CURRENT_SOURCE_DIR}/project.manul"
                "$<TARGET_FILE_DIR:${PROJECT_NAME}>/shaders"
        DEPENDS ${src})
