#	 Copyright (C) 2014  Intel Corporation
#
#    This library is free software; you can redistribute it and/or
#    modify it under the terms of the GNU Lesser General Public
#    License as published by the Free Software Foundation; either
#    version 2.1 of the License, or (at your option) any later version.
#
#    This library is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
#    Lesser General Public License for more details.
#
#    You should have received a copy of the GNU Lesser General Public
#    License along with this library; if not, write to the Free Software
#    Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA
MESSAGE("\n**** Configuring Plugin: CloverviewPlus ****")

FIND_PACKAGE(Qt4 REQUIRED)
INCLUDE(${QT_USE_FILE})

# Find ui files.
file(GLOB GUI_UI ${CMAKE_SOURCE_DIR}/xfstk-sources/plugins/downloader/cloverviewplus/*.ui)

# Run UIC on them
QT4_WRAP_UI(UIC_SOURCES ${GUI_UI})

SET(CP      ${CMAKE_SOURCE_DIR}/xfstk-sources/plugins/downloader/cloverviewplus)
SET(DLDR    ${CMAKE_SOURCE_DIR}/xfstk-sources/plugins/downloader)
SET(DA      ${CMAKE_SOURCE_DIR}/xfstk-sources/api/downloader-api)

# Show Cmake where the header files are.
INCLUDE_DIRECTORIES(
    ${CP}
    ${DLDR}
    ${DA}
    ${CMAKE_CURRENT_BINARY_DIR})

ADD_LIBRARY(XfstkDldrPluginCloverviewPlus
    SHARED
        ${CP}/xfstkdldrpluginuserinterface.cpp
        ${CP}/xfstkdldrpluginoptionsinterface.cpp
        ${CP}/xfstkdldrplugincloverviewplus.cpp
        ${CP}/xfstkdldrthread.cpp
        ${UIC_SOURCES})

target_link_libraries(XfstkDldrPluginCloverviewPlus
    xfstk-command-line
    XfstkFactory
    ${QT_LIBRARIES}
    xfstk-dldr-gui-api
    )

SET_TARGET_PROPERTIES(XfstkDldrPluginCloverviewPlus
    PROPERTIES
        AUTOMOC true)

INSTALL(TARGETS XfstkDldrPluginCloverviewPlus
        LIBRARY DESTINATION /usr/lib/xfstk/xfstkdldrplugins
        COMPONENT gui)

