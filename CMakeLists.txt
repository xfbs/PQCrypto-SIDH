cmake_minimum_required(VERSION 3.10)
project(sidh
    VERSION 3.4
    LANGUAGES C)

add_definitions(-D_AMD64_ -D__NIX__ -O3 -D_GENERIC_)

# util libraries
add_library(aes tests/aes/aes.c)
add_library(sidh src/random/random.c src/sha3/fips202.c)

# implementations
add_library(sidh434
    src/P434/generic/fp_generic.c
    src/P434/P434.c)
target_link_libraries(sidh434 sidh)

add_library(sidh503
    src/P503/generic/fp_generic.c
    src/P503/P503.c)
target_link_libraries(sidh503 sidh)

add_library(sidh610
    src/P610/generic/fp_generic.c
    src/P610/P610.c)
target_link_libraries(sidh610 sidh)

add_library(sidh751
    src/P751/generic/fp_generic.c
    src/P751/P751.c)
target_link_libraries(sidh751 sidh)

# implementations (compressed)
# TODO

# arith tests
add_library(sidhtests tests/test_extras.c)
add_executable(arith-tests-p434 tests/arith_tests-p434.c)
target_link_libraries(arith-tests-p434 sidhtests sidh434)

add_executable(arith-tests-p503 tests/arith_tests-p503.c)
target_link_libraries(arith-tests-p503 sidhtests sidh503)

add_executable(arith-tests-p610 tests/arith_tests-p610.c)
target_link_libraries(arith-tests-p610 sidhtests sidh610)

add_executable(arith-tests-p751 tests/arith_tests-p751.c)
target_link_libraries(arith-tests-p751 sidhtests sidh751)

# sidh tests
add_executable(test-sidh434 tests/test_SIDHp434.c)
target_link_libraries(test-sidh434 sidhtests sidh434)

add_executable(test-sidh503 tests/test_SIDHp503.c)
target_link_libraries(test-sidh503 sidhtests sidh503)

add_executable(test-sidh610 tests/test_SIDHp610.c)
target_link_libraries(test-sidh610 sidhtests sidh610)

add_executable(test-sidh751 tests/test_SIDHp751.c)
target_link_libraries(test-sidh751 sidhtests sidh751)

# sike tests
add_executable(test-sike434 tests/test_SIKEp434.c)
target_link_libraries(test-sike434 sidhtests sidh434)

add_executable(test-sike503 tests/test_SIKEp503.c)
target_link_libraries(test-sike503 sidhtests sidh503)

add_executable(test-sike610 tests/test_SIKEp610.c)
target_link_libraries(test-sike610 sidhtests sidh610)

add_executable(test-sike751 tests/test_SIKEp751.c)
target_link_libraries(test-sike751 sidhtests sidh751)

enable_testing()
add_test(NAME "arith434" COMMAND arith-tests-p434)
add_test(NAME "arith503" COMMAND arith-tests-p503)
add_test(NAME "arith610" COMMAND arith-tests-p610)
add_test(NAME "arith751" COMMAND arith-tests-p751)
add_test(NAME "sidh434" COMMAND test-sidh434)
add_test(NAME "sidh503" COMMAND test-sidh503)
add_test(NAME "sidh610" COMMAND test-sidh610)
add_test(NAME "sidh751" COMMAND test-sidh751)
add_test(NAME "sike434" COMMAND test-sike434)
add_test(NAME "sike503" COMMAND test-sike503)
add_test(NAME "sike610" COMMAND test-sike610)
add_test(NAME "sike751" COMMAND test-sike751)
