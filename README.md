# ROS 2 五个载具仿真实验

五个独立练习均使用 ROS 2 Humble Python 节点；其中纯追踪、无人机航点和 ROV 项目带有轻量运动学模型，激光避障与禁飞区守护通过标准 ROS 话题接入仿真器。

| 项目 | 载具 / 内容 | 主要接口 |
|---|---|---|
| `rover_lidar_avoidance` | 差速小车激光雷达反应式避障 | `/scan` → `/cmd_vel` |
| `rover_pure_pursuit` | 小车椭圆航线纯追踪 | `/odom`, `/cmd_vel`, `/reference_path_xy` |
| `uav_waypoint_pid` | 无人机三维航点跟踪 | `/uav/odom`, `/uav/cmd_vel` |
| `uav_geofence_guard` | 无人机空间围栏限幅 | `/uav/goal_raw` → `/uav/goal_safe` |
| `rov_6dof_teleop` | 水下 ROV 六自由度速度响应模型 | `/rov/cmd_vel` → `/rov/odom` |

## 环境

- Ubuntu 22.04、ROS 2 Humble、Python 3.10（推荐的官方组合）。
- 小车避障需有发布 `sensor_msgs/msg/LaserScan` 的仿真器；其他三个运动模型可独立启动。
- 所有项目均可 `python3 main.py` 启动；相应的 ROS 2 launch 文件位于 `launch/main.launch.py`。

## 运行方式

在每个项目目录的新终端中：

```bash
source /opt/ros/humble/setup.bash
python3 main.py
```

或启动 launch 文件：

```bash
ros2 launch ./launch/main.launch.py
```

输入与输出话题、调参方式和验证步骤见各项目的 `README.md`。本地运行结果尚未采集，项目图为 AI 生成的概念示意图，不代表真实仿真截图。

> 代码和文档由 OpenAI Codex 协助整理；提交者应在自己的 ROS 环境中复核并完成运行验证。
