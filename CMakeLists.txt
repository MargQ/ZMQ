cmake_minimum_required(VERSION 3.15)
project(zmq_ex)

# Исходные файлы проекта
set(SERVER_SOURCES
    tests/server.c
)

set(CLIENT_SOURCES
    tests/client.c
)

set(CLIENT_SOURCES
    src/main.c
)

set(HEADERS
    include/header.h
)

# Найти библиотеку libzmq 
find_library(LIBZMQ_LIBRARY zmq)
find_path(LIBZMQ_INCLUDE_DIR zmq.h) 

# Найти библиотеку czmq 
find_library(CZMQ_LIBRARY czmq)
find_path(CZMQ_INCLUDE_DIR czmq.h)

# Путь до необходимых библиотек
include_directories(${PATH}/libzmq)
link_directories(${PATH}/libzmq)

include_directories(${PATH}/czmq)
link_directories(${PATH}/czmq)

# Добавление исполняемых файлов
add_executable(server ${SERVER_SOURCES})
add_executable(client ${CLIENT_SOURCES})
add_executable(main ${CLIENT_SOURCES})

# Линковка с библиотеками libzmq и czmq 
target_link_libraries(server ${LIBZMQ_LIBRARY} ${CZMQ_LIBRARY})
target_link_libraries(client ${LIBZMQ_LIBRARY} ${CZMQ_LIBRARY})
target_link_libraries(main ${LIBZMQ_LIBRARY} ${CZMQ_LIBRARY})

# Указание на папку, куда будут помещаться исполняемые файлы
set_target_properties(server PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/tests)
set_target_properties(client PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/tests)
set_target_properties(main PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/src)


# Файлы с исходниками на сайте zeromq.org там примеры client/server
# создать тут 2 бинарника. из клиента и сервера сделать 2 бинаринка,, псоле cmake и make.после этого скачть вайршарк и отслеить по пакетам и смотреть где передается хэлло а где ворд, сначала передаем хэлло, а в ответ ворлд