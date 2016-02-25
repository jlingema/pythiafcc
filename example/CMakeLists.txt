
add_executable(pythiafcc-generate generate.cc)

if(${APPLE})
       target_link_libraries(pythiafcc-generate utilities datamodel datamodelDict podio ${PYTHIA8_LIBRARIES} ${HEPMC_LIB} ${fastjet_LIBRARIES})
else()
       target_link_libraries(pythiafcc-generate utilities datamodel datamodelDict podio ${PYTHIA8_LIBRARIES} ${HEPMC_LIB} ${fastjet_LIBRARIES} "-lgfortran")
endif()

install(TARGETS pythiafcc-generate DESTINATION bin)

add_test(NAME generate-ee-ttbar COMMAND pythiafcc-generate ${CMAKE_INSTALL_PREFIX}/../example/ee_ttbar.txt)
set_property(TEST generate-ee-ttbar PROPERTY ENVIRONMENT LD_LIBRARY_PATH=${CMAKE_INSTALL_PREFIX}/lib:${CMAKE_INSTALL_PREFIX}/examples:$ENV{LD_LIBRARY_PATH})

add_test(NAME generate-hh-ttbar COMMAND pythiafcc-generate ${CMAKE_INSTALL_PREFIX}/../example/hh_ttbar.txt)
set_property(TEST generate-hh-ttbar PROPERTY ENVIRONMENT LD_LIBRARY_PATH=${CMAKE_INSTALL_PREFIX}/lib:${CMAKE_INSTALL_PREFIX}/examples:$ENV{LD_LIBRARY_PATH})

add_test(NAME generate-ZH_Zmumu_Hbb COMMAND pythiafcc-generate ${CMAKE_INSTALL_PREFIX}/../example/ZH_Zmumu_Hbb.txt)
set_property(TEST generate-ZH_Zmumu_Hbb PROPERTY ENVIRONMENT LD_LIBRARY_PATH=${CMAKE_INSTALL_PREFIX}/lib:${CMAKE_INSTALL_PREFIX}/examples:$ENV{LD_LIBRARY_PATH})
