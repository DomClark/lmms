INCLUDE(BuildPlugin)

BUILD_PLUGIN(ladspaeffect LadspaEffect.cpp LadspaControls.cpp LadspaControlDialog.cpp LadspaSubPluginFeatures.cpp LadspaEffect.h LadspaControls.h LadspaControlDialog.h LadspaSubPluginFeatures.h MOCFILES LadspaEffect.h LadspaControls.h LadspaControlDialog.h EMBEDDED_RESOURCES logo.png)

SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/ladspa")

IF(LMMS_HAVE_CAPS)
    add_subdirectory(caps)
    set_property(DIRECTORY caps PROPERTY LMMS_THIRD_PARTY TRUE)
ENDIF()

IF(LMMS_HAVE_TAP)
    add_subdirectory(tap)
    set_property(DIRECTORY tap PROPERTY LMMS_THIRD_PARTY TRUE)
ENDIF()

IF(LMMS_HAVE_SWH)
    add_subdirectory(swh)
    set_property(DIRECTORY swh PROPERTY LMMS_THIRD_PARTY TRUE)
ENDIF()

IF(LMMS_HAVE_CMT)
    add_subdirectory(cmt)
    set_property(DIRECTORY cmt PROPERTY LMMS_THIRD_PARTY TRUE)
ENDIF()

IF(LMMS_HAVE_CALF)
    add_subdirectory(calf)
    set_property(DIRECTORY calf PROPERTY LMMS_THIRD_PARTY TRUE)
ENDIF()
