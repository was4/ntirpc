include_directories(
  ${LTTNG_INCLUDE_DIR}
)

set(ntirpc_tracepoints_LIB_SRCS
  rpcping.c
  xprt.c
)

add_library(ntirpc_tracepoints SHARED ${ntirpc_tracepoints_LIB_SRCS})
#add_sanitizers(ntirpc_tracepoints)

target_link_libraries(ntirpc_tracepoints
  ${LTTNG_LIBRARIES}
)

set_target_properties(ntirpc_tracepoints PROPERTIES
  VERSION ${NTIRPC_VERSION}
  SOVERSION "${NTIRPC_MAJOR_VERSION}.${NTIRPC_MINOR_VERSION}"
  )

install(TARGETS ntirpc_tracepoints COMPONENT tracing DESTINATION ${LIB_INSTALL_DIR} )

set(ntirpc_lttng_LIB_SRCS
  main.c
)

add_library(ntirpc_lttng STATIC ${ntirpc_lttng_LIB_SRCS})
#add_sanitizers(ntirpc_lttng)

target_link_libraries(ntirpc_lttng
  ${LTTNG_LIBRARIES}
)

install(TARGETS ntirpc_lttng COMPONENT tracing DESTINATION ${LIB_INSTALL_DIR} )
