# ROS 2 载具仿真实验

本组练习对应仓库中的地面载具、空域载具和水域载具示例，提供差速小车避障、纯追踪路径跟踪、无人机航点控制、禁飞区守护和水下 ROV 遥控响应五个项目。

源码目录：`src/chap9/`

| 实验 | 项目说明 |
|---|---|
| [小车激光雷达避障](chap9/rover_lidar_avoidance.md) | LaserScan 扇区判断与安全速度发布 |
| [小车纯追踪控制](chap9/rover_pure_pursuit.md) | 平面运动学模型跟踪椭圆参考路径 |
| [无人机航点跟踪](chap9/uav_waypoint_pid.md) | 三维位置误差生成限速速度向量 |
| [无人机禁飞区守护](chap9/uav_geofence_guard.md) | 对空间目标施加边界限幅 |
| [水下 ROV 六自由度响应](chap9/rov_6dof_teleop.md) | Twist 输入和阻尼运动学模型 |

项目图片均为 AI 生成的概念示意图，不能代替实际运行截图或仿真验证。
