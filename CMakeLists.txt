CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT (crnlib C CXX)

IF(NOT CMAKE_BUILD_TYPE)
    SET(CMAKE_BUILD_TYPE "Release")
ENDIF(NOT CMAKE_BUILD_TYPE)

IF( ${CMAKE_BUILD_TYPE} STREQUAL Debug )
    # CMAKE_C_FLAGS_DEBUG will also be added to CMAKE_C_FLAGS
    MESSAGE( "Debug build" )
    ADD_DEFINITIONS(-DDEBUG -D_DEBUG -D__DEBUG__)
ENDIF()

IF( BUILD_SHARED_LIBS)
    MESSAGE("Dynamic libs")
    #ADD_DEFINITIONS(-DHLSLCC_DYNLIB)
ENDIF( BUILD_SHARED_LIBS )

SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY "bin" )
SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY "lib" )

#INCLUDE(TestBigEndian)

#TEST_BIG_ENDIAN(BIG_ENDIAN_SYSTEM)

IF(BIG_ENDIAN_SYSTEM)
    MESSAGE("SETTING Big endian")
    ADD_DEFINITIONS(-D__BIG_ENDIAN__)
ELSE()
    MESSAGE("SETTING Little endian")
    ADD_DEFINITIONS(-D__LITTLE_ENDIAN__)
ENDIF()

IF(MSVC)
    OPTION(USE_MSVC_FAST_FLOATINGPOINT "Use MSVC /fp:fast option" ON)
    IF(USE_MSVC_FAST_FLOATINGPOINT)
        ADD_DEFINITIONS(/fp:fast)
    ENDIF(USE_MSVC_FAST_FLOATINGPOINT)
ENDIF(MSVC)

IF(WIN32)
    ADD_DEFINITIONS(-D_CRT_SECURE_NO_WARNINGS /WX /W3 /arch:SSE2)
ENDIF()

#INCLUDE_DIRECTORIES( include src/cbstring/ src/ )

SET(libcrnlib_SOURCES
        crnlib/crn_arealist.cpp
        crnlib/crn_assert.cpp
        crnlib/crn_checksum.cpp
          crnlib/crn_colorized_console.cpp
          crnlib/crn_command_line_params.cpp
          crnlib/crn_comp.cpp
          crnlib/crn_console.cpp
          crnlib/crn_core.cpp
          crnlib/crn_data_stream.cpp
          crnlib/crn_mipmapped_texture.cpp
          crnlib/crn_decomp.cpp
          crnlib/crn_dxt1.cpp
          crnlib/crn_dxt5a.cpp
          crnlib/crn_dxt.cpp
          crnlib/crn_dxt_endpoint_refiner.cpp
          crnlib/crn_dxt_fast.cpp
          crnlib/crn_dxt_hc_common.cpp
          crnlib/crn_dxt_hc.cpp
          crnlib/crn_dxt_image.cpp
          crnlib/crn_dynamic_string.cpp
          crnlib/crn_file_utils.cpp
          crnlib/crn_find_files.cpp
          crnlib/crn_hash.cpp
          crnlib/crn_hash_map.cpp
          crnlib/crn_huffman_codes.cpp
          crnlib/crn_image_utils.cpp
          crnlib/crnlib.cpp
          crnlib/crn_math.cpp
          crnlib/crn_mem.cpp
          crnlib/crn_pixel_format.cpp
          crnlib/crn_platform.cpp
          crnlib/crn_prefix_coding.cpp
          crnlib/crn_qdxt1.cpp
          crnlib/crn_qdxt5.cpp
          crnlib/crn_rand.cpp
          crnlib/crn_resample_filters.cpp
          crnlib/crn_resampler.cpp
          crnlib/crn_ryg_dxt.cpp
          crnlib/crn_sparse_bit_array.cpp
          crnlib/crn_stb_image.cpp
          crnlib/crn_strutils.cpp
          crnlib/crn_symbol_codec.cpp
          crnlib/crn_texture_file_types.cpp
          crnlib/crn_threaded_resampler.cpp
          crnlib/crn_threading_pthreads.cpp
          crnlib/crn_timer.cpp
          crnlib/crn_utils.cpp
          crnlib/crn_value.cpp
          crnlib/crn_vector.cpp
          crnlib/crn_zeng.cpp
          crnlib/crn_texture_comp.cpp
          crnlib/crn_texture_conversion.cpp
          crnlib/crn_dds_comp.cpp
          crnlib/crn_lzma_codec.cpp
          crnlib/crn_ktx_texture.cpp
          crnlib/crn_etc.cpp
          crnlib/crn_rg_etc1.cpp
          crnlib/crn_miniz.cpp
          crnlib/crn_jpge.cpp
          crnlib/crn_jpgd.cpp
          crnlib/lzma_7zBuf2.cpp
          crnlib/lzma_7zBuf.cpp
          crnlib/lzma_7zCrc.cpp
          crnlib/lzma_7zFile.cpp
          crnlib/lzma_7zStream.cpp
          crnlib/lzma_Alloc.cpp
          crnlib/lzma_Bcj2.cpp
          crnlib/lzma_Bra86.cpp
          crnlib/lzma_Bra.cpp
          crnlib/lzma_BraIA64.cpp
          crnlib/lzma_LzFind.cpp
          crnlib/lzma_LzmaDec.cpp
          crnlib/lzma_LzmaEnc.cpp
          crnlib/lzma_LzmaLib.cpp
          
        crnlib/crn_arealist.h
        crnlib/crn_assert.h
        crnlib/crn_checksum.h
          crnlib/crn_colorized_console.h
          crnlib/crn_command_line_params.h
          crnlib/crn_comp.h
          crnlib/crn_console.h
          crnlib/crn_core.h
          crnlib/crn_data_stream.h
          crnlib/crn_mipmapped_texture.h
          crnlib/crn_dxt1.h
          crnlib/crn_dxt5a.h
          crnlib/crn_dxt.h
          crnlib/crn_dxt_endpoint_refiner.h
          crnlib/crn_dxt_fast.h
          crnlib/crn_dxt_hc_common.h
          crnlib/crn_dxt_hc.h
          crnlib/crn_dxt_image.h
          crnlib/crn_dynamic_string.h
          crnlib/crn_file_utils.h
          crnlib/crn_find_files.h
          crnlib/crn_hash.h
          crnlib/crn_hash_map.h
          crnlib/crn_huffman_codes.h
          crnlib/crn_image_utils.h
          crnlib/crn_math.h
          crnlib/crn_mem.h
          crnlib/crn_pixel_format.h
          crnlib/crn_platform.h
          crnlib/crn_prefix_coding.h
          crnlib/crn_qdxt1.h
          crnlib/crn_qdxt5.h
          crnlib/crn_rand.h
          crnlib/crn_resample_filters.h
          crnlib/crn_resampler.h
          crnlib/crn_sparse_bit_array.h
          crnlib/crn_strutils.h
          crnlib/crn_symbol_codec.h
          crnlib/crn_texture_file_types.h
          crnlib/crn_threaded_resampler.h
          crnlib/crn_threading_pthreads.h
          crnlib/crn_timer.h
          crnlib/crn_utils.h
          crnlib/crn_value.h
          crnlib/crn_vector.h
          crnlib/crn_zeng.h
          crnlib/crn_texture_comp.h
          crnlib/crn_texture_conversion.h
          crnlib/crn_dds_comp.h
          crnlib/crn_lzma_codec.h
          crnlib/crn_ktx_texture.h
          crnlib/crn_etc.h
          crnlib/crn_rg_etc1.h
          crnlib/crn_miniz.h
          crnlib/crn_jpge.h
          crnlib/crn_jpgd.h
          crnlib/lzma_7zBuf.h
          crnlib/lzma_7zCrc.h
          crnlib/lzma_7zFile.h
          crnlib/lzma_Alloc.h
          crnlib/lzma_Bcj2.h
          crnlib/lzma_Bra.h
          crnlib/lzma_LzFind.h
          crnlib/lzma_LzmaDec.h
          crnlib/lzma_LzmaEnc.h
          crnlib/lzma_LzmaLib.h

          inc/crn_decomp.h
          inc/crnlib.h
          inc/dds_defs.h
        )
ADD_LIBRARY( crnlib ${libcrnlib_SOURCES} )


#INCLUDE_DIRECTORIES( offline/cjson/ )

#file(GLOB CJSON_CFILES offline/cjson/*.c)
#file(GLOB CJSON_HFILES offline/cjson/*.h)
#source_group("cJSON Files" FILES ${CJSON_CFILES} ${CJSON_HFILES})

#SET(HLSLcc_SOURCES
#        offline/toGLSLStandalone.cpp
#        offline/timer.h
#        offline/timer.cpp
#        offline/hash.h
#        offline/serializeReflection.cpp
#        offline/serializeReflection.h
#        ${CJSON_CFILES}
#        ${CJSON_HFILES}
#        )

#ADD_EXECUTABLE( HLSLcc ${HLSLcc_SOURCES} )

# Compile 32-bit binaries for linux
#IF(CMAKE_HOST_UNIX)#
#
#    ADD_LIBRARY( libHLSLcc-i386 ${libHLSLcc_SOURCES} )
#    ADD_EXECUTABLE( HLSLcc-i386 ${HLSLcc_SOURCES} )
#    TARGET_LINK_LIBRARIES( HLSLcc-i386 libHLSLcc-i386)
#    SET_TARGET_PROPERTIES(libHLSLcc-i386 PROPERTIES COMPILE_FLAGS -m32 LINK_FLAGS -m32 )
#    SET_TARGET_PROPERTIES(HLSLcc-i386 PROPERTIES COMPILE_FLAGS -m32 LINK_FLAGS -m32 )
#ENDIF()

TARGET_LINK_LIBRARIES( crnlib )

# force variables that could be defined on the cmdline
# to be written to the cach

SET( CMAKE_BUILD_TYPE "${CMAKE_BUILD_TYPE}" CACHE STRING
        "One of None Debug Release RelWithDebInfo MinSizeRel" FORCE )
