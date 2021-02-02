if (APPLE)
    # If we're on OS X check for Homebrew's copy of OpenSSL instead of Apple's
    if (NOT OpenSSL_DIR)
        find_program(HOMEBREW brew)
        if (HOMEBREW STREQUAL "HOMEBREW-NOTFOUND")
            message(WARNING "Homebrew not found: not using Homebrew's OpenSSL")
            if (NOT OPENSSL_ROOT_DIR)
                message(WARNING "Use -DOPENSSL_ROOT_DIR for non-Apple OpenSSL")
            endif()
        else()
            execute_process(COMMAND brew --prefix openssl
                OUTPUT_VARIABLE OPENSSL_ROOT_DIR
                OUTPUT_STRIP_TRAILING_WHITESPACE)
        endif()
    endif()
endif()

find_package(OpenSSL)
find_package(gRPC)

