# Use weak jack library linking
if(LMMS_HAVE_WEAKJACK)
	# TODO CMake 3.12: Rename weakjack_objs to weakjack and use it directly
	add_library(weakjack_objs OBJECT weakjack/weak_libjack.c weakjack/weak_libjack.h)
	target_include_directories(weakjack_objs PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/weakjack" "${JACK_INCLUDE_DIRS}")
	set_target_properties(weakjack_objs PROPERTIES C_STANDARD 11)
	# Enable weakjack, disable metadata support
	target_compile_definitions(weakjack_objs PUBLIC USE_WEAK_JACK=1 NO_JACK_METADATA=1)

	# Create an interface library that can be used to pull in the required object files for linking
	add_library(weakjack INTERFACE)
	target_sources(weakjack INTERFACE $<TARGET_OBJECTS:weakjack_objs>)
	target_include_directories(weakjack INTERFACE $<TARGET_PROPERTY:weakjack_objs,INTERFACE_INCLUDE_DIRECTORIES>)
	target_compile_definitions(weakjack INTERFACE $<TARGET_PROPERTY:weakjack_objs,INTERFACE_COMPILE_DEFINITIONS>)
endif()
