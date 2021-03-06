set(MODULE src)
set(BASE "${CMAKE_CURRENT_SOURCE_DIR}")

add_subdirectory(drivers)
add_subdirectory(third)
add_subdirectory(util)

set(
    SOURCES
    "${BASE}/arbiter.cpp"
    "${BASE}/driver.cpp"
    "${BASE}/endpoint.cpp"
)

set(
    HEADERS
    "${BASE}/arbiter.hpp"
    "${BASE}/driver.hpp"
    "${BASE}/endpoint.hpp"
)

install(FILES ${HEADERS} DESTINATION include/arbiter)

if (WIN32)
    add_library(${MODULE} OBJECT ${SOURCES} ${HEADERS})
    set_target_properties(${MODULE}
        PROPERTIES
            COMPILE_DEFINITIONS ARBITER_DLL_EXPORT)
else()
    add_library(${MODULE} OBJECT ${SOURCES})
endif()

