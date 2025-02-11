make_acado_solver
======
This code is a part of https://github.com/ethz-asl/mav_control_rw.git. 

Author: Oskar Ljungqvist
Date: 2017-11-23
Description:

This folder contains code to automatically generate an MPC controller using ACADO toolkit.

The file **nmpc_solver_setup.cpp** is what defines the MPC controller and it is this you should change in order to change the controller. Then build/install it using the explanation below. As an example it easy to change the prediction horizon if that is prefered.

Prerequests: 
------
## Build 
* 下载安装acado, http://acado.github.io/install_linux.html.

* 增加环境变量，在 **~/.bashrc** 增加一句
`
source [你的路径]/ACADOtoolkit/build/acado_env.sh
`
加完这一句后，记得要 *source* 一下
```sh
source ~/.bashrc
```

* 构建求解器，在**nmpc_solver_setup.cpp**上构建你的求解器

* 生成求解器
```sh
cd [你的路径]/make_acado_solver
mkdir -p build
cd build
cmake ..
make 
cd ../solver
./nmpc_solver_setup
```
然后会在**solver/OCPexport**文件里生成你的解析器了

* 将生成的控制器拷贝到测试文件夹test中
```sh
cp -r ./OCPexport/ ../test/solver/
```

* 编译运行例程
```sh
cd ../test
mkdir build
cd build
cmake ..
make
./main
```
每次改动求解器后，要记得删除./test/solver/OCPexport，将新的./solver/OCPexport文件夹替换原来的文件夹

## Example 

[推车实例](http://docs.ros.org/en/indigo/api/acado/html/cgt_getting_started.html)
