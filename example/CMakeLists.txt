
add_executable(pythiafcc-generate generate.cc)

if(${APPLE})
       target_link_libraries(pythiafcc-generate utilities datamodel datamodelDict podio ${PYTHIA8_LIBRARIES} ${HEPMC_LIB} ${fastjet_LIBRARIES})
else()
       target_link_libraries(pythiafcc-generate utilities datamodel datamodelDict podio ${PYTHIA8_LIBRARIES} ${HEPMC_LIB} ${fastjet_LIBRARIES} "-lgfortran")
endif()

install(TARGETS pythiafcc-generate DESTINATION bin)

add_test(NAME generate COMMAND pythiafcc-generate)
set_property(TEST generate PROPERTY ENVIRONMENT LD_LIBRARY_PATH=${CMAKE_INSTALL_PREFIX}/lib:${CMAKE_INSTALL_PREFIX}/examples:$ENV{LD_LIBRARY_PATH})

