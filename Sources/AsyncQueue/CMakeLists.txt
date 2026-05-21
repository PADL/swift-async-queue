#[[
This source file is part of the swift-async-queue open source project

Copyright (c) 2024 Dan Federman and the swift-async-queue project authors
Licensed under MIT License

See https://github.com/dfed/swift-async-queue/blob/main/LICENSE for license information
#]]

file(GLOB_RECURSE ASYNC_QUEUE_SOURCES CONFIGURE_DEPENDS
  *.swift)

add_library(AsyncQueue ${ASYNC_QUEUE_SOURCES})

# Match Package.swift: .swiftLanguageMode(.v6)
target_compile_options(AsyncQueue PRIVATE
  "$<$<COMPILE_LANGUAGE:Swift>:-swift-version;6>")

get_swift_host_os(_swift_os)
set_target_properties(AsyncQueue PROPERTIES
  SOVERSION 0
  INTERFACE_INCLUDE_DIRECTORIES
    "$<BUILD_INTERFACE:${CMAKE_Swift_MODULE_DIRECTORY}>;$<INSTALL_INTERFACE:${CMAKE_INSTALL_LIBDIR}/swift/${_swift_os}>")

_install_target(AsyncQueue)
set_property(GLOBAL APPEND PROPERTY ASYNC_QUEUE_EXPORTS AsyncQueue)
