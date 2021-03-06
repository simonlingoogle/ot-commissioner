#
#  Copyright (c) 2019, The OpenThread Authors.
#  All rights reserved.
#
#  Redistribution and use in source and binary forms, with or without
#  modification, are permitted provided that the following conditions are met:
#  1. Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
#  2. Redistributions in binary form must reproduce the above copyright
#     notice, this list of conditions and the following disclaimer in the
#     documentation and/or other materials provided with the distribution.
#  3. Neither the name of the copyright holder nor the
#     names of its contributors may be used to endorse or promote products
#     derived from this software without specific prior written permission.
#
#  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
#  AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
#  IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
#  ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
#  LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
#  CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
#  SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
#  INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
#  CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
#  ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
#  POSSIBILITY OF SUCH DAMAGE.
#

add_library(commissioner STATIC
    openthread/bloom_filter.cpp
    openthread/crc16.cpp
    openthread/pbkdf2_cmac.cpp
    openthread/random.cpp
    openthread/sha256.cpp
    cbor.cpp
    coap.cpp
    commissioner_impl.cpp
    commissioner_safe.cpp
    commissioning_session.cpp
    cose.cpp
    dtls.cpp
    error.cpp
    logging.cpp
    multicast_dns.cpp
    network_data.cpp
    socket.cpp
    tlv.cpp
    token_manager.cpp
    udp_proxy.cpp)

target_link_libraries(commissioner PRIVATE
    cose
    mdns
    mbedtls
    pthread
    fmt::fmt
    event_core_static
    event_pthreads_static
    commissioner-common)

target_include_directories(commissioner PUBLIC ${PROJECT_SOURCE_DIR}/include)
target_include_directories(commissioner PRIVATE
    ${PROJECT_SOURCE_DIR}/third_party/mbedtls/repo/include
    ${PROJECT_SOURCE_DIR}/third_party/libevent/repo/include
    ${PROJECT_BINARY_DIR}/third_party/libevent/repo/include)

install(TARGETS commissioner
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)

install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/commissioner
        DESTINATION include)
