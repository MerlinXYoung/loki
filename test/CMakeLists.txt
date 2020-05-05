
include_directories(${PROJECT_SOURCE_DIR}/include/loki)
list(APPEND CMAKE_CXX_FLAGS -fpermissive )

MACRO(SUBDIRLIST result curdir)


 FILE(GLOB children RELATIVE ${curdir} ${curdir}/*)


 SET(dirlist"")


 FOREACH(child ${children})


 IF(IS_DIRECTORY ${curdir}/${child})


 LIST(APPEND dirlist ${child})


 ENDIF()


 ENDFOREACH()


 SET(${result} ${dirlist})


ENDMACRO()

SUBDIRLIST(SUBDIRS ${CMAKE_CURRENT_SOURCE_DIR})

# message(STATUS ${SUBDIRS} )

FOREACH(subdir ${SUBDIRS})

    
    set(TGT ${subdir})
    file(GLOB TGT_SRCS "${subdir}/*.cpp")

    add_executable(${TGT} ${TGT_SRCS})
    target_link_libraries(${TGT} Loki Threads::Threads)

    add_test(testrun_${TGT} ${TGT})

ENDFOREACH()