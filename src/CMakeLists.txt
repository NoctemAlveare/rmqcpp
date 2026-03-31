find_package(Threads REQUIRED) # CMake 3.26-rc3 Bug https://gitlab.kitware.com/cmake/cmake/-/issues/24505
find_package(ZLIB REQUIRED)
if (ENABLE_COMPRESSION)
    find_package(zstd CONFIG REQUIRED)
endif()
find_package(Boost REQUIRED)
set(OPENSSL_USE_STATIC_LIBS TRUE)
find_package(OpenSSL REQUIRED)

# BDE-required subpackages
find_package(bal REQUIRED)

add_subdirectory(rmq)
# Only add rmqtestmocks and tests when BUILD_TESTING is enabled
if(BUILD_TESTING)
    find_package(GTest REQUIRED)
    add_subdirectory(rmqtestmocks)
    add_subdirectory(tests)
endif()
