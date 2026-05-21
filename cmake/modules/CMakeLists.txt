#[[
This source file is part of the swift-async-queue open source project

Copyright (c) 2024 Dan Federman and the swift-async-queue project authors
Licensed under MIT License

See https://github.com/dfed/swift-async-queue/blob/main/LICENSE for license information
#]]

include(CMakePackageConfigHelpers)

set(ASYNC_QUEUE_EXPORTS_FILE
  ${CMAKE_CURRENT_BINARY_DIR}/AsyncQueueExports.cmake)

configure_file(AsyncQueueConfig.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/AsyncQueueConfig.cmake)

get_property(ASYNC_QUEUE_EXPORTS GLOBAL PROPERTY ASYNC_QUEUE_EXPORTS)
export(TARGETS ${ASYNC_QUEUE_EXPORTS}
  NAMESPACE AsyncQueue::
  FILE ${ASYNC_QUEUE_EXPORTS_FILE}
  EXPORT_LINK_INTERFACE_LIBRARIES)

install(EXPORT AsyncQueueTargets
  FILE AsyncQueueTargets.cmake
  NAMESPACE AsyncQueue::
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/AsyncQueue)

configure_package_config_file(
  AsyncQueueConfig.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/install/AsyncQueueConfig.cmake
  INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/AsyncQueue)

install(FILES
  ${CMAKE_CURRENT_BINARY_DIR}/install/AsyncQueueConfig.cmake
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/AsyncQueue)
