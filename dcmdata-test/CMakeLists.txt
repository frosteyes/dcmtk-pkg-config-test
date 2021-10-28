# Access to system installed dcmtk
find_package(PkgConfig REQUIRED) 
pkg_check_modules(DCMTK REQUIRED dcmtk) 

# declare executables
add_executable(local_dcmdata_tests
  tchval.cc
  tdict.cc
  telemlen.cc
  tests.cc
  tfilter.cc
  tgenuid.cc
  ti2dbmp.cc
  titem.cc
  tmatch.cc
  tnewdcme.cc
  tparent.cc
  tparser.cc
  tpath.cc
  tpread.cc
  tsequen.cc
  tspchrs.cc
  tstrval.cc
  tvrcomp.cc
  tvrdatim.cc
  tvrds.cc
  tvrfd.cc
  tvrol.cc
  tvrov.cc
  tvrpn.cc
  tvrsv.cc
  tvrui.cc
  tvruv.cc
)

# make sure executables are linked to the DCMTK libs
target_link_libraries(local_dcmdata_tests ${DCMTK_LIBRARIES})
