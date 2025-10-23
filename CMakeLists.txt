# SlicerPySera/CMakeLists.txt
cmake_minimum_required(VERSION 3.16.3)
project(SlicerPySera)

set(EXTENSION_HOMEPAGE "https://example.com/SlicerPySera")
set(EXTENSION_CATEGORY "Radiomics")
set(EXTENSION_CONTRIBUTORS "Your Name (Institution)")
set(EXTENSION_DESCRIPTION "PySera: radiomics extraction library + Slicer UI wrapper")
set(EXTENSION_ICONURL "")
set(EXTENSION_SCREENSHOTURLS "")

find_package(Slicer REQUIRED)
include(${Slicer_USE_FILE})

# Add the scripted module (PySera_Ext)
add_subdirectory(PySera_Ext)

# Optionally: add CLI and Qt modules if needed
add_subdirectory(PySeraCLI)
add_subdirectory(PySeraQt)

include(${Slicer_EXTENSION_CPACK})
