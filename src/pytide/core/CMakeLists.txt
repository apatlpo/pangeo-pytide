# Copyright (c) 2019 CNES
#
# All rights reserved. Use of this source code is governed by a
# BSD-style license that can be found in the LICENSE file.
file(GLOB_RECURSE WRAPPED_SOURCES "*.cpp")
pybind11_add_module(core ${WRAPPED_SOURCES})
set_target_properties(core PROPERTIES LINK_SEARCH_START_STATIC 1)
set_target_properties(core PROPERTIES LINK_SEARCH_END_STATIC 1)
find_package(MKL)
if(MKL_FOUND)
    add_definitions(-DEIGEN_USE_MKL_ALL)
    include_directories(${MKL_INCLUDE_DIRS})
    target_link_libraries(core PUBLIC ${MKL_LIBRARIES})
endif()
install(TARGETS core DESTINATION lib/tidal_constituents)