Example about how to install a dynamic linked library with CMake

```shell
mkdir build
cd build
cmake ..
cmake --build . --parallel
cmake --install . --prefix "Install_path/usr"
```