aux_source_directory(. SRC_LIST)
# 指定生成可执行文件
add_executable(ThreadPool ${SRC_LIST})
# 指定可执行文件链接时需要的库文件
add_library(threadpool SHARED ${SRC_LIST})

target_link_libraries(ThreadPool pthread)
target_link_libraries(threadpool pthread)