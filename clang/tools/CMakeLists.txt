create_subdirectory_options(CLANG TOOL)

add_clang_subdirectory(diagtool)
add_clang_subdirectory(driver)
add_clang_subdirectory(apinotes-test)
if(CLANG_ENABLE_CIR)
  add_clang_subdirectory(cir-opt)
  add_clang_subdirectory(cir-translate)
  add_clang_subdirectory(cir-lsp-server)
endif()
add_clang_subdirectory(clang-diff)
add_clang_subdirectory(clang-format)
add_clang_subdirectory(clang-fuzzer)
add_clang_subdirectory(clang-import-test)
add_clang_subdirectory(clang-linker-wrapper)
add_clang_subdirectory(clang-nvlink-wrapper)
add_clang_subdirectory(clang-offload-packager)
add_clang_subdirectory(clang-offload-bundler)
add_clang_subdirectory(clang-scan-deps)
add_clang_subdirectory(clang-sycl-linker)
add_clang_subdirectory(clang-installapi)
if(HAVE_CLANG_REPL_SUPPORT)
  add_clang_subdirectory(clang-repl)
endif()

add_clang_subdirectory(c-index-test)

add_clang_subdirectory(clang-refactor)
# For MinGW/Cygwin we only enable shared library if LLVM_LINK_LLVM_DYLIB=ON.
# Without that option resulting library is too close to 2^16 DLL exports limit.
if((UNIX AND NOT CYGWIN) OR (MSVC AND LLVM_BUILD_LLVM_DYLIB_VIS) OR
  ((MINGW OR CYGWIN) AND LLVM_LINK_LLVM_DYLIB))
  add_clang_subdirectory(clang-shlib)
endif()

if(CLANG_ENABLE_STATIC_ANALYZER)
  add_clang_subdirectory(clang-check)
  add_clang_subdirectory(clang-extdef-mapping)
  add_clang_subdirectory(scan-build)
  add_clang_subdirectory(scan-build-py)
  add_clang_subdirectory(scan-view)
endif()

# We support checking out the clang-tools-extra repository into the 'extra'
# subdirectory. It contains tools developed as part of the Clang/LLVM project
# on top of the Clang tooling platform. We keep them in a separate repository
# to keep the primary Clang repository small and focused.
# It also may be included by LLVM_EXTERNAL_CLANG_TOOLS_EXTRA_SOURCE_DIR.
add_llvm_external_project(clang-tools-extra extra)

# libclang may require clang-tidy in clang-tools-extra.
add_clang_subdirectory(libclang)

add_clang_subdirectory(offload-arch)
add_subdirectory(identify-scope)
