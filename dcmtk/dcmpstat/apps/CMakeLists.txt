# declare additional include directories
INCLUDE_DIRECTORIES(${dcmtls_SOURCE_DIR}/include ${LIBXML_INCDIR})

# declare directories containing used libraries
LINK_DIRECTORIES(${dcmpstat_BINARY_DIR} ${ofstd_BINARY_DIR} ${dcmdata_BINARY_DIR} ${dcmtls_BINARY_DIR} ${dcmnet_BINARY_DIR} ${dcmqrdb_BINARY_DIR} ${dcmimgle_BINARY_DIR} ${dcmsr_BINARY_DIR} ${dcmsign_BINARY_DIR} ${ZLIB_LIBDIR} ${LIBXML_LIBDIR} ${OPENSSL_LIBDIR})

# declare executables
FOREACH(PROGRAM dcmmkcrv dcmmklut dcmp2pgm dcmprscp dcmprscu dcmpsmk dcmpsprt dcmpsrcv dcmpssnd)
  ADD_EXECUTABLE(${PROGRAM} ${PROGRAM})
ENDFOREACH(PROGRAM)
ADD_EXECUTABLE(dcmpschk dcmpschk vrscan)

# declare installation files
FOREACH(PROGRAM dcmmkcrv dcmmklut dcmp2pgm dcmprscp dcmprscu dcmpschk dcmpsmk dcmpsprt dcmpsrcv dcmpssnd)
  INSTALL_TARGETS(${INSTALL_BINDIR} ${PROGRAM})
ENDFOREACH(PROGRAM)

# make sure executables are linked to the corresponding libraries
FOREACH(PROGRAM dcmmkcrv dcmmklut dcmp2pgm dcmprscp dcmprscu dcmpsmk dcmpschk dcmpsprt dcmpsrcv dcmpssnd)
  TARGET_LINK_LIBRARIES(${PROGRAM} netapi32 wsock32 ofstd dcmdata dcmnet dcmqrdb dcmimgle dcmpstat ${ZLIB_LIBS})
ENDFOREACH(PROGRAM)
FOREACH(PROGRAM dcmmklut dcmp2pgm dcmprscp dcmprscu dcmpschk dcmpsmk dcmpsprt dcmpsrcv dcmpssnd)
  TARGET_LINK_LIBRARIES(${PROGRAM} dcmsr)
ENDFOREACH(PROGRAM)
FOREACH(PROGRAM dcmp2pgm dcmprscp dcmprscu dcmpsprt dcmpsrcv dcmpssnd)
  TARGET_LINK_LIBRARIES(${PROGRAM} dcmtls dcmdsig ${LIBXML_LIBS} ${OPENSSL_LIBS})
ENDFOREACH(PROGRAM)
