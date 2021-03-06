configure_file(${CMAKE_CURRENT_SOURCE_DIR}/include/eotio/chain/core_symbol.hpp.in ${CMAKE_CURRENT_SOURCE_DIR}/include/eotio/chain/core_symbol.hpp)

file(GLOB HEADERS "include/eotio/chain/*.hpp" "include/eotio/chain/contracts/*.hpp")

## SORT .cpp by most likely to change / break compile
add_library( eotio_chain
             merkle.cpp
             name.cpp
             transaction.cpp
             block_header.cpp
             block_header_state.cpp
             block_state.cpp
             fork_database.cpp
             controller.cpp
             authorization_manager.cpp
             resource_limits.cpp
             block_log.cpp
             genesis_state.cpp
             transaction_context.cpp
             eotio_contract.cpp
             eotio_contract_abi.cpp

#             chain_config.cpp
#             block_trace.cpp
              wast_to_wasm.cpp
              wasm_interface.cpp
              wasm_eotio_validation.cpp
              wasm_eotio_injection.cpp
              apply_context.cpp
              abi_serializer.cpp
              asset.cpp

             webassembly/wavm.cpp
             webassembly/binaryen.cpp

#             get_config.cpp
#             global_property_object.cpp
#
#             contracts/chain_initializer.cpp


#             transaction_metadata.cpp
             ${HEADERS}
             )

target_link_libraries( eotio_chain eot_utilities fc chainbase Logging IR WAST WASM Runtime
      wasm asmjs passes cfg ast emscripten-optimizer support softfloat builtins
                     )
target_include_directories( eotio_chain
                            PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include" "${CMAKE_CURRENT_BINARY_DIR}/include"
                                   "${CMAKE_CURRENT_SOURCE_DIR}/../wasm-jit/Include"
                                   "${CMAKE_CURRENT_SOURCE_DIR}/../../externals/binaryen/src"
                            )

#if(MSVC)
#  set_source_files_properties( db_init.cpp db_block.cpp database.cpp block_log.cpp PROPERTIES COMPILE_FLAGS "/bigobj" )
#endif(MSVC)
