project (cork64)

cmake_minimum_required (VERSION 3.1)

set (CMAKE_CXX_STANDARD 11)

#build mpir
add_subdirectory("./mpir-generic")

if ((FIPS_MACOS OR FIPS_WINDOWS OR FIPS_LINUX) AND NOT (FIPS_RASPBERRYPI OR FIPS_OSX_USE_ARC OR FIPS_UWP))


fips_begin_lib(cork64)


include_directories("./")
include_directories("./accel")
include_directories("./file_formats")
include_directories("./isct")
include_directories("./math")
include_directories("./mpz")
include_directories("./mesh")
include_directories("./rawmesh")
include_directories("./util")

#link mpir. Requires pulling and initializing the submodule
include_directories("./mpir-generic")



# fips_files(
# 	GLOB cork_SRC
# 	"./*.cpp"
# 	"./*.h"		
# 	"./accel/*.cpp"
# 	"./accel/*.h"
# 	"./file_formats/*.cpp"
# 	"./file_formats/*.h"
# 	"./isct/*.cpp"
# 	"./isct/*.c"
# 	"./isct/*.h"
# 	"./math/*.cpp"
# 	"./math/*.h"
# 	"./mesh/*.cpp"
# 	"./mesh/*.tpp"
# 	"./mesh/*.h"
# 	"./rawmesh/*.cpp"
# 	"./rawmesh/*.tpp"
# 	"./rawmesh/*.h"
# 	"./util/*.cpp"
# 	"./util/*.h"
# )

# file(
# 	GLOB public_headers
# 	"./*.h"
# )

fips_src(. RECURSE GROUP)

add_definitions(
	-D_USE_MATH_DEFINES 
	-DNOMINMAX 
	-DNO_TIMER
	-DREDUCED
	-DCDT_ONLY
	-DTRILIBRARY
	-DANSI_DECLARATORS
	)

#add_definitions(-DDLLEXPORT)

# add_library(cork64 STATIC ${cork_SRC})

fips_end_lib()

#link mpir
target_link_libraries(cork64 mpir)

endif()


#install public facing headers and lib
# install (TARGETS cork64 DESTINATION ${PROJECT_SOURCE_DIR}/lib)
# install (FILES ${public_headers} DESTINATION ${PROJECT_SOURCE_DIR}/include)

