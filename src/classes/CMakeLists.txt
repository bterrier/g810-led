# Search hidapi
find_library(HIDAPI_LIB hidapi-hidraw)

# Search libusb
find_library(LIBUSB_LIB usb-1.0)


if (NOT LIBUSB_LIB AND NOT HIDAPI_LIB)
    message(FATAL_ERROR "Requires libusb or hidapi!")
endif()

# If the user did not choose a library, we try to use hidapi if available
if (NOT LIB)
    if (HIDAPI_LIB)
        set(LIB hidapi)
    else()
        set(LIB libusb)
    endif()
endif()

# Set the flags and defines for the selected library
if (LIB STREQUAL "libusb")
    add_definitions(-Dlibusb)
    set(USB_LIB -lusb-1.0)
else()
    add_definitions(-Dhidapi)
    set(USB_LIB -lhidapi-hidraw)
endif()


set(HEADERS
    Keyboard.h
)

set(SOURCES
    Keyboard.cpp
)

add_library(libg810-led
    ${SOURCES}
    ${HEADERS}
    )

target_link_libraries(libg810-led ${USB_LIB})
