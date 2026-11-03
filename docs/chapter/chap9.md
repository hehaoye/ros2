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

## 练习一：使用服务完成整数加法

服务适合请求与响应式交互。本练习使用 ROS 2 自带的 `example_interfaces/srv/AddTwoInts`，客户端发送两个整数，服务端返回和。

终端 1 启动服务端：

```bash
source /opt/ros/humble/setup.bash
ros2 run demo_nodes_cpp add_two_ints_server
```

终端 2 调用服务：

```bash
source /opt/ros/humble/setup.bash
ros2 service list
ros2 service type /add_two_ints
ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts "{a: 17, b: 25}"
```

预期响应中 `sum` 为 `42`。若服务名不同，先用 `ros2 service list` 查看当前服务名，再将其替换到调用命令中。按 `Ctrl+C` 停止服务端。

