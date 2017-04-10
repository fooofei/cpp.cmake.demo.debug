
## cmake debug release 差别

需要编译的二进制为 Debug ，则：
```
cmake -DCMAKE_BUILD_TYPE=Debug <path>
make
```

需要编译的二进制为 Release ，则：
```
cmake -DCMAKE_BUILD_TYPE=Release <path>
make
```

就以上这么操作，Debug Release 的区分是在 cmake 阶段进行的，不是在 make 阶段。

## 观察生成文件的区别

使用 BeyondCompare 对比发现，区别在 cmake 生成的 `CMakeFiles\test.dir\flags.make` 和 `CMakeFiles\test.dir\link.txt` 这两个文件的区别。

模式\文件|flags.make 文件 | link.txt 文件
---------|----------------|----------------
default  | CXX_FLAGS  =   | /usr/bin/c++  ...
Debug    | CXX_FLAGS = -g | /usr/bin/c++   -g  ...
Release  | CXX_FLAGS = -O3 -DNDEBUG   | /usr/bin/c++   -O3 -DNDEBUG  ...

