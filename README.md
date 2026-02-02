# 🌋 SoulSolvent: Vulkan Shader & Rendering Research
![UE Version](https://img.shields.io/badge/Unreal_Engine-5.3+-blue?logo=unrealengine)
![Category](https://img.shields.io/badge/Technical_Art-Shader_Development-orange)
![Status](https://img.shields.io/badge/Status-In_Progress-green)

> **项目定位**：从底层数学逻辑出发，在 UE5 中重构自定义光照模型，旨在探索火山地形的风格化渲染与性能优化。

---

## 🛠️ 当前技术实现 (Technical Implementation)

### 1. 基础光照重构：从 Lambert 到 Half-Lambert
本项目脱离了引擎默认的 Lit 模式，通过材质编辑器手动实现了光照向量运算，解决了复杂地形内壁的“死黑”问题。

* **兰伯特 (Lambert)**: 
    * 公式：DirectLight = saturate(Dot(Normal, LightDir))
    * **心得**：建立了法线与光向的初步空间关系，但在火山坑阴影处表现过于生硬。
* **半兰伯特 (Half-Lambert)**:
    * 公式：Result = (Dot(Normal, LightDir) \times 0.5 + 0.5)^2
    * **效果**：通过对点积结果进行**线性重映射**，极大地增强了背光面的通透感，模拟出微弱的环境光散射效果。



---

## 📌 避坑与 Debug 记录 (Development Log)

在 TA 的进阶路上，解决问题的过程比结果更重要：

* **[SM5] Power Node 报错修复**：
    * **现象**：连接自发光后出现红色报错，提示 `Missing Power Base input`。
    * **原因**：逻辑混淆，误将数据源连入 `Exp` 指数端而导致 `Base` 底数端空置。
    * **解决**：明确了底数（数值流）与指数（对比度调整）的数学对应关系，确保了 Shader 编译成功。
* **版本管理习惯**：
    * 坚持使用 Git 进行原子化提交。即便是一个公式的微调（如从 Power 2.0 到 7.0），也会记录在册，确保资产的安全性。

---

## 📅 未来路线图 (Roadmap)

### 🟢 近期目标：动态环境感
- [ ] **Noise 扰动系统**：引入噪声函数，让火山内的蓝光产生类似岩浆律动的“呼吸感”。
- [ ] **Fresnel 边缘效应**：增加内壁边缘的轮廓光，增强空间层次感。

### 🟡 中期目标：矩阵与变换
- [ ] **矩阵旋转平移**：使用 $3 \times 3$ 矩阵控制熔岩纹理的扭曲与流动，不只是简单的 UV 偏移。
- [ ] **自定义材质函数 (MF)**：将光照模型封装，提高材质逻辑的复用性。

### 🔴 长期愿景
- [ ] **程序化火山地貌**：结合材质位移与噪声，实现动态隆起的火山口资产。

---

## 🤝 关于作者
一名正在向独立 TA 进化的开发者。
**“记录一下成为更好的自己”**
