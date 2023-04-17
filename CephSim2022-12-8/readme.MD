## Introduce
This project is a discrete event simulator based on NS3 simulation platform. The main purpose is to simulate Ceph and obtain latency data.

## Environment
CPU: Intel(R) Xeon(R) CPU E5-2620 v4 @ 2.10GHz

OS: Ubuntu：20.04 Server
(Linux version 5.4.0-146-generic (buildd@lcy02-amd64-026) (gcc version 9.4.0 (Ubuntu 9.4.0-1ubuntu1~20.04.1)))
 

NS3：3.35

## Install NS-3
下面安装方法是自己经测试可以完成安装的脚本，如果出问题可以自行在官网查找安装教程 https://www.nsnam.org/documentation/

```SHELL
1. git clone https://gitlab.com/nsnam/bake
2. 
export BAKE_HOME=`pwd`/bake 
export PATH=$PATH:$BAKE_HOME
export PYTHONPATH=$PYTHONPATH:$BAKE_HOME
3. bake.py check  
4. bake.py configure -e ns-3.35
5. bake.py show   
6. bake.py deploy
7.
cd source/ns-3.35
./test.py #test
8. ./waf --run hello-simulator #hello world
9. rm -rf scratch/* # delete hello world code
10. move the CephSim2022-12-8.zip to folder ns-3.35/scratch
11. unzip CephSim2022-12-8.zip
```

## Run
- 将代码文件夹（CephSim）放在NS3的scratch路径下（需要事先安装好NS3）。

以下命令在```source/ns-3.35```目录下运行 

- 创建存放结果的目录
``` shell 
mkdir cephSimResult
cd cephSimResult
mkdir latency  
mkdir packetTrace
mkdir serverTrace
# mkdir cluster_map_copy #if just run code ,no need 
```  

-  运行仿真 （回到ns3.35目录下）
```shell
cd ..  # back to the source/ns-3.35
# ./waf --run scratch/CephSim/CephSim #for the first code
./waf --run scratch/CephSim2022-12-8/CephSim2022-12-8 # for the lastest code
```
## Result

- cephSimResult/01_latencyPreview.csv 每一轮运行的延迟，SLA总体统计信息
- cephSimResult/waitTime.csv 每个节点的等待时间，用以动态图神经网络模型的输入
- cephSimResult/latency/ 文件夹中内容是每轮运行每个请求的延迟记录
- cephSimResult/packetTrace 文件夹中内容是每轮每个请求的trace，信息内容见表头
- cephSimResult/serverTrace 文件夹内容是每个OSD节点的请求处理trace，用来查看后端调度方案的有效性和debug

## Key Configurations
The file is ```scratch/CephSim2022-12-8/cephSimDefine.h```

相关参数都有注释，具体和运行有关的主要是下面这两个
```
#define RENUM 16000              //请求数量
#define RUN_NUM 3    //循环次数
```


## Note
* 因项目编译问题 函数实现直接写在了.h文件中

* ns-3不是ns-2的向后兼容扩展；这是一个新的模拟器。这两个模拟器都是用 C++ 编写的，但 ns-3是一个不支持ns-2 API 的新模拟器。

* 项目位于是自己定义的文件夹下，编译后可执行文件名会默认变成和文件夹名称一样 （自己二次开发后，修改文件夹名字后需要修改运行脚本）所以运行脚本如下。（如果出现一堆爆红一般是没找到对应的build的可运行文件，可以去翻看NS3-3XX/build/scratch目录下是否成功生成了可执行文件。）
```
./waf --run scratch/文件夹名/文件夹名
```

## NS3 官方文档

- 起始页 https://www.nsnam.org/documentation/

- API查询 https://www.nsnam.org/doxygen/index.html

- 初始教程 https://www.nsnam.org/docs/release/3.36/tutorial/html/index.html

- 关键概念 https://www.nsnam.org/docs/release/3.36/tutorial/html/conceptual-overview.html#key-abstractions
