cmake_minimum_required(VERSION 3.9)

# Specify the tex file name
set(TEX_NAME CI)
set(CONFIG_ROOT /Users/quantum/texconfig)
project(CI NONE)
include(UseLATEX.cmake)


# BUILD: Add a file to the specified project
add_latex_document(${TEX_NAME}.tex
		INPUTS
			packages.tex
			main/fci.tex
			main/frozen.tex
			main/address.tex
		IMAGE_DIRS
			graphs
)

# POST-BUILD: move the created .pdf-file to the top directory (copy and delete)
add_custom_command(TARGET "${TEX_NAME}_pdf" POST_BUILD
COMMAND ${CMAKE_COMMAND} -E copy "${TEX_NAME}.pdf" ..
COMMAND ${CMAKE_COMMAND} -E copy "${TEX_NAME}.pdf" ../../../Products
COMMAND ${CMAKE_COMMAND} -E remove "${TEX_NAME}.pdf"
COMMENT "Moving PDF-file to top directory.")
