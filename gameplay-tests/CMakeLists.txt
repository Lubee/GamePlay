
include_directories( 
    ${CMAKE_SOURCE_DIR}/gameplay/src
    ${CMAKE_SOURCE_DIR}/external-deps/lua/include
    ${CMAKE_SOURCE_DIR}/external-deps/bullet/include
    ${CMAKE_SOURCE_DIR}/external-deps/libpng/include
    ${CMAKE_SOURCE_DIR}/external-deps/oggvorbis/include
    ${CMAKE_SOURCE_DIR}/external-deps/zlib/include
    ${CMAKE_SOURCE_DIR}/external-deps/openal/include
    ${CMAKE_SOURCE_DIR}/external-deps/glew/include
)

add_definitions(-D__linux__)

link_directories(
    ${CMAKE_SOURCE_DIR}/external-deps/lua/lib/linux
    ${CMAKE_SOURCE_DIR}/external-deps/zlib/lib/linux
    ${CMAKE_SOURCE_DIR}/external-deps/libpng/lib/linux
    ${CMAKE_SOURCE_DIR}/external-deps/bullet/lib/linux
    ${CMAKE_SOURCE_DIR}/external-deps/oggvorbis/lib/linux
    ${CMAKE_SOURCE_DIR}/external-deps/glew/lib/linux
)


set(GAMEPLAY_LIBRARIES
    gameplay
    m
    lua
    png
    z
    vorbis
    ogg
    BulletDynamics
    BulletCollision
    LinearMath
    openal
    GLEW
    GL
    rt
    dl
    X11
) 

add_definitions(-lstdc++ -lgameplay -lm -llua -lz -lpng -logg -lvorbis -lBulletCollision -lBulletDynamics -lLinearMath-lopenal -LGLEW -lGL -lrt -ldl -lX11)

set( GAME_NAME gameplay-tests)

set(GAME_SRC
    
    src/FirstPersonCamera.cpp
	src/FirstPersonCamera.h
    src/Grid.cpp
	src/Grid.h
    src/Test.cpp
	src/Test.h
    src/TestsGame.cpp
	src/TestsGame.h
    src/Audio3DTest.cpp
	src/Audio3DTest.h
	src/CreateSceneTest.cpp
	src/CreateSceneTest.h	
	src/CreateSceneTest.h
    src/GestureTest.cpp
    src/GestureTest.h
    src/InputTest.cpp
    src/InputTest.h
	src/LoadSceneTest.cpp
	src/LoadSceneTest.h
	src/MeshBatchTest.cpp
	src/MeshBatchTest.h
	src/MeshPrimitiveTest.cpp
	src/MeshPrimitiveTest.h
	src/PhysicsSceneTest.cpp
	src/PhysicsSceneTest.h
	src/SpriteBatchTest.cpp
	src/SpriteBatchTest.h
	src/TextTest.cpp
	src/TextTest.h
	src/TextureTest.cpp
	src/TextureTest.h
	src/TriangleTest.cpp
	src/TriangleTest.h
)

add_executable(${GAME_NAME}
    ${GAME_SRC}
)

target_link_libraries(${GAME_NAME} ${GAMEPLAY_LIBRARIES})

set_target_properties(${GAME_NAME} PROPERTIES
    OUTPUT_NAME "${GAME_NAME}"
    CLEAN_DIRECT_OUTPUT 1
)

source_group(res FILES ${GAME_RES} ${GAMEPLAY_RES} ${GAME_RES_SHADERS} ${GAME_RES_SHADERS_LIB})
source_group(src FILES ${GAME_SRC})

COPY_RES( ${GAME_NAME} )
COPY_RES_EXTRA( ${GAME_NAME} ${CMAKE_SOURCE_DIR}/gameplay
    res/logo_powered_white.png 
    res/shaders/*
    )
