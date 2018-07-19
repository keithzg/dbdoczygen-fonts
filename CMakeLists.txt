project(OxygenFont)
set(PROJECT_VERSION "5.4.90")
cmake_minimum_required(VERSION 2.8.12)

find_package(ECM 1.2.0 REQUIRED NO_MODULE)

set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})

include(KDEInstallDirs)
include(ECMPackageConfigHelpers)
include(ECMSetupVersion)
include(FeatureSummary)

# create a Config.cmake and a ConfigVersion.cmake file and install them
set(CMAKECONFIG_INSTALL_DIR "${CMAKECONFIG_INSTALL_PREFIX}/OxygenFont")

include(ECMPackageConfigHelpers)

ecm_setup_version(${PROJECT_VERSION} VARIABLE_PREFIX OXYGENFONT
                  PACKAGE_VERSION_FILE "${CMAKE_CURRENT_BINARY_DIR}/OxygenFontConfigVersion.cmake"
)

ecm_configure_package_config_file("${CMAKE_CURRENT_SOURCE_DIR}/OxygenFontConfig.cmake.in"
                                  "${CMAKE_CURRENT_BINARY_DIR}/OxygenFontConfig.cmake"
                                  INSTALL_DESTINATION  ${CMAKECONFIG_INSTALL_DIR}
)

install(FILES
        "${CMAKE_CURRENT_BINARY_DIR}/OxygenFontConfig.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/OxygenFontConfigVersion.cmake"
        DESTINATION "${CMAKECONFIG_INSTALL_DIR}"
        COMPONENT Devel)

if(NOT DEFINED OXYGEN_FONT_INSTALL_DIR)
  set(OXYGEN_FONT_INSTALL_DIR  ${CMAKE_INSTALL_PREFIX}/${SHARE_INSTALL_PREFIX}/fonts/truetype/oxygen)
endif()

find_program(FONTFORGE_EXECUTABLE NAMES fontforge)
if(FONTFORGE_EXECUTABLE)
    message(STATUS "FontForge found: ${FONTFORGE_EXECUTABLE}")
else()
    message(FATAL_ERROR "Could not find FontForge executable")
endif()

find_program(MKEOT_EXECUTABLE NAMES mkeot)
if(MKEOT_EXECUTABLE)
    message(STATUS "mkeot from eot-utils found: ${MKEOT_EXECUTABLE}")
else()
    message(FATAL_ERROR "Could not find mkeot executable")
endif()

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)

add_custom_target(regular_ttf ALL fontforge ${CMAKE_CURRENT_SOURCE_DIR}/generate-ttf.pe
                   ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Regular-400/src/Oxygen-GMCL-Sans.sfd
                   ${CMAKE_CURRENT_BINARY_DIR}/oxygen-fonts/Regular-400/Oxygen-GMCL-Sans.ttf
                  )
add_custom_target(regular_eot ALL mkeot 
                   ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Regular-400/Oxygen-GMCL-Sans.ttf > ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Regular-400/Oxygen-GMCL-Sans.eot
                  )
add_dependencies(regular_eot regular_ttf)
add_custom_target(bold_ttf ALL fontforge ${CMAKE_CURRENT_SOURCE_DIR}/generate-ttf.pe
                   ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Bold-700/src/Oxygen-GMCL-Sans-Bold.sfd
                   ${CMAKE_CURRENT_BINARY_DIR}/oxygen-fonts/Bold-700/Oxygen-GMCL-Sans-Bold.ttf
                  )
add_custom_target(bold_eot ALL mkeot 
                   ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Bold-700/Oxygen-GMCL-Sans-Bold.ttf > ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Bold-700/Oxygen-GMCL-Sans-Bold.eot
                  )
add_dependencies(bold_eot bold_ttf)
add_custom_target(mono_ttf ALL fontforge ${CMAKE_CURRENT_SOURCE_DIR}/generate-ttf.pe
                   ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/mono-400/src/OxygenMono-Regular.sfd
                   ${CMAKE_CURRENT_BINARY_DIR}/oxygen-fonts/mono-400/OxygenMono-Regular.ttf
                  )
add_custom_target(mono_eot ALL mkeot 
                   ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/mono-400/OxygenMono-Regular.ttf > ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/mono-400/OxygenMono-Regular.eot
                  )
add_dependencies(mono_eot mono_ttf)

set(fontFiles
    ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/mono-400/OxygenMono-Regular.ttf
    ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Bold-700/Oxygen-GMCL-Sans-Bold.ttf
    ${CMAKE_CURRENT_SOURCE_DIR}/oxygen-fonts/Regular-400/Oxygen-GMCL-Sans.ttf
)

install(FILES ${fontFiles} DESTINATION ${OXYGEN_FONT_INSTALL_DIR})
install(FILES org.kde.oxygen-fonts.metainfo.xml DESTINATION ${CMAKE_INSTALL_METAINFODIR})
