macro(ncnn_add_example name)
    add_executable(${name} ${name}.cpp)
    target_include_directories(${name} PRIVATE ${OpenCV_INCLUDE_DIRS})
    target_link_libraries(${name} PRIVATE ncnn ${OpenCV_LIBS})

    # add test to a virtual project group
    set_property(TARGET ${name} PROPERTY FOLDER "examples")
endmacro()

find_package(OpenCV QUIET COMPONENTS opencv_world)
# for opencv 2.4 on ubuntu 16.04, there is no opencv_world but OpenCV_FOUND will be TRUE
if("${OpenCV_LIBS}" STREQUAL "")
    set(OpenCV_FOUND FALSE)
endif()
if(NOT OpenCV_FOUND)
    find_package(OpenCV QUIET COMPONENTS core highgui imgproc imgcodecs videoio)
endif()
if(NOT OpenCV_FOUND)
    find_package(OpenCV QUIET COMPONENTS core highgui imgproc)
endif()

if(NOT OpenCV_FOUND)
    message(WARNING "OpenCV not found, examples won't be built")
elseif(NOT NCNN_PIXEL)
    message(WARNING "NCNN_PIXEL not enabled, examples won't be built")
else()
    message(STATUS "OpenCV library: ${OpenCV_INSTALL_PATH}")
    message(STATUS "    version: ${OpenCV_VERSION}")
    message(STATUS "    libraries: ${OpenCV_LIBS}")
    message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

    if(${OpenCV_VERSION_MAJOR} GREATER 3)
        set(CMAKE_CXX_STANDARD 11)
    endif()
    include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../src)
    include_directories(${CMAKE_CURRENT_BINARY_DIR}/../src)

    #ncnn_add_example(squeezenet)
    #ncnn_add_example(squeezenet_c_api)
    #ncnn_add_example(fasterrcnn)
    #ncnn_add_example(rfcn)
    #ncnn_add_example(yolov2)
    #ncnn_add_example(yolov3)
    #ncnn_add_example(yolov4)
    #ncnn_add_example(yolov5)
    #ncnn_add_example(mobilenetv2ssdlite)
    #ncnn_add_example(mobilenetssd)
    #ncnn_add_example(squeezenetssd)
    #ncnn_add_example(shufflenetv2)
    #ncnn_add_example(peleenetssd_seg)
    #ncnn_add_example(simplepose)
    #ncnn_add_example(retinaface)
    #ncnn_add_example(yolact)
    #ncnn_add_example(nanodet)
endif()
