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


## 练习二：检查并修改节点参数

参数用于配置节点行为。使用示例参数节点观察参数的声明、读取和更新。

```bash
source /opt/ros/humble/setup.bash
ros2 run demo_nodes_cpp parameter_blackboard --ros-args -r __node:=lesson_parameters
```

在另一个终端检查节点参数：

```bash
source /opt/ros/humble/setup.bash
ros2 param list /lesson_parameters
ros2 param get /lesson_parameters use_sim_time
ros2 param set /lesson_parameters lesson_rate 5
ros2 param get /lesson_parameters lesson_rate
```

如果节点未声明 `lesson_rate`，运行时设置可能被拒绝；这时先通过 `ros2 param list` 选择节点已声明的参数。参数服务仅影响当前节点实例，重启节点后是否保留取决于参数是否从文件加载。


## 练习三：用 launch 同时启动两个节点

Launch 文件能集中启动多个节点。新建 `talker_listener.launch.py`：

```python
from launch import LaunchDescription
from launch_ros.actions import Node


def generate_launch_description():
    return LaunchDescription([
        Node(
            package='demo_nodes_cpp',
            executable='talker',
            name='lesson_talker',
            output='screen',
        ),
        Node(
            package='demo_nodes_cpp',
            executable='listener',
            name='lesson_listener',
            output='screen',
        ),
    ])
```

在保存该文件的目录运行：

```bash
source /opt/ros/humble/setup.bash
ros2 launch ./talker_listener.launch.py
```

在另一个终端运行 `ros2 topic echo /chatter` 查看消息。launch 退出时会一起停止由它启动的节点。


## 练习四：观察 Action 的目标、反馈和结果

Action 适合需要较长时间执行并持续汇报进度的任务。使用 Fibonacci 示例观察客户端和服务端：

终端 1：

```bash
source /opt/ros/humble/setup.bash
ros2 run demo_nodes_cpp fibonacci_action_server
```

终端 2：

```bash
source /opt/ros/humble/setup.bash
ros2 action list
ros2 run demo_nodes_cpp fibonacci_action_client
```

客户端运行时会显示任务反馈，完成后返回最终序列。也可以用 `ros2 action info /fibonacci` 查看 Action 类型和服务端数量。若示例程序的 Action 名称不同，以 `ros2 action list` 输出为准。

