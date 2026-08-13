cmake_minimum_required(VERSION 3.20)
project(blns23_q7933 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(Boost REQUIRED)
find_package(OpenSSL REQUIRED)

add_library(blns23_q7933
    src/blindsig_blns7933.cpp
    src/blindsig_blns7933_integer_ring.cpp
    src/blindsig_blns7933_ntrusolve.cpp
    src/blindsig_blns7933_reduce.cpp
    src/blindsig_blns7933_babai_reduce.cpp
    src/blindsig_blns7933_gaussian.cpp
    src/blindsig_blns7933_quality.cpp
    src/blindsig_blns7933_real_ring.cpp
    src/blindsig_blns7933_ldl.cpp
    src/blindsig_blns7933_sampling.cpp
    src/blindsig_blns7933_sign.cpp
    src/blindsig_blns7933_csprng.cpp
)
add_library(blns23::q7933 ALIAS blns23_q7933)

target_include_directories(blns23_q7933
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
        ${Boost_INCLUDE_DIRS}
)
target_link_libraries(blns23_q7933 PUBLIC OpenSSL::Crypto)
target_compile_options(blns23_q7933 PRIVATE
    -Wall -Wextra -Wpedantic -Wconversion -Wshadow
)

include(GNUInstallDirs)
install(TARGETS blns23_q7933
    EXPORT blns23Q7933Targets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(EXPORT blns23Q7933Targets
    NAMESPACE blns23::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/blns23-q7933
)
