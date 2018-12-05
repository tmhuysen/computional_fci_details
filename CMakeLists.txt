cmake_minimum_required(VERSION 3.9)

# Specify the tex file name
set(TEX_NAME FCI)
set(CONFIG_ROOT /Users/quantum/texconfig)
project(FCI NONE)
include(UseLATEX.cmake)


# BUILD: Add a file to the specified project
add_latex_document(${TEX_NAME}.tex
		INPUTS
			packages.tex
)

# POST-BUILD: move the created .pdf-file to the top directory (copy and delete)
add_custom_command(TARGET "${TEX_NAME}_pdf" POST_BUILD
COMMAND ${CMAKE_COMMAND} -E copy "${TEX_NAME}.pdf" ..
COMMAND ${CMAKE_COMMAND} -E remove "${TEX_NAME}.pdf"
COMMENT "Moving PDF-file to top directory.")
