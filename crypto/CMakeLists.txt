INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})

IF (CRYPTO STREQUAL INTERNAL OR CRYPTO STREQUAL TOMCRYPT)

SET(sources crypto.c)

IF (CRYPTO STREQUAL INTERNAL)
	SET(sources
		${sources}
		crypto.c
		md4.c
		md5.c
		sha1.c
		des.c
	)
ENDIF(CRYPTO STREQUAL INTERNAL)

ADD_LIBRARY(internal-crypto SHARED ${sources})
IF (CRYPTO STREQUAL TOMCRYPT)
	TARGET_LINK_LIBRARIES(internal-crypto tomcrypt)
ENDIF(CRYPTO STREQUAL TOMCRYPT)

INSTALL(TARGETS internal-crypto LIBRARY DESTINATION lib${LIB_SUFFIX}/accel-ppp )

ENDIF(CRYPTO STREQUAL INTERNAL OR CRYPTO STREQUAL TOMCRYPT)
