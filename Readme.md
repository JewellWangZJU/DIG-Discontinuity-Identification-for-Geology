# DIG：基于AI视觉模型的岩体三维结构面识别工具

## 项目简介

DIG（Discontinuity Identification for Geology）是一种结合AI视觉大模型与运动恢复结构（Structure-from-Motion, SfM）技术的三维结构面识别系统，支持从图像自动提取岩体结构面信息，并实现二维至三维数据的高精度映射与结构分析。

## 技术方案

DIG包含两个并行过程：

1. **二维结构面检测**：依托预训练的AI视觉模型，实现对结构面（节理、裂隙等）的快速识别与分割，支持交互提示（点、框）以提升识别精度。
2. **三维结构重建与映射**：基于SfM技术生成稀疏点云及相机姿态信息，并建立像素与点云之间的对应关系，从而将二维识别结果自动投影至三维空间，实现结构面空间定位与重建。

## 核心特点

* **开箱即用**：无需人工参数调整或训练数据集，适应多种现场数据
* **交互识别**：支持实时提示交互，用户可修正或强化识别区域
* **三维支持**：自动建立二维-三维映射，实现结构面三维定位与导出
* **多设备兼容**：支持无人机/手持设备（移动式）和三脚架相机（固定式）数据
* **结构面索引机制**：通过单/双重索引机制自动关联图像、合成图与点云，实现结构面的高效提取

## 安装与运行
模式选择：`auto` 自动识别，`interactive` 人工提示增强识别，`manual` 人工标注
(...
待补充
...）

## 典型应用场景

* 工程地质调查与设计支撑
* 岩体三维建模与节理分析
* 高风险边坡及地下工程裂隙监测

## 联系方式

王嘉伟 Jiawei Wang (Jewell) 
PhD Candidate, Disaster Prevention Engineering Institute
College of Civil Engineering and Architecture, Zhejiang University, Zhejiang, China
📧 22112076@zju.edu.cn / jewellwangzju@gmail.com
🔗 QRMAILER

## 许可协议

MIT License
