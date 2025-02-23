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
MESSAGE("\n**** Configuring Downloader Solo ****")

FIND_PACKAGE(Boost REQUIRED COMPONENTS program_options)

FIND_PACKAGE(Qt4 REQUIRED)
INCLUDE(${QT_USE_FILE})

SET(INC ${CMAKE_SOURCE_DIR}/xfstk-sources/core)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/xfstk-sources/core/factory
    ${INC}/factory
    ${INC}/command-line-helper
    ${INC}/downloader-solo)

SET (SRCS
    ${INC}/downloader-solo/xfstkdownloader.cpp
    ${INC}/downloader-solo/xfstkdownloadermain.cpp
    ${CMAKE_CURRENT_BINARY_DIR})

ADD_EXECUTABLE(xfstk-dldr-solo
    ${SRCS})

TARGET_LINK_LIBRARIES(xfstk-dldr-solo
    ${Boost_LIBRARIES}
    ${QT_LIBRARIES}
    XfstkFactory
    )

INSTALL(TARGETS xfstk-dldr-solo
  RUNTIME DESTINATION /usr/bin
    COMPONENT cli)
