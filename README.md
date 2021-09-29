# Rust_DPDK
本项目是一个针对DPDK 20.11的Rust封装库，通过对C语言编写的DPDK库进行封装，使得外部Rust应用程序能够直接通过封装得到的Rust API访问DPDK库中的函数，从而实现用Rust语言编写DPDK应用程序。本项目目前只对DPDK的约200个常用API进行了封装，功能依然很不完善，使用者可以根据，本项目的封装方法按需添加自己需要的DPDK函数。
## preparation
要使用本库，首先要配置DPDK环境

```bash
cd dpdk
sudo meson build
cd build
sudo ninja install
```
设置DPDK大页(运行时)

```bash
sudo chmod 777 /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
echo 1024 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```
加载linux driver，详细可见：http://doc.dpdk.org/guides/linux_gsg/linux_drivers.html。

绑定网络端口

```bash
cd dpdk/usertools
//check the network card net_cd
ifconfig
sudo dpdk-devbind.py --bind=net_cd
//check the bindings
sudo dpdk-devbind.py --status
```
## Running Result
运行DPDK自带的Helloworld程序

![在这里插入图片描述](https://img-blog.csdnimg.cn/cf2dc2d3ecc445c183d339f04d82212f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6ZmI57ut5YW0,size_20,color_FFFFFF,t_70,g_se,x_16)
sudo cargo run运行Rust语言改写的DPDK应用程序

![在这里插入图片描述](https://img-blog.csdnimg.cn/b5e33bc9b7a94130809f4a349a773719.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6ZmI57ut5YW0,size_20,color_FFFFFF,t_70,g_se,x_16)


