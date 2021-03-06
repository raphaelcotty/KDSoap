## This file is part of the KD Soap library.
##
## SPDX-FileCopyrightText: 2021 Klarälvdalens Datakonsult AB, a KDAB Group company <info@kdab.com>
##
## SPDX-License-Identifier: LGPL-2.1-only OR LGPL-3.0-only OR GPL-2.0-only OR GPL-3.0-only OR LicenseRef-KDAB-KDSoap OR LicenseRef-KDAB-KDSoap-US
##
## Licensees holding valid commercial KD Soap licenses may use this file in
## accordance with the KD Soap Commercial License Agreement provided with
## the Software.
##
## Contact info@kdab.com if any conditions of this licensing are not clear to you.
##

# qhelpgenerator
find_program(QHELPGEN_EXECUTABLE qhelpgenerator
  HINTS ${QT_INSTALL_BINS}
)
if(QHELPGEN_EXECUTABLE)
  set(HAVE_QHELPGEN "YES")
else()
  set(HAVE_QHELPGEN "NO")
  message(STATUS "Unable to generate the API documentation in qch format. To fix, install the qthelpgenerator program which comes with Qt5.")
endif()

# Doxygen
find_package(Doxygen)
set_package_properties(Doxygen PROPERTIES
  TYPE OPTIONAL
  DESCRIPTION "API Documentation system"
  URL "https://www.doxygen.org"
  PURPOSE "Needed to build the API documentation."
)
if(DOXYGEN_DOT_EXECUTABLE)
  set(HAVE_DOT "YES")
else()
  set(HAVE_DOT "NO")
  message(STATUS "Unable to provide inheritance diagrams for the API documentation. To fix, install the graphviz project from https://www.graphviz.org")
endif()

if(DOXYGEN_FOUND)
  add_subdirectory(api)
endif()
