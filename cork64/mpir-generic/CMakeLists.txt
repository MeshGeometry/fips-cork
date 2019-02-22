project (mpir-generic C)

cmake_minimum_required (VERSION 2.8.6)

if ((FIPS_MACOS OR FIPS_WINDOWS OR FIPS_LINUX) AND NOT (FIPS_RASPBERRYPI OR FIPS_OSX_USE_ARC OR FIPS_UWP))

fips_begin_lib(mpir)

include_directories("./")
include_directories("./fft")
include_directories("./mpf")
include_directories("./mpq")
include_directories("./mpn/generic")
include_directories("./mpz")
include_directories("./printf")
include_directories("./scanf")

fips_src(. RECURSE GROUP)

add_definitions(-DHAVE_CONFIG_H)
add_definitions(-D_LIB)

if(WIN32)
	add_definitions(-D_WIN64) #usually building for x64
endif()

fips_end_lib()

endif()

