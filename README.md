# luckfox_pico_rga
luckfox-pico RGA 使用例程

## 实验平台
+ luckfox-pico pro （luckfox-pico mini/plus DMA 申请失败问题待解决）

## 编译
```
cd luckfox_pico_rga
mkdir build
cd build
cmake ..
make && make install
```

## 运行
将编译生成的 `luckfox_rga_demo` 拷贝到开发板上，进入 `luckfox_rga_demo/bin` 执行
```
./luckfox_rga_demo
```
在 `luckfox_rga_demo/pic` 中会生成输入图像 `in0w1280-h720-rgba8888.bin` 左右翻转后的图像 `out0w1280-h720-rgba8888.bin`。
可以使用 `YUView` 工具进行观察。
