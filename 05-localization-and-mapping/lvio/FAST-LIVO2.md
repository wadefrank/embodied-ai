# 简介

GitHub: [https://github.com/hku-mars/fast-livo2](https://github.com/hku-mars/fast-livo2)

论文：[https://arxiv.org/abs/2408.14035](https://arxiv.org/abs/2408.14035)


# 整体架构

```
 Camera                   LiDAR                  IMU
   │                        │                     │
   ▼                        ▼                     ▼
图像预处理                点云预处理             IMU状态传播
(去畸变/灰度化/金字塔) （解析/过滤/时间排序）   (状态预测、协方差传播) 
   │                        │                     │
   │                        └────────┬────────────┘
   │                                 ▼
   │                           点云运动补偿（运动畸变去除）
   │                                 │
   │                                 ▼
   │                             体素降采样
   │                                 │
   │                                 ▼
   │        LiDAR Measurement Model(地图邻域搜索 + 局部平面拟合 + 点到平面残差)
   │                                 │
   │                                 ▼
   │                       LiDAR Iterated ESIKF
   │                                 │
   │                                 ▼
   │                   统一Visual-LiDAR体素地图：几何属性更新
   │                                 │
   └─────────────────────────────────┤
                                     ▼
                         Visual Measurement Model
				                     │    
				                     ▼
			 可见性判断 + Raycasting + 选择参考Patch + 地图点投影
					                 │
								     ▼
	            平面先验Patch Warp + 光度残差 + 曝光参数估计
                                     │
                                     ▼
                           Visual Iterated ESIKF
                                     │
                                     ▼
                统一Visual-LiDAR体素地图：视觉属性/参考Patch动态更新
                                     │
                                     ▼
               发布 Odom / Path / TF / PointCloud / Colored Map
```