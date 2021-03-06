option (USE_INTERNAL_BOOST_LIBRARY "Use internal Boost library" ${NOT_UNBUNDLED})

if (USE_INTERNAL_BOOST_LIBRARY)
    set (LIBRARY_DIR ${ClickHouse_SOURCE_DIR}/contrib/boost)

    # filesystem

    set (SRCS_FILESYSTEM
        ${LIBRARY_DIR}/libs/filesystem/src/codecvt_error_category.cpp
        ${LIBRARY_DIR}/libs/filesystem/src/operations.cpp
        ${LIBRARY_DIR}/libs/filesystem/src/path_traits.cpp
        ${LIBRARY_DIR}/libs/filesystem/src/path.cpp
        ${LIBRARY_DIR}/libs/filesystem/src/portability.cpp
        ${LIBRARY_DIR}/libs/filesystem/src/unique_path.cpp
        ${LIBRARY_DIR}/libs/filesystem/src/utf8_codecvt_facet.cpp
        ${LIBRARY_DIR}/libs/filesystem/src/windows_file_codecvt.cpp
    )

    add_library (_boost_filesystem ${SRCS_FILESYSTEM})
    add_library (boost::filesystem ALIAS _boost_filesystem)
    target_include_directories (_boost_filesystem SYSTEM BEFORE PUBLIC ${LIBRARY_DIR})

    # headers-only

    add_library (_boost_headers_only INTERFACE)
    add_library (boost::headers_only ALIAS _boost_headers_only)
    target_include_directories (_boost_headers_only SYSTEM BEFORE INTERFACE ${LIBRARY_DIR})

    # iostreams

    set (SRCS_IOSTREAMS
        ${LIBRARY_DIR}/libs/iostreams/src/file_descriptor.cpp
        ${LIBRARY_DIR}/libs/iostreams/src/gzip.cpp
        ${LIBRARY_DIR}/libs/iostreams/src/mapped_file.cpp
        ${LIBRARY_DIR}/libs/iostreams/src/zlib.cpp
    )

    add_library (_boost_iostreams ${SRCS_IOSTREAMS})
    add_library (boost::iostreams ALIAS _boost_iostreams)
    target_include_directories (_boost_iostreams PRIVATE ${LIBRARY_DIR})
    target_link_libraries (_boost_iostreams PRIVATE zlib)

    # program_options

    set (SRCS_PROGRAM_OPTIONS
        ${LIBRARY_DIR}/libs/program_options/src/cmdline.cpp
        ${LIBRARY_DIR}/libs/program_options/src/config_file.cpp
        ${LIBRARY_DIR}/libs/program_options/src/convert.cpp
        ${LIBRARY_DIR}/libs/program_options/src/options_description.cpp
        ${LIBRARY_DIR}/libs/program_options/src/parsers.cpp
        ${LIBRARY_DIR}/libs/program_options/src/positional_options.cpp
        ${LIBRARY_DIR}/libs/program_options/src/split.cpp
        ${LIBRARY_DIR}/libs/program_options/src/utf8_codecvt_facet.cpp
        ${LIBRARY_DIR}/libs/program_options/src/value_semantic.cpp
        ${LIBRARY_DIR}/libs/program_options/src/variables_map.cpp
        ${LIBRARY_DIR}/libs/program_options/src/winmain.cpp
    )

    add_library (_boost_program_options ${SRCS_PROGRAM_OPTIONS})
    add_library (boost::program_options ALIAS _boost_program_options)
    target_include_directories (_boost_program_options SYSTEM BEFORE PUBLIC ${LIBRARY_DIR})

    # regex

    set (SRCS_REGEX
        ${LIBRARY_DIR}/libs/regex/src/c_regex_traits.cpp
        ${LIBRARY_DIR}/libs/regex/src/cpp_regex_traits.cpp
        ${LIBRARY_DIR}/libs/regex/src/cregex.cpp
        ${LIBRARY_DIR}/libs/regex/src/fileiter.cpp
        ${LIBRARY_DIR}/libs/regex/src/icu.cpp
        ${LIBRARY_DIR}/libs/regex/src/instances.cpp
        ${LIBRARY_DIR}/libs/regex/src/internals.hpp
        ${LIBRARY_DIR}/libs/regex/src/posix_api.cpp
        ${LIBRARY_DIR}/libs/regex/src/regex_debug.cpp
        ${LIBRARY_DIR}/libs/regex/src/regex_raw_buffer.cpp
        ${LIBRARY_DIR}/libs/regex/src/regex_traits_defaults.cpp
        ${LIBRARY_DIR}/libs/regex/src/regex.cpp
        ${LIBRARY_DIR}/libs/regex/src/static_mutex.cpp
        ${LIBRARY_DIR}/libs/regex/src/usinstances.cpp
        ${LIBRARY_DIR}/libs/regex/src/w32_regex_traits.cpp
        ${LIBRARY_DIR}/libs/regex/src/wc_regex_traits.cpp
        ${LIBRARY_DIR}/libs/regex/src/wide_posix_api.cpp
        ${LIBRARY_DIR}/libs/regex/src/winstances.cpp
    )

    add_library (_boost_regex ${SRCS_REGEX})
    add_library (boost::regex ALIAS _boost_regex)
    target_include_directories (_boost_regex PRIVATE ${LIBRARY_DIR})

    # system

    set (SRCS_SYSTEM
        ${LIBRARY_DIR}/libs/system/src/error_code.cpp
    )

    add_library (_boost_system ${SRCS_SYSTEM})
    add_library (boost::system ALIAS _boost_system)
    target_include_directories (_boost_system PRIVATE ${LIBRARY_DIR})
else ()
    message (FATAL_ERROR "TODO: external Boost library is not supported!")
endif ()
