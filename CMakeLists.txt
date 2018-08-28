CMAKE_MINIMUM_REQUIRED(VERSION 3.10)

project(CNPY)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

install(FILES "cnpy.h" DESTINATION include)
install(FILES "mat2npz" "npy2mat" "npz2mat" DESTINATION bin PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)

add_executable(example1 example1.cpp)
option(USE_ZLIB "Enable zlib for support of compressed *.npz files." OFF)
if (USE_ZLIB)
    find_package(ZLIB REQUIRED)
    include_directories(${ZLIB_INCLUDE_DIRS})
    target_compile_definitions(example1 PRIVATE CNPY_USE_ZLIB)
    target_link_libraries(example1 ${ZLIB_LIBRARIES})
endif (USE_ZLIB)
