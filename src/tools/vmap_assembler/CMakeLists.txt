# Copyright (C) 2008-2012 OregonCore <http://www.oregoncore.com/>
# Copyright (C) 2008-2012 TrinityCore <http://www.trinitycore.org/>
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

include_directories(
  ${CMAKE_SOURCE_DIR}/dep/g3dlite/include
  ${CMAKE_SOURCE_DIR}/src/server/shared
  ${CMAKE_SOURCE_DIR}/src/server/shared/Dynamic  
  ${CMAKE_SOURCE_DIR}/src/server/collision/Maps
  ${CMAKE_SOURCE_DIR}/src/server/collision/Models
  ${CMAKE_SOURCE_DIR}/src/framework  
  ${CMAKE_SOURCE_DIR}/src/framework/Platform
  ${ACE_INCLUDE_DIR}
  ${ZLIB_INCLUDE_DIR}
)

add_definitions(-DNO_CORE_FUNCS)
add_executable(vmap_assembler VMapAssembler.cpp)
add_dependencies(vmap_assembler mpq)

if(CMAKE_SYSTEM_NAME MATCHES "Darwin")
  set_target_properties(vmap_assembler PROPERTIES LINK_FLAGS "-framework Carbon")
endif()

target_link_libraries(vmap_assembler
  collision
  g3dlib
  ${ZLIB_LIBRARIES}
)

if( UNIX )
  install(TARGETS vmap_assembler DESTINATION bin)
elseif( WIN32 )
  install(TARGETS vmap_assembler DESTINATION "${CMAKE_INSTALL_PREFIX}")
endif()
