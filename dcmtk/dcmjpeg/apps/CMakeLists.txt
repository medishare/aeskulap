# declare additional include directories
INCLUDE_DIRECTORIES(${dcmjpeg_SOURCE_DIR}/include ${ofstd_SOURCE_DIR}/include ${dcmdata_SOURCE_DIR}/include ${dcmimgle_SOURCE_DIR}/include ${dcmimage_SOURCE_DIR}/include ${dcmjpeg_SOURCE_DIR}/libijg8 ${dcmjpeg_SOURCE_DIR}/libijg12 ${dcmjpeg_SOURCE_DIR}/libijg16 ${ZLIB_INCDIR} ${LIBTIFF_INCDIR} ${LIBPNG_INCDIR})

# declare directories containing used libraries
LINK_DIRECTORIES(${dcmjpeg_BINARY_DIR} ${ofstd_BINARY_DIR} ${dcmdata_BINARY_DIR} ${dcmimgle_BINARY_DIR} ${dcmimage_BINARY_DIR}  ${ZLIB_LIBDIR} ${LIBTIFF_LIBDIR} ${LIBPNG_LIBDIR})

# declare executables
FOREACH(PROGRAM dcmcjpeg dcmdjpeg dcmj2pnm dcmmkdir)
  ADD_EXECUTABLE(${PROGRAM} ${PROGRAM})
ENDFOREACH(PROGRAM)

# declare installation files
FOREACH(PROGRAM dcmcjpeg dcmdjpeg dcmj2pnm dcmmkdir)
  INSTALL_TARGETS(${INSTALL_BINDIR} ${PROGRAM})
ENDFOREACH(PROGRAM)

# make sure executables are linked to the corresponding libraries
FOREACH(PROGRAM dcmcjpeg dcmdjpeg dcmj2pnm dcmmkdir)
  TARGET_LINK_LIBRARIES(${PROGRAM} netapi32 wsock32 ofstd dcmdata dcmimgle dcmimage dcmjpeg ijg8 ijg12 ijg16 ${ZLIB_LIBS})
ENDFOREACH(PROGRAM)
TARGET_LINK_LIBRARIES(dcmj2pnm ${LIBTIFF_LIBS} ${LIBPNG_LIBS})
