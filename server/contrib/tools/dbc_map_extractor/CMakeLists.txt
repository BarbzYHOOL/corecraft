#
# Copyright (C) 2014 Corecraft <https://www.worldofcorecraft.com/>
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
#

file(GLOB_RECURSE source *.cpp *.h)

set(source
  ${source}
  ${CMAKE_CURRENT_SOURCE_DIR}/loadlib/adt.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/loadlib/loadlib.cpp
)

set(include_dirs
  ${CMAKE_SOURCE_DIR}/dep/libmpq
  ${CMAKE_CURRENT_SOURCE_DIR}/loadlib
  ${CMAKE_CURRENT_SOURCE_DIR}
)

include_directories(${include_dirs})

add_executable(dbc_map_extractor
  ${source}
)

target_link_libraries(dbc_map_extractor
  mpq
  ${BZIP2_LIBRARIES}
  ${ZLIB_LIBRARIES}
)

install(TARGETS dbc_map_extractor DESTINATION ${BIN_DIR})

if(OPTIMIZED)
  add_definitions(-DOPTIMIZED_BUILD)
endif()
