# Rust_DPDK
This project is a Rust package library for DPDK 20.11.By encapsulating the DPDK library written in C language, external Rust applications can directly use the functions in the DPDK library through the Rust API.This project currently only encapsulates about 200 commonly used APIs of DPDK, and the functions are still very imperfect. Users can add the DPDK functions they need according to the method of this project.
## preparation
Configure DPDK environment

```bash
cd dpdk
sudo meson build
cd build
sudo ninja install
```
Set DPDK hugepages (runtime)

```bash
sudo chmod 777 /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
echo 1024 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```
Load the linux driver, see in detail:
http://doc.dpdk.org/guides/linux_gsg/linux_drivers.html。

Bind the network port

```bash
cd dpdk/usertools
//check the network card net_cd
ifconfig
sudo dpdk-devbind.py --bind=net_cd
//check the bindings
sudo dpdk-devbind.py --status
```
## Running Result
Run the Helloworld program , which is in /dpdk/examples/helloworld

![在这里插入图片描述](https://img-blog.csdnimg.cn/cf2dc2d3ecc445c183d339f04d82212f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6ZmI57ut5YW0,size_20,color_FFFFFF,t_70,g_se,x_16)

sudo cargo run,run DPDK application rewritten in Rust language

![在这里插入图片描述](https://img-blog.csdnimg.cn/b5e33bc9b7a94130809f4a349a773719.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6ZmI57ut5YW0,size_20,color_FFFFFF,t_70,g_se,x_16)


