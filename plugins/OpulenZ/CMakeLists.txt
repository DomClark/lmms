INCLUDE(BuildPlugin)

# Avoid unused warnings for mididata.h
IF(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-unused-variable")
ENDIF()

INCLUDE_DIRECTORIES(adplug/src)

add_library(adplug_opl_objs OBJECT
	adplug/src/opl.h
	adplug/src/fmopl.c
	adplug/src/fmopl.h
	adplug/src/temuopl.cpp
	adplug/src/temuopl.h
)
set_target_properties(adplug_opl_objs PROPERTIES LMMS_THIRD_PARTY TRUE)

build_plugin(opulenz
	OpulenZ.cpp
	OpulenZ.h
	$<TARGET_OBJECTS:adplug_opl_objs>
	MOCFILES OpulenZ.h
	EMBEDDED_RESOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.png"
)
