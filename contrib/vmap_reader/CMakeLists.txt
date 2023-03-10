# Copyright (C) 2005-2009 MaNGOS project <http://getmangos.com/>
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

cmake_minimum_required(VERSION 2.6...3.20)

project(VmapsReader)

ADD_DEFINITIONS(-DMMAP_GENERATOR -DNO_CORE_FUNCS -DDEBUG)

# zlib
ADD_DEFINITIONS(-DNO_vsnprintf)

ADD_DEFINITIONS("-ggdb")
ADD_DEFINITIONS("-O3")

include_directories(
    ../../src
    ../../src/shared
    ../../src/game
    ../../src/game/vmap
    ../../dep/include/g3dlite
    ../../src/framework
    ../../dep/ACE_wrappers
    ../../objdir/dep/ACE_wrappers
    ../../dep/recastnavigation/Detour/Include
    ../../dep/recastnavigation/Recast/Include
    ../../dep/src/zlib
)

if(WIN32)
  add_library(zlib
      ../../dep/src/zlib/adler32.c
      ../../dep/src/zlib/compress.c
      ../../dep/src/zlib/crc32.c
      ../../dep/src/zlib/deflate.c
      ../../dep/src/zlib/example.c
      ../../dep/src/zlib/gzio.c
      ../../dep/src/zlib/infback.c
      ../../dep/src/zlib/inffast.c
      ../../dep/src/zlib/inflate.c
      ../../dep/src/zlib/inftrees.c
      ../../dep/src/zlib/trees.c
      ../../dep/src/zlib/uncompr.c
      ../../dep/src/zlib/zutil.c
  )
endif(WIN32)

add_library(g3dlite
    ../../dep/src/g3dlite/AABox.cpp
    ../../dep/src/g3dlite/Any.cpp
    ../../dep/src/g3dlite/AnyVal.cpp
    ../../dep/src/g3dlite/AreaMemoryManager.cpp
    ../../dep/src/g3dlite/BinaryFormat.cpp
    ../../dep/src/g3dlite/BinaryInput.cpp
    ../../dep/src/g3dlite/BinaryOutput.cpp
    ../../dep/src/g3dlite/Box.cpp
    ../../dep/src/g3dlite/Box2D.cpp
    ../../dep/src/g3dlite/BumpMapPreprocess.cpp
    ../../dep/src/g3dlite/Capsule.cpp
    ../../dep/src/g3dlite/CollisionDetection.cpp
    ../../dep/src/g3dlite/Color1.cpp
    ../../dep/src/g3dlite/Color1uint8.cpp
    ../../dep/src/g3dlite/Color3.cpp
    ../../dep/src/g3dlite/Color3uint8.cpp
    ../../dep/src/g3dlite/Color4.cpp
    ../../dep/src/g3dlite/Color4uint8.cpp
    ../../dep/src/g3dlite/Cone.cpp
    ../../dep/src/g3dlite/constants.cpp
    ../../dep/src/g3dlite/ConvexPolyhedron.cpp
    ../../dep/src/g3dlite/CoordinateFrame.cpp
    ../../dep/src/g3dlite/Crypto.cpp
    ../../dep/src/g3dlite/Crypto_md5.cpp
    ../../dep/src/g3dlite/Cylinder.cpp
    ../../dep/src/g3dlite/debugAssert.cpp
    ../../dep/src/g3dlite/fileutils.cpp
    ../../dep/src/g3dlite/filter.cpp
    ../../dep/src/g3dlite/format.cpp
    ../../dep/src/g3dlite/g3dfnmatch.cpp
    ../../dep/src/g3dlite/g3dmath.cpp
    ../../dep/src/g3dlite/GCamera.cpp
    ../../dep/src/g3dlite/GLight.cpp
    ../../dep/src/g3dlite/GThread.cpp
    ../../dep/src/g3dlite/GUniqueID.cpp
    ../../dep/src/g3dlite/Intersect.cpp
    ../../dep/src/g3dlite/license.cpp
    ../../dep/src/g3dlite/Line.cpp
    ../../dep/src/g3dlite/LineSegment.cpp
    ../../dep/src/g3dlite/Log.cpp
    ../../dep/src/g3dlite/Matrix.cpp
    ../../dep/src/g3dlite/Matrix3.cpp
    ../../dep/src/g3dlite/Matrix4.cpp
    ../../dep/src/g3dlite/MemoryManager.cpp
    ../../dep/src/g3dlite/MeshAlg.cpp
    ../../dep/src/g3dlite/MeshAlgAdjacency.cpp
    ../../dep/src/g3dlite/MeshAlgWeld.cpp
    ../../dep/src/g3dlite/MeshBuilder.cpp
    ../../dep/src/g3dlite/NetAddress.cpp
    ../../dep/src/g3dlite/NetworkDevice.cpp
    ../../dep/src/g3dlite/PhysicsFrame.cpp
    ../../dep/src/g3dlite/Plane.cpp
    ../../dep/src/g3dlite/PrecomputedRandom.cpp
    ../../dep/src/g3dlite/prompt.cpp
    ../../dep/src/g3dlite/Quat.cpp
    ../../dep/src/g3dlite/Random.cpp
    ../../dep/src/g3dlite/Ray.cpp
    ../../dep/src/g3dlite/Rect2D.cpp
    ../../dep/src/g3dlite/ReferenceCount.cpp
    ../../dep/src/g3dlite/RegistryUtil.cpp
    ../../dep/src/g3dlite/Sphere.cpp
    ../../dep/src/g3dlite/SplineBase.cpp
    ../../dep/src/g3dlite/stringutils.cpp
    ../../dep/src/g3dlite/System.cpp
    ../../dep/src/g3dlite/TextInput.cpp
    ../../dep/src/g3dlite/TextOutput.cpp
    ../../dep/src/g3dlite/ThreadSet.cpp
    ../../dep/src/g3dlite/Triangle.cpp
    ../../dep/src/g3dlite/uint128.cpp
    ../../dep/src/g3dlite/UprightFrame.cpp
    ../../dep/src/g3dlite/Vector2.cpp
    ../../dep/src/g3dlite/Vector2int16.cpp
    ../../dep/src/g3dlite/Vector3.cpp
    ../../dep/src/g3dlite/Vector3int16.cpp
    ../../dep/src/g3dlite/Vector3int32.cpp
    ../../dep/src/g3dlite/Vector4.cpp
    ../../dep/src/g3dlite/Vector4int8.cpp
    ../../dep/src/g3dlite/Welder.cpp
    ../../dep/src/g3dlite/WinMain.cpp
)

if(UNIX)
  find_package(ZLIB REQUIRED)
  if(ZLIB_FOUND)
    include_directories(${ZLIB_INCLUDE_DIRS})
    target_link_libraries(g3dlite ${ZLIB_LIBRARIES})
  endif(ZLIB_FOUND)
else()
  target_link_libraries(g3dlite zlib)
endif(UNIX)

add_library(vmap
	../../src/game/vmap/BIH.cpp
	../../src/game/vmap/VMapManager2.cpp
	../../src/game/vmap/MapTree.cpp
	../../src/game/vmap/TileAssembler.cpp
	../../src/game/vmap/WorldModel.cpp
	../../src/game/vmap/ModelInstance.cpp
)

if(UNIX)
  find_package(ZLIB REQUIRED)
  if(ZLIB_FOUND)
    include_directories(${ZLIB_INCLUDE_DIRS})
    target_link_libraries(vmap ${ZLIB_LIBRARIES} g3dlite)
  endif(ZLIB_FOUND)
else()
  target_link_libraries(vmap zlib g3dlite)
endif(UNIX)

set(SOURCES
    main.cpp
    VMapExtensions.cpp
)

add_executable(vmaps_reader ${SOURCES} )

if(UNIX)
  find_package(ZLIB REQUIRED)
  if(ZLIB_FOUND)
    include_directories(${ZLIB_INCLUDE_DIRS})
    target_link_libraries(vmaps_reader g3dlite vmap ${ZLIB_LIBRARIES})
  endif(ZLIB_FOUND)
else()
  target_link_libraries(vmaps_reader g3dlite vmap zlib)
endif(UNIX)
