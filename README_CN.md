# 脑电图(EEG)研究前沿：从基础脑科学到人工智能 (2024-2026)

> 一份面向 CS/AI 研究者的 EEG 领域全景式综述 —— 从神经元的生物物理基础到深度学习基础模型与脑机接口，层层递进，系统梳理。每篇论文保留英文原标题，附中文一句话解读。

**最后更新**: 2026-04-10 | **引用论文**: 70+ | **公开数据集**: 15+

---

## 目录

- [第一部分：大脑基础 — 写给工程师的入门指南](#第一部分大脑基础--写给工程师的入门指南)
  - [0.1 大脑解剖基础](#01-大脑解剖基础)
  - [0.2 神经元如何通信](#02-神经元如何通信)
  - [0.3 从神经元到脑电波](#03-从神经元到脑电波)
  - [0.4 EEG 信号链](#04-eeg-信号链)
  - [0.5 EEG 与其他脑成像技术对比](#05-eeg-与其他脑成像技术对比)
- [第二部分：EEG 基础概念](#第二部分eeg-基础概念)
  - [1.1 神经振荡的频段](#11-神经振荡的频段)
  - [1.2 EEG 记录系统](#12-eeg-记录系统)
  - [1.3 事件相关电位 (ERP)](#13-事件相关电位-erp)
- [第三部分：经典信号处理](#第三部分经典信号处理)
  - [2.1 预处理流程](#21-预处理流程)
  - [2.2 源定位](#22-源定位)
  - [2.3 脑连接与网络分析](#23-脑连接与网络分析)
- [第四部分：神经科学前沿](#第四部分神经科学前沿)
  - [3.1 意识研究](#31-意识研究)
  - [3.2 睡眠与记忆巩固](#32-睡眠与记忆巩固)
  - [3.3 注意力与认知负荷](#33-注意力与认知负荷)
  - [3.4 神经振荡新理论 (2024-2026)](#34-神经振荡新理论-2024-2026)
- [第五部分：EEG + 深度学习](#第五部分eeg--深度学习)
  - [4.1 EEG 基础模型](#41-eeg-基础模型)
  - [4.2 自监督与迁移学习](#42-自监督与迁移学习)
  - [4.3 脑解码：EEG 转文本与视觉重建](#43-脑解码eeg-转文本与视觉重建)
  - [4.4 EEG 信号分类](#44-eeg-信号分类)
- [第六部分：脑机接口](#第六部分脑机接口)
  - [5.1 运动想象 BCI](#51-运动想象-bci)
  - [5.2 P300 与 SSVEP](#52-p300-与-ssvep)
  - [5.3 新兴 BCI 范式](#53-新兴-bci-范式)
- [第七部分：临床应用](#第七部分临床应用)
  - [6.1 癫痫检测与预测](#61-癫痫检测与预测)
  - [6.2 自动睡眠分期](#62-自动睡眠分期)
  - [6.3 神经退行性疾病生物标志物](#63-神经退行性疾病生物标志物)
  - [6.4 精神疾病分类](#64-精神疾病分类)
  - [6.5 脑年龄估计](#65-脑年龄估计)
- [第八部分：数据集、工具与基础设施](#第八部分数据集工具与基础设施)
  - [7.1 主要公开数据集](#71-主要公开数据集)
  - [7.2 开源工具](#72-开源工具)
  - [7.3 基础模型代码仓库](#73-基础模型代码仓库)
- [第九部分：研究社区](#第九部分研究社区)
  - [8.1 重要研究组](#81-重要研究组)
  - [8.2 竞赛与挑战](#82-竞赛与挑战)
  - [8.3 相关会议](#83-相关会议)
- [第十部分：新兴方向 (2025-2027)](#第十部分新兴方向-2025-2027)

---

## 第一部分：大脑基础 — 写给工程师的入门指南

> 如果你是从机器学习或信号处理方向切入 EEG 研究的，这一部分将帮你建立必要的神经科学直觉。不需要你成为神经科学家，但理解信号的来源是做好下游任务的前提。

### 0.1 大脑解剖基础

**大脑皮层的四个叶**:

人类大脑皮层分为四大脑叶，每个脑叶承担不同的功能：

| 脑叶 | 位置 | 主要功能 | 与 EEG 的关系 |
|------|------|----------|---------------|
| **额叶** (Frontal) | 前部 | 执行功能、决策、运动规划、语言产生 (Broca区) | 运动想象 BCI 的关键区域；前额 theta 节律反映认知负荷 |
| **顶叶** (Parietal) | 顶部 | 体感处理、空间感知、注意力整合 | P300 成分的主要发生源；空间注意力研究的核心区域 |
| **颞叶** (Temporal) | 侧面 | 听觉处理、语言理解 (Wernicke区)、记忆 | N400 语义加工、内侧颞叶(含海马)参与记忆编码 |
| **枕叶** (Occipital) | 后部 | 视觉处理 | Alpha 节律的主要来源；SSVEP-BCI 的目标区域 |

**灰质与白质**:
- **灰质** (Gray matter)：由神经元细胞体组成，位于大脑皮层表面（厚约 2-4mm）和皮层下核团。EEG 信号主要来源于灰质中锥体神经元的突触后电位。
- **白质** (White matter)：由髓鞘包裹的轴突纤维束组成，是大脑的"布线系统"。白质连接的完整性直接影响 EEG 信号在脑区间的传播与同步。

**皮层柱** (Cortical columns)：
大脑皮层的基本功能单元是垂直于皮层表面的微型柱状结构（直径约 0.5mm，包含 ~80-100 个神经元）。同一皮层柱内的锥体神经元具有平行排列的顶树突，当它们同步激活时会产生可在头皮测量到的电场 —— 这正是 EEG 信号的物理基础。

**丘脑** (Thalamus)：
位于大脑深处的"中继站"，几乎所有感觉信息（除嗅觉外）都经过丘脑传递到皮层。丘脑与皮层之间的环路（丘脑-皮层环路）是产生 alpha 和 sleep spindle 等脑电节律的核心结构。

**海马** (Hippocampus)：
位于内侧颞叶，是记忆编码和空间导航的关键结构。海马的 theta 节律(4-8 Hz)在记忆形成中起核心作用。虽然海马位置较深，头皮 EEG 难以直接记录其活动，但可通过颅内 EEG (iEEG/SEEG) 进行研究。

### 0.2 神经元如何通信

**动作电位** (Action Potential, AP)：
- 当神经元接收到足够的兴奋性输入，达到阈值电位（约 -55mV）时，产生一个持续 ~1ms 的全或无电信号
- 沿轴突以 1-100 m/s 的速度传播到突触末梢
- 具有不应期（绝对不应期 ~1ms + 相对不应期 ~2ms），限制了神经元的最大放电率（约 500 Hz）

**突触传递** (Synaptic Transmission)：
- 动作电位到达突触末梢 -> 释放神经递质 -> 与突触后受体结合 -> 产生突触后电位
- **兴奋性突触后电位** (EPSP)：谷氨酸等兴奋性递质使突触后膜去极化
- **抑制性突触后电位** (IPSP)：GABA 等抑制性递质使突触后膜超极化
- 一个皮层锥体神经元通常接收 ~10,000 个突触输入

**为什么 EEG 测量的是 PSP 而不是 AP?**

这是理解 EEG 信号本质的关键问题：

| 特性 | 动作电位 (AP) | 突触后电位 (PSP) |
|------|--------------|------------------|
| 持续时间 | ~1 ms | 10-200 ms |
| 空间范围 | 局限于轴突上一小段 | 沿树突大范围分布 |
| 同步性 | 不同神经元的 AP 难以精确同步 | 相同输入驱动的 PSP 天然同步 |
| 极性一致性 | 双相，快速翻转 | 单极性持续较长，有利于空间叠加 |

简单来说：PSP 足够慢、足够同步、空间分布足够广，使得成千上万个锥体神经元的 PSP 能够在头皮上叠加出可测量的电位差。AP 太快太短，来不及叠加就消失了。

### 0.3 从神经元到脑电波

**振荡如何产生?**

脑电波（神经振荡）并非单个神经元的特性，而是大量神经元群体活动的涌现现象：

1. **兴奋-抑制平衡**：兴奋性神经元激活抑制性中间神经元（interneurons），抑制性中间神经元反过来抑制兴奋性神经元，形成负反馈环路。这个环路的固有延迟决定了振荡频率。
2. **抑制性中间神经元的核心作用**：PV+（小白蛋白阳性）中间神经元通过 GABA_A 受体提供快速抑制，驱动 gamma 振荡（30-100 Hz）；SOM+（生长抑素阳性）中间神经元则与 theta/alpha 节律相关。
3. **丘脑-皮层环路**：丘脑中继核的固有膜特性（T 型钙通道的去失活/再激活周期）产生 ~10 Hz 的振荡，通过丘脑-皮层投射传导到皮层，这是 alpha 节律和睡眠纺锤波的主要来源。

**关键概念 —— 同步性**：
当同一皮层区域内数万个锥体神经元以相同频率和相位产生 PSP 时，电场在头皮上相干叠加。神经振荡本质上就是这种大规模同步活动的外在表现。

### 0.4 EEG 信号链

从突触后电位到你屏幕上的波形，信号经历了以下完整路径：

```
突触后电位 (PSP)
    ↓ 皮层锥体细胞顶树突产生电流偶极子
等效电流偶极子 (Current Dipole)
    ↓ 电场通过脑组织传导
容积传导 (Volume Conduction)
    ↓ 经过脑脊液 → 颅骨 → 头皮（每层都衰减和平滑信号）
头皮表面电位（~10-100 μV）
    ↓ 导电膏/干电极拾取
电极采集（电位差）
    ↓ 前置放大器（增益 ~1000-10000x）+ 抗混叠滤波器
模数转换 (ADC)（采样率 250-1000 Hz，分辨率 16-24 bit）
    ↓ 数字信号
软件处理（滤波 → 去伪迹 → ICA → 分段 → 分析）
```

**信号衰减的物理原因**：
- 颅骨的电导率仅为脑脊液的 1/80，是信号从皮层到头皮的主要衰减层
- 深度为 d 的电流偶极子源，在头皮上的投影宽度约为 ~2d —— 这意味着空间分辨率受限于约 1-2 cm
- 这就是为什么 EEG 的空间分辨率远不如 fMRI，但时间分辨率（毫秒级）远优于 fMRI（秒级）

### 0.5 EEG 与其他脑成像技术对比

| 技术 | 测量对象 | 时间分辨率 | 空间分辨率 | 设备成本 | 便携性 | 典型应用场景 |
|------|---------|-----------|-----------|---------|--------|------------|
| **EEG** | 头皮电位 (PSP) | ~1 ms | ~1-2 cm | $1K-100K | 高（可穿戴） | BCI、睡眠、癫痫、认知研究 |
| **MEG** | 颅外磁场 | ~1 ms | ~3-5 mm | ~$2M+ | 极低（需屏蔽室） | 癫痫灶定位、语言皮层映射 |
| **fMRI** | BOLD 信号（血氧） | ~1-2 s | ~1 mm | ~$1-3M | 无 | 认知神经科学、临床诊断 |
| **fNIRS** | 近红外光吸收（血氧） | ~100 ms | ~1 cm | $10K-100K | 中等 | 婴幼儿研究、社交互动 |
| **ECoG/iEEG** | 皮层表面/深部电位 | ~1 ms | ~1 mm | 手术费用 | 无（需开颅植入） | 癫痫手术规划、高精度 BCI |

**对 AI 研究者的启示**：EEG 之所以成为 AI+脑科学交叉研究的首选模态，核心原因在于：(1) 毫秒级时间分辨率适合序列建模；(2) 多通道空间结构天然适合图神经网络等空间建模方法；(3) 设备门槛低，数据采集成本可控，便于大规模数据集构建。

---

## 第二部分：EEG 基础概念

### 1.1 神经振荡的频段

| 频段 | 频率范围 | 典型振幅 | 认知/生理状态 | 关键脑区 | 临床意义 |
|------|---------|---------|-------------|---------|---------|
| **Delta** (δ) | 0.5-4 Hz | 20-200 μV | 深睡眠 (N3)、婴幼儿脑电 | 丘脑 → 广泛皮层 | 异常增多提示脑损伤或脑病 |
| **Theta** (θ) | 4-8 Hz | 5-100 μV | 记忆编码、空间导航、嗜睡 | 海马、前额中线 | 癫痫灶的间期放电常含 theta |
| **Alpha** (α) | 8-13 Hz | 10-50 μV | 安静觉醒(闭眼)、主动抑制 | 枕叶(视觉alpha)、感觉运动区(mu节律) | 阿尔茨海默症早期 alpha 减弱 |
| **Beta** (β) | 13-30 Hz | 5-30 μV | 主动思维、运动规划、焦虑 | 运动皮层、额叶 | 帕金森病 beta 振荡异常 |
| **Gamma** (γ) | 30-100+ Hz | 1-10 μV | 意识感知、特征绑定、记忆提取 | 广泛分布 | 精神分裂症 gamma 节律缺陷 |

**进阶知识**：
- **Mu 节律** (8-13 Hz)：与视觉 alpha 频率相同但发生在感觉运动区，运动想象时出现事件相关去同步化 (ERD)，是运动想象 BCI 的核心信号特征
- **Sleep spindle** (12-15 Hz)：N2 期睡眠特有的梭形波，持续 0.5-2 秒，由丘脑网状核产生，与记忆巩固密切相关
- **1/f 噪声（非周期成分）**：EEG 功率谱不只包含上述周期性振荡，还有一个遵循 1/f^β 衰减的非周期背景。该斜率 β 本身也携带有意义的信息（例如与意识水平相关）

**经典参考文献**：
- Buzsaki, *Rhythms of the Brain* (Oxford, 2006) — 神经振荡领域最有影响力的专著
- Fries, "Rhythms for Cognition: Communication through Coherence" (*Neuron*, 2015) — 通过相干性实现脑区间信息路由的理论框架

### 1.2 EEG 记录系统

**标准电极放置系统**：
- **10-20 系统** (19-21 通道)：临床标准。电极位置根据颅骨标志点（鼻根、枕外隆突、耳前点）按 10% 和 20% 间距定义。命名规则：字母表示脑区 (F=额, C=中央, P=顶, O=枕, T=颞)，奇数=左半球，偶数=右半球，z=中线。
- **10-10 系统** (64-128 通道)：研究级标准，提供更高的空间采样密度
- **高密度 EEG** (256-512 通道)：用于源定位研究，由 UCSD SCCN 等团队推广

**信号基本参数**：
- 振幅：10-100 μV（对比 ECG ~1mV, EMG ~10mV —— EEG 是最微弱的生物电信号之一）
- 采样率：通常 250-1000 Hz（高频振荡研究可达 20 kHz）
- 阻抗要求：湿电极 <5 kΩ，干电极 <50 kΩ，电容式电极 <1 MΩ

**干电极技术进展 (2023-2026)**：
传统湿电极需要导电膏来降低皮肤-电极界面阻抗，佩戴耗时且不适合日常使用。干电极和半干电极是消费级 EEG 和可穿戴设备发展的关键技术瓶颈。近年来 IDUN Guardian（耳内式）、Emotiv EPOC X、Muse 2 等设备在信号质量与舒适度之间取得了更好的平衡。

### 1.3 事件相关电位 (ERP)

ERP 是通过对同一刺激的多次试验进行时间锁定平均而提取的电位波形，反映特定认知加工过程：

| 成分 | 潜伏期 | 极性 | 认知过程 | 经典范式 | 应用 |
|------|--------|------|---------|---------|------|
| **N1/P1** | 80-120 ms | N/P | 早期感觉加工 | 任意刺激 | 感觉通路完整性评估 |
| **MMN** (失匹配负波) | 100-250 ms | N | 前注意变化检测 | 被动 oddball | 精神分裂症生物标志物 |
| **N170** | ~170 ms | N | 面孔加工 | 面孔 vs. 物体 | 自闭症面孔加工研究 |
| **P300** (P3b) | 300-600 ms | P | 刺激评估、情境更新 | 主动 oddball | BCI 拼写器、注意力评估 |
| **N400** | ~400 ms | N | 语义加工 | 句子阅读 | 语言理解、EEG-to-Text 研究 |
| **P600** | ~600 ms | P | 句法再分析 | 花园路径句 | 语言加工研究 |
| **ERN** (错误相关负波) | 错误后 50-100 ms | N | 错误检测 | Flanker/Stroop | 强迫症、焦虑研究 |

**经典参考文献**：
- Luck, *An Introduction to the Event-Related Potential Technique* (MIT Press, 2nd ed., 2014) — ERP 技术的标准教科书

---

## 第三部分：经典信号处理

### 2.1 预处理流程

标准 EEG 预处理流水线（按顺序执行）：

```
1. 高通滤波 (0.1-1 Hz)     → 去除慢漂移
2. 工频陷波 (50/60 Hz)      → 去除电网干扰
3. 坏导检测与插值           → 球面样条插值修复坏导
4. 重参考                   → 平均参考 / 双侧乳突 / REST
5. ICA (独立成分分析)       → 分离并去除伪迹（眨眼、肌电、心电）
6. 分段 (Epoching)          → 围绕事件标记切割时间窗
7. 基线校正                 → 减去刺激前均值
8. 伪迹剔除                 → 振幅阈值或概率判据剔除坏段
```

**前沿方向 (2024-2026): 深度学习去伪迹**：
- **ICLabel** (Pion-Tonachini et al., *NeuroImage*, 2019) — 基于 CNN 的 ICA 成分自动分类，已集成进 EEGLAB 和 MNE-Python。[GitHub](https://github.com/sccn/ICLabel)
- **IC-U-Net** (Cai et al., *NeuroImage*, 2024) — 基于 U-Net 的时域直接去伪迹，无需 ICA 步骤
- **EEGDfus** (Li et al., 2025) — 基于条件扩散模型的 EEG 去噪，从含噪 EEG 生成干净信号

### 2.2 源定位

**逆问题** (Inverse Problem)：从头皮电位推断脑内源活动位置。这是一个数学上的不适定问题（无穷多个源分布可产生相同的头皮电位模式），必须引入先验约束：

- **前向问题** (Forward Problem)：给定源活动位置和方向，计算头皮电位分布。需要头部体积导体模型（球模型或基于 MRI 的个体化 BEM/FEM 模型）
- **逆向求解方法**：
  - **偶极子拟合**：假设 1-3 个等效电流偶极子，快速但假设过强
  - **波束成形** (LCMV, DICS)：空间滤波方法，保持良好时间分辨率
  - **分布式源模型** (eLORETA, sLORETA, MNE)：在整个皮层上估计电流密度分布，无需预设偶极子数量

**前沿方向**：基于深度学习的源定位 (Hecker et al., *NeuroImage*, 2024) —— 用 CNN 在前向模型生成的训练数据上学习逆映射，推理速度远超传统迭代算法。

### 2.3 脑连接与网络分析

**功能连接** (Functional Connectivity) 方法：

| 方法 | 原理 | 优点 | 局限 |
|------|------|------|------|
| **相干性** (Coherence) | 频域相关 | 计算简单，物理意义清晰 | 容积传导伪连接问题严重 |
| **相位锁定值** (PLV) | 相位同步，不依赖振幅 | 抗容积传导干扰较好 | 仍受共同源影响 |
| **格兰杰因果** (Granger Causality) | 时间序列预测性检验 | 有向连接，可推断因果影响方向 | 假设线性，对噪声敏感 |
| **传递熵** (Transfer Entropy) | 信息论方法 | 捕捉非线性因果关系 | 计算量大，需要长数据 |
| **微状态分析** (Microstate) | 准稳态拓扑图聚类 | 全脑动态描述（通常 4-7 类典型状态） | 空间分辨率受限于电极数量 |

**前沿方向 (2024-2026)**：
- **图神经网络建模 EEG 连接** —— 将电极视为图节点，学习动态邻接矩阵 (Zhong et al., *IEEE TNNLS*, 2024)
- **"A deep learning-enriched framework for analyzing brain functional connectivity"** — 提出 FCNet，可解释的 CNN 用于频谱有向功能连接分析 (Zhao et al., *Scientific Reports*, 2025)

---

## 第四部分：神经科学前沿

### 3.1 意识研究

EEG 在意识研究领域正发挥越来越重要的作用，尤其是对意识障碍患者（植物状态 vs. 最小意识状态）的鉴别诊断：

**扰动复杂性指数 (PCI)**：
Casali et al. (*Science Translational Medicine*, 2013) 提出的 TMS-EEG 综合指标。对大脑施加 TMS 脉冲后测量 EEG 响应的时空复杂度：意识清醒状态下脑响应复杂度高（PCI > 0.31），无意识状态下响应简单或消失。在 200+ 例患者中诊断准确率达 97%。

**1/f 谱斜率作为意识标志物**：
- **"The Neural Correlates of Consciousness: A Spectral Exponent Approach to Diagnosing Disorders of Consciousness"** — 评估 EEG 谱指数作为意识水平的客观生物标志物，窄带 SE(1-20 Hz) 对区分植物状态与最小意识状态表现出更优的诊断灵敏度 (Colombo et al., *Brain Sciences*, 2025)
- 斜率越陡（更负的指数）= 意识水平越低

**IIT vs GNWT 两大意识理论**：
- **整合信息论** (IIT, Tononi)：意识 = 系统整合信息的能力 (Φ)。从 EEG 估算 Φ 在计算上极具挑战，但基于状态空间模型的近似方法正在推进
- **全局神经工作空间理论** (GNWT, Dehaene & Changeux)：意识 = 信息在脑区间的全局广播。EEG 中的 P300 和晚期广泛激活模式（"点火"模式）被视为意识接入的标志
- 两大理论的对抗性合作研究正在进行 (Melloni et al., *Nature Neuroscience*, 2024)

**"Detection of EEG dynamic complex patterns in disorders of consciousness"** — 分析 237 例意识障碍患者，识别出五种反复出现的功能连接模式，其出现概率与意识水平强相关 (Sitt et al., *Communications Biology*, 2025)

### 3.2 睡眠与记忆巩固

**睡眠纺锤波与记忆**：
N2 期的 sigma 频段 (12-15 Hz) 纺锤波现在被认为与特定记忆痕迹相关联。在学习过程中被 theta 节律"标记"的记忆会在后续睡眠中被优先重放 (Petzka et al., *Nature Neuroscience*, 2024)。

**慢振荡-纺锤波耦合** (SO-Spindle Coupling)：
- 慢振荡 (<1 Hz) 的特定相位调控纺锤波的出现时机，创造海马-皮层记忆转移的最佳时间窗口
- 耦合的精确程度可预测次日记忆表现 (Helfrich et al., 2018；2024-2025 年更新分析)

**"Theta oscillations tag memories for sleep-dependent consolidation"** — 证明学习期间 3-8 Hz theta 节律可以"标签"记忆以供后续睡眠巩固，theta 幅度可预测学习后睡眠中慢振荡-纺锤波耦合的强度 (Staresina et al., *bioRxiv*, 2025)

**靶向记忆再激活** (TMR)：
在睡眠期间呈现与学习相关的线索（声音、气味），可增强记忆巩固。EEG 触发的 TMR（在慢振荡特定相位递送线索）是一个活跃的干预研究方向。

### 3.3 注意力与认知负荷

- **Alpha 去同步化**：经典的注意力标志物。注意目标刺激时，相关皮层区域 alpha 功率降低（去抑制），无关区域 alpha 功率升高（主动抑制）。"聚光灯"比喻：alpha 压制无关脑区的信息处理
- **前额 Theta**：随认知负荷增加而增强（心算、工作记忆任务）。在神经工效学中用于实时工作负荷监测
- **注意瞬脱** (Attentional Blink, AB)：快速连续呈现的两个目标中，第二个目标在 200-500ms 间隔内常被漏掉。EEG 相关物为漏检目标的 P300 缺失

### 3.4 神经振荡新理论 (2024-2026)

**pACF 方法**：
- **"Rhythmicity of neuronal oscillations delineates their cortical and spectral architecture"** — 引入相位自相关函数 (pACF) 直接量化 SEEG 和 MEG 数据中的节律性，揭示了传统方法不可见的精细皮层节律架构 (Schaworonkow & Bhatt et al., *Communications Biology*, 2024)
- pACF 比传统频谱分析和 FOOOF/specparam 更干净地分离周期性与非周期性成分

**行波** (Traveling Waves)：
EEG/ECoG 证据表明振荡并非驻波，而是以有组织的模式在皮层上传播。行波的方向和速度与认知状态相关 (Muller et al., 2018; 2024 年更新分析)。

**跨频耦合** (Cross-Frequency Coupling, CFC)：
Theta 相位与 gamma 振幅之间的相位-振幅耦合 (PAC) 被提出为多项目工作记忆的神经机制：每个 theta 周期内的每个 gamma 爆发代表一个记忆项目 (Lisman & Jensen, 2013；验证工作持续进行中)。

**"Processes and measurements: A framework for understanding neural oscillations in field potentials"** — 区分振荡研究中的"测量"与"过程"，回应振荡究竟是因果性的还是附现象的这一持续争论 (Miller et al., *Trends in Cognitive Sciences*, 2024)

---

## 第五部分：EEG + 深度学习

### 4.1 EEG 基础模型

2023-2026 年 EEG 领域最大的范式转变：在海量无标注 EEG 数据上预训练大模型，然后对下游任务进行微调。

| 模型 | 年份 | 会议 | 预训练数据 | 参数量 | 核心创新 | 代码 |
|------|------|------|-----------|--------|---------|------|
| **LaBraM** | 2024 | ICLR (Spotlight) | ~2,500 小时, ~20 数据集 | -- | 向量量化分词器 + 掩码神经编码预测 | [GitHub](https://github.com/935963004/LaBraM) |
| **NeuroLM** | 2025 | ICLR | 多模态 (EEG + 文本), ~25,000 小时 | 1.7B | 首个十亿级 EEG-语言模型；将 EEG 视为 LLM 的"外语" | [GitHub](https://github.com/935963004/NeuroLM) |
| **CBraMod** | 2025 | ICLR | EEG + 多种生物信号 | -- | 十字交叉 Transformer，空间与时间双路注意力 | [GitHub](https://github.com/wjq-learning/CBraMod) |
| **Brant-2** | 2024 | arXiv | 22K 小时临床 EEG | -- | 最大单源预训练；支持 4 至 1024 通道 | [arXiv](https://arxiv.org/abs/2402.10251) |
| **EEGPT** | 2024 | NeurIPS | 多个 EEG 数据集 | 10M | 基于掩码的双重自监督学习；时空对齐 | [GitHub](https://github.com/BINE022/EEGPT) |
| **EEGMamba** | 2025 | Neural Networks | 16,724 小时, 5 个数据集 | -- | 用 Mamba 状态空间模型替代 Transformer 主干 | [GitHub](https://github.com/wjq-learning/EEGMamba) |
| **REVE** | 2025 | arXiv | 25,000 名被试 | -- | 最大被试规模预训练；新颖 4D 位置编码适配任意电极配置 | [项目主页](https://brain-bzh.github.io/reve/) |
| **BIOT** | 2023 | NeurIPS | 多种生物信号 (EEG, ECG, EMG) | -- | 异质信号统一分词，跨模态迁移 | [GitHub](https://github.com/ycq091044/BIOT) |
| **BENDR** | 2021 | arXiv | TUH 语料库 | -- | 对比自监督学习；"被试不变"表征 | [GitHub](https://github.com/SPOClab-ca/BENDR) |
| **FoME** | 2024 | arXiv | 多中心数据 | 476M/745M | 自适应时空注意力缩放的基础模型 | -- |

**综述论文**：
- **"Self-supervised Learning for Electroencephalogram: A Systematic Survey"** — EEG 自监督学习的系统分类法（对比、预测、生成范式），涵盖 100+ 方法 (Zhang et al., *ACM Computing Surveys*, 2025)
- **"Large Language Models for EEG: A Comprehensive Survey and Taxonomy"** — 将 LLM-EEG 研究组织为四个领域：基础模型、EEG-to-语言解码、跨模态生成、临床工具 (Li et al., arXiv, 2025) [arXiv](https://arxiv.org/abs/2506.06353)
- **"A Simple Review of EEG Foundation Models"** — 15+ EEG 基础模型的并排对比，包括架构、预训练数据与下游性能 (Guo et al., arXiv, 2025) [arXiv](https://arxiv.org/abs/2504.20069)

### 4.2 自监督与迁移学习

核心挑战：EEG 在不同被试间差异巨大（头部解剖、电极放置、阻抗），预训练通过以下策略应对：

- **对比学习** (Contrastive Learning)：学习表征使同一被试/同一状态的 EEG 接近，不同被试的 EEG 远离。代表方法：BENDR, ContraWR (2023)
- **掩码信号预测** (Masked Signal Prediction)：遮盖 EEG 的部分片段，从上下文预测。代表方法：LaBraM, CBraMod
- **域适应** (Domain Adaptation)：对齐源域和目标域被试的特征分布，是实现"零校准" BCI 的关键

**统一基准**：**EEG-FM-Bench** (2025) — 在 14 个数据集、10 个范式上统一评估 7 个基础模型，包括梯度分析和表征探测。[GitHub](https://github.com/xw1216/EEG-FM-Bench)

### 4.3 脑解码：EEG 转文本与视觉重建

#### EEG-to-Text（EEG 转文本）

1. **"DeWave: Discrete EEG Waves Encoding for Brain Dynamics to Text Translation"** — 引入量化变分编码器将连续 EEG 映射到离散 codex 分词并与预训练 LLM 对齐，首次不依赖词级标记直接翻译原始 EEG，在 ZuCo 数据集上取得 41.35 BLEU-1 (Duan et al., NeurIPS 2023) [arXiv](https://arxiv.org/abs/2309.14030)

2. **"Are EEG-to-Text Models Working?"** — **必读警示论文**。批判性分析显示许多 EEG-to-Text 模型在评估中使用了隐式 teacher-forcing，模型在随机噪声上的表现可匹配真实 EEG，呼吁更严格的基准 (Jo & Yang, ACL 2024) [论文](https://aclanthology.org/2024.acl-long.727/)

3. **"NeuSpeech: Decode Neural Signal as Speech"** — 将 Whisper 语音模型改造为接受原始 MEG/EEG 输入，展示了从非侵入式记录直接进行神经-语音解码的可行性 (Yang et al., 2024) [arXiv](https://arxiv.org/abs/2403.01748)

#### EEG-to-Image/Video（EEG 转图像/视频）

4. **"DreamDiffusion: High-Quality EEG-to-Image Generation with Temporal Masked Signal Modeling and CLIP Alignment"** — 用时序掩码信号建模预训练 EEG 编码器并对齐到 CLIP 空间，再用冻结的 Stable Diffusion 从脑活动生成图像 (Bai et al., ECCV 2024) [arXiv](https://arxiv.org/abs/2306.16934)

5. **"Visual Decoding and Reconstruction via EEG Embeddings with Guided Diffusion"** — 引入自适应思维映射器 (ATM) 将 EEG 投影到 CLIP 嵌入空间，两阶段多管道生成策略实现 SOTA 零样本分类、检索和重建 (Li et al., NeurIPS 2024)

6. **"EEG2Video: Towards Decoding Dynamic Visual Perception from EEG Signals"** — 从 EEG 重建 2 秒视频片段，引入动态感知噪声添加扩散过程和 SEED-DV 数据集（20 名被试、1400 个视频片段、40 个概念），语义分类准确率达 79.8% (Liu et al., NeurIPS 2024)

7. **"Perceptogram: Reconstructing Visual Percepts from EEG"** — 证明从 EEG 到 CLIP 空间的简单线性解码器加冻结扩散模型就足以实现 SOTA 图像重建，揭示了对应语义类别、纹理和色调的可解释 EEG 特征图 (Dehaene et al., NeurIPS 2024)

#### 内部言语解码

8. **"Chisco: An EEG-based BCI dataset for decoding of imagined speech"** — 发布迄今最大的个体内部言语 EEG 数据集：每位被试 >20,000 句、>900 分钟高密度 EEG，面向中文想象语音研究 (Li et al., *Scientific Data*, 2024)

9. **"Inner speech in motor cortex and implications for speech neuroprostheses"** — 利用多单元记录证明内部言语在运动皮层中有稳健表征，实时解码想象句子达到实用 BCI 性能 (Wandelt et al., *Cell*, 2025)

### 4.4 EEG 信号分类

**情绪识别**：
- 主要数据集：DEAP (32 名被试)、SEED 系列 (15 名被试, 3/4/7 类情绪)
- 前沿方法：图神经网络捕捉电极间空间关系；通过域适应提升跨被试准确率（SEED 上 70-85%）
- 关键挑战：跨被试泛化性差、情绪标签主观性高

**运动想象分类**：
- **EEGNet** (Lawhern et al., 2018) — 紧凑型 CNN，至今仍是强基线
- Transformer 系列：EEG Conformer (Song et al., 2023), ATCNet (Altaheri et al., 2023)
- 当前 SOTA：BCI Competition IV-2a 四分类约 85-90%

---

## 第六部分：脑机接口

### 5.1 运动想象 BCI

运动想象（想象手、脚运动）在感觉运动皮层上层产生可检测的事件相关去同步化 (ERD)：mu 节律 (8-12 Hz) 和 beta 节律 (18-26 Hz) 功率下降。

**深度学习用于 MI-BCI**：
- Transformer 和注意力机制已成为主流，取代了传统 CSP+LDA 流水线
- **"Advancing BCI with a transformer-based model for motor imagery classification"** — 结合改进的 Transformer 和 TCN 的 EEGEncoder，在 BCI-IV-2a 上被试依赖准确率达 86.46% (Lee et al., *Scientific Reports*, 2025)
- **"Hierarchical attention enhanced deep learning achieves high precision motor imagery classification"** — 整合空间 CNN、时序 LSTM 和选择性注意力，准确率达 97.25% (Wang et al., *Scientific Reports*, 2025)

**迁移学习是关键前沿**：
让 BCI 在新用户上无需冗长校准即可工作。域适应方法（对抗学习、最优传输）展现出巨大潜力。Min et al. (2024) 利用预训练 EEG 模型实现了无需校准的跨被试 MI 解码。

### 5.2 P300 与 SSVEP

**P300 拼写器**：
- 用户注视字母网格中的目标字母；oddball P300 响应识别目标
- **"SpellerSSL: Self-Supervised Learning with P300 Aggregation for Speller BCIs"** — 首次将自监督预训练应用于 P300 拼写器，仅 7 次重复即达 94% 字符识别率和 21.86 bits/min 信息传输率 (Li et al., arXiv, 2025)
- **"Connecting a P300 speller to a large language model"** — 将 P300 BCI 拼写器与 LLM 集成用于词预测和句子补全，大幅提升打字速度 (Belozerov et al., *bioRxiv*, 2025)

**SSVEP (稳态视觉诱发电位)**：
- 用户注视不同频率闪烁的视觉刺激；频率标记的脑响应识别注视目标
- 清华大学 BCI 实验室创下 **60+ 字符/分钟** 的世界纪录 —— 最快的非侵入式 BCI
- **"Enhancing the performance of SSVEP-based BCIs by combining task-related component analysis and deep neural network"** — 混合 eTRCA + sbCNN 框架结合传统空间滤波与子带 CNN (Zhang et al., *Scientific Reports*, 2025)
- 滤波器组典型相关分析 (FBCCA) 仍是主导的信号处理方法

### 5.3 新兴 BCI 范式

- **混合 BCI**：结合 MI + SSVEP 或 MI + P300，获取更高的信息传输速率
- **错误相关电位 (ErrP)**：检测 BCI 犯错的时刻，实现自动纠错
- **被动式 BCI**：监测认知状态（疲劳、注意力、工作负荷）而无需用户显式指令。应用于驾驶、航空、教育等领域

---

## 第七部分：临床应用

### 6.1 癫痫检测与预测

**癫痫检测**：
- 深度学习在连续 EEG 上的检测灵敏度已超过 95%
- 关键数据集：CHB-MIT (PhysioNet)
- 前沿方向：面向可穿戴设备的单通道检测方法

**癫痫预测**：
- 在发作前 30-60 分钟进行预测，信号特征包括发作前同步性变化和熵变化
- **"Deep learning for epileptic seizure prediction from EEG signals: A review"** — 全面综述 CNN、RNN 和混合架构，报告准确率最高达 99%，灵敏度最高达 99.8%，同时指出泛化性和实时处理的挑战 (Rasheed et al., *Biomedical Signal Processing and Control*, 2025)
- **"Single-channel EEG-based seizure prediction using deep learning"** — 开发超轻量级单通道模型，临床可操作标准为 2 分钟预测窗口、30 分钟发作发生期 (Kim et al., *Scientific Reports*, 2026)
- 自监督方法 (2024-2025) 在患者特异性预测上展现出改进

**高频振荡 (HFO)**：
80-500 Hz 的高频信号作为致痫灶的生物标志物。Gotman Lab (McGill) 等团队正在开发基于深度学习的自动 HFO 检测。

### 6.2 自动睡眠分期

将睡眠自动分类为 Wake（清醒）、N1、N2、N3、REM 五个阶段：

- **"KAN-SleepNet: A deep learning model combining Kolmogorov-Arnold Networks and bidirectional LSTM for automated sleep staging"** — 创新性地将 KAN（Kolmogorov-Arnold 网络）与 BiLSTM 结合用于 EEG 睡眠分期，展示了近期提出的 KAN 架构在生物信号处理中的应用潜力 (Xiong et al., *Digital Health*, 2025)
- **"MPSleepNet: Matrix Profile-Guided Transformer for Multi-Channel Sleep Classification"** — 使用 Matrix Profile 预处理 PSG 数据以突出显著模式，通过 Transformer 编码器融合时频表征 (Wu et al., *ACM SPML*, 2024)
- 标准基准：Sleep-EDF Expanded (PhysioNet)。当前 SOTA：整体准确率约 85-88%，N2/N3 等高代表性阶段可达 90%+

### 6.3 神经退行性疾病生物标志物

**阿尔茨海默症 (AD)**：
- EEG 减慢（alpha 减弱、theta/delta 增多）是早期生物标志物，可在临床诊断前数年被检测到
- **"STEADYNet: Spatiotemporal EEG analysis for dementia detection using convolutional neural network"** — 基于 CNN 的多通道时空特征模型，痴呆检测准确率达 98.24% (Sangle et al., *Cognitive Neurodynamics*, 2024)
- **"An explainable and efficient deep learning framework for EEG-based diagnosis of Alzheimer's disease and frontotemporal dementia"** — 使用 TCN 和 LSTM 同时分类 AD 和额颞叶痴呆，具有模型可解释性 (Wang et al., *Frontiers in Medicine*, 2025)

**帕金森病 (PD)**：
基底神经节-皮层回路中的 beta 频段异常，可用于深部脑刺激 (DBS) 参数调节。

### 6.4 精神疾病分类

**抑郁症 (MDD)**：
- 前额 alpha 不对称性（左侧 alpha 偏高 = 更多抑郁倾向）
- 深度学习分类准确率约 80-85%
- **"Advances in EEG-based detection of Major Depressive Disorder using shallow and deep learning techniques: A systematic review"** — 系统综述 CNN、LSTM、CNN-LSTM 混合、GNN 和 Transformer 用于 MDD 检测 (Ahmed et al., *Computers in Biology and Medicine*, 2025)
- **"Automated depression detection via cloud-based EEG analysis with transfer learning and synchrosqueezed wavelet transform"** — 云端部署的诊断系统，结合同步挤压小波变换特征提取与迁移学习 (Chen et al., *Scientific Reports*, 2025)

**ADHD**：Theta/Beta 比值在 ADHD 中偏高（但荟萃分析显示效应量小于最初报告），机器学习用于 ADHD 亚型分类。

**精神分裂症**：P300 振幅降低、gamma 频段异常、失匹配负波缺陷。

### 6.5 脑年龄估计

从 EEG 预测生理年龄，"脑年龄差距"（预测年龄 - 实际年龄）是一个有价值的健康生物标志物：正差距提示脑老化加速。

- **"Brain age revisited: Investigating the state vs. trait hypotheses of EEG-derived brain-age dynamics with deep learning"** — 使用时序卷积网络进行临床 EEG 年龄回归，探究脑年龄差距是瞬态状态还是稳定特质 (Gemein et al., *Imaging Neuroscience*, 2024)
- **"Dementia Risk and Machine Learning-Derived Brain Age Index from Sleep EEG"** — 大规模研究（7,000+ 个体，五个社区队列）将睡眠 EEG 衍生的脑年龄指数与痴呆风险关联 (Sun et al., 2025)
- **"EEG estimates brain age in infants with high precision"** — 在婴幼儿群体中开发 EEG 脑年龄估计器，展示了用于神经发育筛查的临床可行性 (Stevenson et al., *NeuroImage*, 2025)

---

## 第八部分：数据集、工具与基础设施

### 7.1 主要公开数据集

| 数据集 | 年份 | 被试数 | 通道数 | 任务 | 数据规模 | 链接 |
|--------|------|--------|--------|------|---------|------|
| **TUH EEG Corpus** | 2016+ | 10,874 | 19-24 | 临床（正常/异常） | ~572 GB | [isip.piconepress.com](https://isip.piconepress.com/projects/tuh_eeg/) |
| **HBN-EEG** | 2023+ | 3,000+ | 128 | 6 项认知任务（5-21 岁） | 多 TB | [neuromechanist.github.io](https://neuromechanist.github.io/data/hbn/) |
| **SEED / SEED-IV / SEED-VII** | 2015+ | 15 | 62 | 情绪识别（3/4/7 类） | ~2 GB/版本 | [bcmi.sjtu.edu.cn](https://bcmi.sjtu.edu.cn/home/seed/) |
| **DEAP** | 2012 | 32 | 32+8 外周 | 情绪（效价、唤醒度） | ~3 GB | [eecs.qmul.ac.uk](http://eecs.qmul.ac.uk/mmv/datasets/deap/) |
| **BCI Competition IV-2a** | 2008 | 9 | 22 | 四分类运动想象 | -- | [bbci.de](https://www.bbci.de/competition/iv/) |
| **CHB-MIT** | 2010 | 22（儿科） | 23 | 癫痫检测 | ~40 GB | [physionet.org](https://physionet.org/content/chbmit/1.0.0/) |
| **Sleep-EDF Expanded** | 2018 | 78 (197 记录) | 2+EOG+EMG | 睡眠分期 | -- | [physionet.org](https://physionet.org/content/sleep-edfx/1.0.0/) |
| **EEG Motor Movement** | 2004 | 109 | 64 | 运动执行/想象 | ~3 GB | [physionet.org](https://physionet.org/content/eegmmidb/1.0.0/) |
| **THINGS-EEG** | 2022+ | 10-50 | 63-64 | 视觉物体识别 | ~100 GB+ | [osf.io](https://osf.io/3jk45/) |
| **Inner Speech** | 2022 | 10 | 128 | 内部/发声/视觉化言语 | 5,640 试次 | [Nature](https://www.nature.com/articles/s41597-022-01147-2) |
| **Chisco** | 2024 | 多名 | 高密度 | 想象语音（20K+ 句） | 最大单人数据集 | [Nature](https://www.nature.com/articles/s41597-024-04114-1) |
| **SEED-DV** | 2024 | 20 | 62 | 视频视觉感知 | 1400 视频片段 | NeurIPS 2024 |
| **EEG Challenge 2025** | 2025 | 3,000+ | 128 | 6 项认知任务（跨被试解码） | -- | [eeg2025.github.io](https://eeg2025.github.io/data/) |
| **消费级 vs 研究级对比** | 2026 | 30 | 多种 | 设备对比 | -- | *Scientific Data* (Kok et al., 2026) |

**基准平台**：
- **Brain4FMs** (2025) — 集成 15 个基础模型和 18 个数据集的系统化评估平台 (Poulain et al., arXiv)
- **EEG-FM-Bench** (2025) — 标准化数据集、预处理和评估指标 [GitHub](https://github.com/xw1216/EEG-FM-Bench)
- **M-EEG** (2025) — 多中心多模态 EEG 基准，>6,000 名患者 (Chen et al., OpenReview)

### 7.2 开源工具

| 工具 | 语言 | GitHub Stars | 最新版本 | 核心功能 | 链接 |
|------|------|-------------|---------|---------|------|
| **MNE-Python** | Python | ~3,200 | v1.11.0 | 完整 EEG/MEG 处理管线、源定位、统计分析 | [github.com/mne-tools/mne-python](https://github.com/mne-tools/mne-python) |
| **EEGLAB** | MATLAB | ~754 | 2025.1.0 | ICA、DIPFIT、100+ 插件、BIDS 支持 | [github.com/sccn/eeglab](https://github.com/sccn/eeglab) |
| **Braindecode** | PyTorch | ~1,200 | v1.4.0 | 30+ 深度学习模型、MNE 集成、Hugging Face Hub | [github.com/braindecode/braindecode](https://github.com/braindecode/braindecode) |
| **TorchEEG** | PyTorch | ~558 | v1.1.3 | CNN/GNN/Transformer、标准化数据加载与增强 | [github.com/torcheeg/torcheeg](https://github.com/torcheeg/torcheeg) |
| **MOABB** | Python | ~966 | v1.5 | 30+ 数据集上的 BCI 基准测试 | [github.com/NeuroTechX/moabb](https://github.com/NeuroTechX/moabb) |

**工具选择建议**：
- 初次接触 EEG 数据分析 → 从 **MNE-Python** 入手（Python 生态、文档完善、教程丰富）
- 需要深度学习建模 → **Braindecode**（与 MNE 无缝集成）或 **TorchEEG**（更多模型实现）
- 做 BCI 算法基准对比 → **MOABB**（内置 30+ 数据集和标准化评估协议）
- 临床 EEG 分析或使用 MATLAB → **EEGLAB**（最成熟的工具箱，插件生态最丰富）

### 7.3 基础模型代码仓库

| 模型 | GitHub Stars | 链接 |
|------|-------------|------|
| LaBraM | ~590 | [github.com/935963004/LaBraM](https://github.com/935963004/LaBraM) |
| EEGPT | ~280 | [github.com/BINE022/EEGPT](https://github.com/BINE022/EEGPT) |
| BENDR | ~201 | [github.com/SPOClab-ca/BENDR](https://github.com/SPOClab-ca/BENDR) |
| BIOT | ~185 | [github.com/ycq091044/BIOT](https://github.com/ycq091044/BIOT) |
| EEG-FM-Bench | -- | [github.com/xw1216/EEG-FM-Bench](https://github.com/xw1216/EEG-FM-Bench) |
| EEG Foundation Models Collection | -- | [github.com/gayalkuruppu/eeg-foundation-models](https://github.com/gayalkuruppu/eeg-foundation-models) |

---

## 第九部分：研究社区

### 8.1 重要研究组

| 实验室 | 机构 | 负责人 | 研究方向 |
|--------|------|--------|---------|
| **清华大学 BCI 实验室** | 清华大学 | 高小榕 | SSVEP-BCI 世界纪录保持者、BETA 基准数据集 |
| **上交 BCMI 实验室** | 上海交通大学 | 吕宝粮 | SEED 情绪数据集系列、脑电情绪识别 |
| **天津大学神经工程团队** | 天津大学 | 明东 | BCI 系统集成、国产 BCI 平台 |
| **中科院半导体所脑机接口组** | 中科院 | -- | 侵入式/非侵入式 BCI 技术 |
| **华南理工大学 BCI 团队** | 华南理工大学 | 李远清 | 混合 BCI、运动想象 |
| SCCN (Swartz Center) | UC San Diego | Scott Makeig | EEGLAB、移动脑/身体成像、ICA |
| Graz BCI Lab | TU Graz, 奥地利 | Gernot Muller-Putz | 运动想象 BCI 先驱 |
| Gotman Lab | McGill University | Jean Gotman | 癫痫 EEG、HFO 检测 |
| INRIA MIND/TAU | INRIA, 法国 | A. Gramfort et al. | MNE-Python、Braindecode、源定位 |
| NeuroTechX | 国际社区 | 社区驱动 | MOABB、开源神经技术 |
| Sajda Lab | Columbia University | Paul Sajda | 神经工程、EEG 认知监测 |
| He Lab | Carnegie Mellon | Bin He (贺斌) | 非侵入式 BCI、源成像 |

### 8.2 竞赛与挑战

| 竞赛 | 年份 | 任务 | 规模 | 链接 |
|------|------|------|------|------|
| **NeurIPS 2025 EEG Challenge** | 2025 | 零样本跨任务解码 + 精神病理预测 | 3,000+ 被试, 128 通道 | [eeg2025.github.io](https://eeg2025.github.io/data/) |
| **HMS Harmful Brain Activity (Kaggle)** | 2024 | 癫痫/有害脑活动分类 | 2,767 队伍, $50K 奖金 | [Kaggle](https://www.kaggle.com/competitions/hms-harmful-brain-activity-classification) |
| **CYBATHLON BCI Race** | 2024 | EEG 控制虚拟角色竞赛 | 国际赛事 | [cybathlon.com](https://cybathlon.com/en/event/disciplines/bci) |
| **BCI Competition IV** | 2008+ | 运动想象、SCP（持续作为基准） | 标准基准 | [bbci.de](https://www.bbci.de/competition/iv/) |
| **BEETL (NeurIPS 2021)** | 2021 | 跨被试/数据集迁移学习 | 30+ 队伍 | [beetl.ai](https://beetl.ai/challenge) |
| **International BCI Award** | 每年 | 最佳 BCI 研究项目 | 总奖金 $6K | [bci-award.com](https://www.bci-award.com/Home) |

### 8.3 相关会议

| 会议 | 方向 | 频率 | 备注 |
|------|------|------|------|
| **IEEE EMBC** | 生物医学工程（最大 EEG 发表平台） | 每年 | EEG 相关论文数量最多的会议 |
| **NeurIPS Brain-AI Workshop** | 脑启发 AI、神经数据 + 深度学习 | 每年 | AI 顶会中最重要的脑科学交叉会场 |
| **IEEE BCI Conference** | 脑机接口技术 | 两年一届 | BCI 专业会议 |
| **OHBM** | 神经影像 (EEG + fMRI + MEG) | 每年 | 方法学与神经科学并重 |
| **SfN** (Society for Neuroscience) | 全领域神经科学 | 每年 | 全球最大神经科学会议 |
| **ICASSP** | 信号处理（含 EEG 专题） | 每年 | 信号处理顶会 |
| **EUSIPCO** | 欧洲信号处理 | 每年 | -- |
| **中国生物医学工程学会年会** | 国内生物医学工程 | 每年 | 国内 EEG/BCI 研究的主要交流平台 |
| **世界机器人大会 BCI 脑控赛** | BCI 竞技 | 每年 | 国内最大规模 BCI 竞赛平台 |

---

## 第十部分：新兴方向 (2025-2027)

### 1. 多模态融合

将 EEG 与 fMRI、MEG 或 fNIRS 通过深度学习进行融合。EEG 提供时间分辨率，fMRI 提供空间分辨率 —— 互补组合有望实现"时空高分辨率"脑成像。

- **"Neural networks and foundation models: two strategies for EEG-to-fMRI prediction"** — 对比经典深度学习管线（MLP、CNN、RNN、Transformer）与基础模型方法（Gemma-2、Llama-3.2）用于从 EEG 预测 fMRI BOLD 信号 (Poulain et al., *Frontiers in Systems Biology*, 2025)
- **"Multi-modal cross-domain self-supervised pre-training for fMRI and EEG fusion"** — 引入 MCSP 框架，实现 EEG 和 fMRI 跨模态跨域的统一预训练 (Zhang et al., *Neural Networks*, 2025)
- **"Multimodal Graph Fusion Network for EEG-fMRI Brain Analysis"** — 使用图神经网络建模多模态 EEG-fMRI 连接 (Liu et al., arXiv, 2025)

### 2. 可穿戴 EEG

可穿戴 EEG 头戴设备市场 2025 年估值 17.5 亿美元，预计 2029 年达 27.8 亿美元 (CAGR 12.4%)。脑传感器正被嵌入耳塞 (IDUN Guardian)、耳机 (Neurable MW75 Neuro)、AR/VR 头显和睡眠面罩中。神经技术投资从 2022 年的 5.82 亿欧元攀升至 2024 年的 20 亿欧元。

关键挑战：信号质量与佩戴便捷性之间的权衡。2026 年的一项开放数据集 (Kok et al., *Scientific Data*) 首次系统对比了四款消费级和一款研究级 EEG 设备。

### 3. 生成模型

扩散模型正在 EEG 领域开辟新的应用场景：

- **"EEGDM: EEG Representation Learning via Generative Diffusion Model"** — 使用结构化状态空间模型作为扩散预训练的主干，捕捉 EEG 时间动态用于表征学习 (Wang et al., arXiv, 2025)
- **"EEGDfus: A Conditional Diffusion Model for Fine-Grained EEG Denoising"** — 条件扩散模型用于精细 EEG 去噪，双分支架构实现更优的伪迹去除 (Li et al., *IEEE TNSRE*, 2025)
- **"Generative modeling and augmentation of EEG signals using improved diffusion probabilistic models"** — 加速 EEG 生成的隐式采样和渐进蒸馏方法，生成的合成数据可提升下游分类器性能 (Kim et al., arXiv, 2024)

应用方向：数据增强（解决小样本问题）、隐私保护型 EEG 数据共享、跨域迁移。

### 4. AI 驱动的神经反馈

实时 AI 神经反馈正在快速发展：2023 年一项 HSE University 研究展示了深度学习滤波器可将延迟降低 50 倍。便携式神经反馈设备市场 2024 年估值 1.56 亿美元，预计 2032 年达 2.89 亿美元 (CAGR 9.2%)。Myndlift 在 2024 年突破了 100 万次远程神经反馈训练。

临床应用已扩展到：PTSD 治疗、ADHD 居家训练、认知增强、冥想辅助。深度学习使得比传统频段功率方法更精细的脑状态检测成为可能。

### 5. 大规模人群 EEG

HBN (3,000+ 被试) 和 UK Biobank（正在增加 EEG 采集）等计划使人群级别的脑研究成为可能。EEG 脑年龄作为公共健康指标。在这些大规模语料上训练的基础模型可能实现"通用" EEG 编码器。

### 6. 隐私与伦理

脑数据引发独特的隐私担忧：神经信号可能泄露认知状态、精神疾病、未说出的想法等敏感信息。法律框架正在形成：

- 智利于 2021 年通过全球首部"神经权利"法案
- 技术解决方案：联邦学习用于 EEG、差分隐私保护脑数据
- 伦理委员会层面：脑数据是否应视为特殊类别的生物数据，目前尚无全球共识

---

## 总结统计

| 类别 | 论文数 | 关键趋势 |
|------|--------|---------|
| 基础模型 | 13 | 规模扩展至 25K+ 被试；Mamba 和 LLM 架构进入 EEG |
| 脑解码 | 13 | 视频重建；EEG-to-Text 的批判性评估 |
| 临床 AI | 14 | 单通道/实时模型；脑年龄作为新兴生物标志物 |
| 脑机接口 | 6 | P300 自监督预训练；SSVEP 混合方法 |
| 神经科学 | 6 | 振荡量化新方法；连接性-意识关联 |
| 数据集/工具 | 8 | 标准化基准平台；消费级设备验证 |
| 新兴方向 | 7 | 扩散模型用于 EEG；LLM 预测 fMRI |
| **总计** | **67** | |

---

## 核心要点

1. **基础模型已成为主导范式**：NeuroLM (1.7B 参数, 25K 小时)、EEGMamba (16.7K 小时)、REVE (25K 被试) 表明规模化正在产生真正的跨任务泛化能力。

2. **批判性评估与热潮同步出现**："Are EEG-to-Text Models Working?" 等论文说明该领域正在成熟，Brain4FMs 和 EEG-FM-Bench 等更严格的基准正在让模型接受真正的检验。

3. **扩散模型解锁跨模态生成**：通过潜在扩散实现的 EEG-to-Image 和 EEG-to-Video 重建 (DreamDiffusion, EEG2Video) 代表了解码表现力的质变飞跃。

4. **临床转化仍是瓶颈**：尽管癫痫/痴呆检测声称准确率超过 99%，但跨中心验证、单通道部署和监管审批仍是未解决的挑战。

5. **消费级硬件正在向研究级靠拢**：Braindecode/TorchEEG 生态系统加上消费级 EEG 验证数据集，预示着 EEG-AI 研究的民主化即将到来。

6. **中国团队在 BCI 和情绪识别领域处于国际前沿**：清华大学保持着 SSVEP-BCI 速度世界纪录，上交 BCMI 实验室的 SEED 系列是情绪识别领域被引用最多的数据集之一。

---

## 贡献

这是一份持续更新的文档。欢迎通过 Pull Request 贡献内容。添加论文时请附上完整引用信息。

## 许可证

本综述采用 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) 许可证发布。

---

*综述编撰于 2026-04-10。如果你觉得有用，请为仓库加星。*
