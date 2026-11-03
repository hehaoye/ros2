# ROS2 

以下测试都是基于 Ubuntu 20.04 ROS Humble

```shell
source /opt/ros/humble/setup.bash
ros2 topic pub /chatter std_msgs/String "data: Hello world"
# 重新打开一个终端
ros2 topic echo /chatter
```

![](../img/ros/ros2_pub_echo.png)


## 运行 talker 和 listener 示例

```shell
ros2 run demo_nodes_cpp talker
ros2 run demo_nodes_cpp listener
```

![](../img/ros/ros2_talker_listener.png)


## 新增：载具仿真实验项目

本组提供五个 ROS 2 小型载具控制项目，包含差速小车激光雷达避障、纯追踪路径跟踪、无人机三维航点跟踪、禁飞区守护和水下 ROV 六自由度响应模型。详见[项目总览](../chap9_projects.md)。
