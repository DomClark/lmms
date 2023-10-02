INCLUDE(BuildPlugin)
INCLUDE_DIRECTORIES(game-music-emu/gme)

add_library(gme_objs OBJECT
	game-music-emu/gme/Gb_Apu.cpp
	game-music-emu/gme/Gb_Apu.h
	game-music-emu/gme/Gb_Oscs.cpp
	game-music-emu/gme/Blip_Buffer.cpp
	game-music-emu/gme/Gb_Oscs.h
	game-music-emu/gme/blargg_common.h
	game-music-emu/gme/Blip_Buffer.h
	game-music-emu/gme/Multi_Buffer.cpp
	game-music-emu/gme/blargg_source.h
	game-music-emu/gme/Multi_Buffer.h
)
set_target_properties(gme_objs PROPERTIES LMMS_THIRD_PARTY TRUE)

build_plugin(freeboy
	FreeBoy.cpp
	FreeBoy.h
	GbApuWrapper.cpp
	GbApuWrapper.h
	$<TARGET_OBJECTS:gme_objs>
	MOCFILES FreeBoy.h
	EMBEDDED_RESOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.png"
)
