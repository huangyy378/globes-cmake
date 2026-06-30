# example programs
add_executable(example-tour example-tour.c)
add_executable(example1 example1.c myio.c)
add_executable(example2 example2.c myio.c)
add_executable(example3 example3.c myio.c)
add_executable(example4 example4.c myio.c)
add_executable(example5 example5.c myio.c)
add_executable(example6 example6.c myio.c)

set(LINK_LIBS 
    globeslib          # GLoBES
    ${GSL_LIB}         # libgsl.so
    ${GSLCBLAS_LIB}    # libgslcblas.so
    ${M_LIB}           # libm.so
)

foreach(target_name example-tour example1 example2 example3 example4 example5 example6)
    target_link_libraries(${target_name} 
    globeslib 
    ${GSL_LIB} 
    ${GSLCBLAS_LIB} 
    ${M_LIB}
    -Wl,--no-as-needed
)
    target_include_directories(${target_name} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
endforeach()

file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/
     DESTINATION ${CMAKE_CURRENT_BINARY_DIR}
     FILES_MATCHING PATTERN "*.glb" PATTERN "*.dat")

install(FILES
    NFstandard.glb
    D-Chooz_far.glb
    D-Chooz_near.glb
    Reactor1.glb
    Reactor.dat
    XCC.dat
    XNC.dat
    XCCreactor.dat
    DESTINATION share/globes/examples
)
