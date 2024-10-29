


# 编译LAME库


设备录制声音时，保存成.wav格式时，size太大了。5s音频保存的size接近900K！故保存成mp3压缩格式，中等音质大概70K。保存有损的mp3需要用到LAME库，编译下。

参考[博文](https://blog.csdn.net/u012150124/article/details/82053206)

## 下载LAME源码

[src_code](http://sourceforge.net/projects/lame/files/lame/3.99/lame-3.99.5.tar.gz)
解压后进入主目录。




## 编译

1. 复制源码

```shell
mkdir src
cd src 
mkdir cpp build
cd cpp
cp -r ../../libmp3lame/*.c ./
cp -r ../../libmp3lame/*.h ./
cp -r ../../libmp3lame/vector/*.c ./
cp -r ../../libmp3lame/vector/*.h ./
cp ../../include/lame.h ./
```


2. 编写CMakelist.txt
vim CMakelist.txt

```cmake
cmake_minimum_required(VERSION 3.0)
project(LAME)
include_directories(${PROJECT_SOURCE_DIR})
file(GLOB SRC_LIST "${CMAKE_CURRENT_SOURCE_DIR}/*.c")
add_library(lame SHARED ${SRC_LIST})
```

3. 解决报错

- 将 util.h 文件的 574 行的”extern ieee754_float32_t fast_log2(ieee754_float32_t x);” 替换为 “extern float fast_log2(float x);”
- bcopy，index报错: 全局搜索bcopy，index。这些功能现在标准的C++弃用，注释掉。 之后重新编译下。