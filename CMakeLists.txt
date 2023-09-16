cmake_minimum_required(VERSION 3.13.4)
project(cxx-zygisk)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS off)
set(CMAKE_VISIBILITY_INLINES_HIDDEN on)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)

set(libcxx_includes
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/src
)

set(libcxx_sources
    src/algorithm.cpp
    src/any.cpp
    src/atomic.cpp
    src/barrier.cpp
    src/bind.cpp
    src/charconv.cpp
    src/chrono.cpp
    src/condition_variable.cpp
    src/condition_variable_destructor.cpp
    src/debug.cpp
    src/exception.cpp
    src/filesystem/directory_iterator.cpp
    src/filesystem/int128_builtins.cpp
    src/filesystem/operations.cpp
    src/functional.cpp
    src/future.cpp
    src/hash.cpp
    src/ios.cpp
    src/ios.instantiations.cpp
    src/iostream.cpp
    src/legacy_debug_handler.cpp
    src/legacy_pointer_safety.cpp
    src/locale.cpp
    src/memory.cpp
    src/mutex.cpp
    src/mutex_destructor.cpp
    src/new.cpp
    src/optional.cpp
    src/random_shuffle.cpp
    src/random.cpp
    src/regex.cpp
    src/shared_mutex.cpp
    src/stdexcept.cpp
    src/string.cpp
    src/strstream.cpp
    src/system_error.cpp
    src/thread.cpp
    src/typeinfo.cpp
    src/utility.cpp
    src/valarray.cpp
    src/variant.cpp
    src/vector.cpp
    src/verbose_abort.cpp
)

set(libcxx_cxxflags "-std=c++20 -fvisibility-global-new-delete-hidden -fvisibility=hidden -fvisibility-inlines-hidden -DLIBCXX_BUILDING_LIBCXXABI -D_LIBCPP_NO_EXCEPTIONS -D_LIBCPP_NO_RTTI -D_LIBCPP_BUILDING_LIBRARY -D_LIBCPP_DISABLE_VISIBILITY_ANNOTATIONS -D__STDC_FORMAT_MACROS")

set(libcxxabi_src_files
    src/abi/abort_message.cpp
    src/abi/cxa_aux_runtime.cpp
    src/abi/cxa_default_handlers.cpp
    src/abi/cxa_exception_storage.cpp
    src/abi/cxa_guard.cpp
    src/abi/cxa_handlers.cpp
    src/abi/cxa_noexception.cpp
    src/abi/cxa_thread_atexit.cpp
    src/abi/cxa_vector.cpp
    src/abi/cxa_virtual.cpp
    src/abi/stdlib_exception.cpp
    src/abi/stdlib_new_delete.cpp
    src/abi/stdlib_stdexcept.cpp
    src/abi/stdlib_typeinfo.cpp
)

set(libcxxabi_includes
    include
    include/abi
)

set(libcxxabi_cflags
    -D__STDC_FORMAT_MACROS
)

set(libcxxabi_cppflags "-D_LIBCXXABI_NO_EXCEPTIONS -Wno-macro-redefined -Wno-unknown-attributes -DHAS_THREAD_LOCAL"
)

include_directories(${libcxx_includes})
include_directories(${libcxxabi_includes})
set(CMAKE_CXX_FLAGS "${libcxx_cxxflags} ${libcxxabi_cppflags} -ffunction-sections -fdata-sections ${CMAKE_CXX_FLAGS}")

add_library(cxx-zygisk STATIC ${libcxx_sources} ${libcxxabi_src_files})
