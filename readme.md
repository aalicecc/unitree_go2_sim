# 宇树go2仿真

详细步骤请参考：[unitree_guide](https://support.unitree.com/home/zh/Algorithm_Practice/quickstart)

## 快速开始

1. 安装LCM库：

```bash
sudo apt install liblcm-dev
```

2. 安装其他依赖

```bash
sudo apt-get install build-essential autoconf automake autopoint libglib2.0-dev libtool openjdk-8-jdk python-dev
```

3. 拉取仓库

```bash
git clone --recurse-submodules https://github.com/aalicecc/unitree_go2_sim.git
```

```bash
cd unitree_go2_sim/unitree_ros
git submodule update --remote --recursive
```

```bash
cd unitree_ros_to_real/
git submodule update --remote --recursive
```

4. 编译工作空间
```bash
catkin_make
```

## 使用说明

开始使用 unitree_guide 总共分为两步。

1. 运行 Gazebo 仿真环境:

在同一个终端中，执行下列命令：

```bash
source devel/setup.bash
```

然后执行下列命令来打开 Gazebo 仿真环境：

```bash
roslaunch unitree_guide gazeboSim.launch
```

2. 启动控制器:

打开另外一个终端，并切换至相同路径下(本文假设该路经为~/catkin_ws )，然后输入下列命令以启动控制器：

```bash
sudo ./devel/lib/unitree_guide/junior_ctrl
```

然后控制器终端中按下 "2"。此时在 Gazebo 环境中的机器人会站起来，同时终端会显示 “Switched from passive to fixed stand”。

接下来同样选中该终端，然后按下键盘上的 “4” 键，在终端显示“按下键盘上的 “Switched from fixed stand to trotting”内容后，连续按两下键盘上的 “w” 键，机器人即可缓慢向前运动，按下键盘上的 “空格” 键，机器人则会停下来。

在仿真环境中，按下键盘上的 W A S D 键 分别控制机器人 前进 左平移 后腿 右平移。按下键盘上的 J L 键 分别控制机器人 左转 右转。

## 常见问题

1. sudo devel/lib/unitree_guide/junior_ctrl 时出错

用户在使用命令 sudo ./devel/lib/unitree_guide/junior_ctrl，启动控制器时，终端可能会提示某些动态库 so 文件找不到。

解决方法：打开一个终端，使用任一个文本编辑器打开动态库路径配置文件 (此处以 vim 为例)

```bash
sudo vim /etc/ld.so.conf
```

添加以下路径：

```bash
/opt/ros/noetic/lib
/usr/local/lib
```

在编辑并保存后，在终端输入下列命令以立即生效相关设置。然后再次启动控制器即可解决问题。

```bash
sudo ldconfig
```