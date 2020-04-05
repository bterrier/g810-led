# Add subdirectory first
add_subdirectory(classes)

# Then we configure the executable
set(HEADERS
    helpers/help.h
    helpers/utils.h
)

set(SOURCES
    main.cpp
    helpers/help.cpp
    helpers/utils.cpp
)

add_executable(g810-led
    ${SOURCES}
    ${HEADERS}
)

target_link_libraries(g810-led libg810-led)
