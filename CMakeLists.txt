cmake_minimum_required(VERSION 3.16)
project(PacketAnalyzer VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Source files
set(SOURCES
    src/main.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
)

# Header files location
include_directories(${CMAKE_SOURCE_DIR}/include)

# Create the executable
add_executable(packet_analyzer ${SOURCES})


# DPI Engine
add_executable(dpi_engine
    src/main_dpi.cpp
    src/dpi_engine.cpp
    src/load_balancer.cpp
    src/fast_path.cpp
    src/rule_manager.cpp
    src/connection_tracker.cpp
    src/sni_extractor.cpp
    src/types.cpp
    src/pcap_reader.cpp
    src/packet_parser.cpp
)

target_include_directories(dpi_engine PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

find_package(Threads REQUIRED)
target_link_libraries(dpi_engine PRIVATE Threads::Threads)


# For macOS, we might need to link against system libraries later
if(APPLE)
    # Add any macOS-specific settings here
endif()
