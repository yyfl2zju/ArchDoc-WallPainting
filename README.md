# ArchDoc-WallPainting

**首个面向考古文档壁画提取的图文关联与精细分割基准数据集**

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)

## 📖 简介

ArchDoc-WallPainting 是一个专为 **"阅读以观"（Reading to See）** 计算范式设计的基准数据集，旨在解决考古文档中壁画图像与语义描述之间的"物理隔离"问题。

在数字人文与计算考古学领域，海量扫描版考古报告中蕴藏着珍贵的壁画图像及其专家解读。然而，文档复杂的版面结构导致视觉证据（壁画图像）与语义描述（图注、正文）在物理空间上分离，使这些知识处于"可见而不可用"的状态。

本数据集支持两阶段深度学习框架 **LACA-Net** 的训练与评估：
1. **Stage 1**: 版面分析与图文匹配 — 将图注与对应壁画区域进行逻辑关联
2. **Stage 2**: 文本引导精细分割 — 基于图注语义实现像素级壁画主体提取

## 📊 数据集概览

| 阶段 | 子集 | 规模 | 数据来源 | 任务 |
|------|------|------|----------|------|
| Stage 1 | synth | 5,000 页 / 12,468 壁画 | muralDH1714 + VLM | 图文匹配训练 |
| Stage 1 | real | 383 页 / 397 壁画 | 《中国出土壁画全集》 | 图文匹配测试 |
| Stage 2 | clean | 584 壁画 | 多来源 | 简单场景 |
| Stage 2 | dirty | 397 壁画 | 多来源 | 精细分割 |

**总计**: 5,383 页文档，13,846 张壁画标注

## 📁 目录结构

```
ArchDoc-WallPainting/
├── README.md                       # 本文件
├── stage1/                         # 阶段1：版面分析与图文匹配
│   ├── README.md
│   ├── synth/                      # 合成数据（训练）
│   │   ├── annotations/
│   │   ├── images/
│   │   └── pages/
│   └── real/                       # 真实数据（测试）
│       ├── annotations/
│       ├── images/
│       └── pages/
│
└── stage2/                         # 阶段2：文本引导分割
    ├── README.md
    ├── clean/                      # 干净壁画
    │   ├── annotations/
    │   └── images/
    └── dirty/                      # 需分割壁画
        ├── annotations/
        ├── images/
        └── mattes/
```

## 📝 标注格式

所有标注采用 JSON 格式：

```json
{
  "caption": "壁画描述性图注（含名称、年代、尺寸、出土信息等）",
  "bbox_in_page": [x1, y1, x2, y2],
}
```

## 🔬 研究背景

### 核心挑战

1. **结构-语义两难困境**: 现有文档版面分析模型缺乏语义理解能力，而指代性图像分割模型在复杂文档上下文中失效
2. **物理隔离特性**: 图注与对应壁画在页面上可能相距甚远，甚至跨页分布
3. **精细边缘保留**: 传统二值掩码难以保留壁画边缘的半透明细节

### 解决方案

**"阅读以观"（Reading to See）范式**：模拟人类专家"先阅读文本理解语境、再定位图像并精细观察"的认知过程。

## 📖 数据来源

| 来源 | 类型 | 说明 |
|------|------|------|
| 《中国出土壁画全集》(10卷) | 真实文档 | 汉代至明清墓室壁画 |
| 《敦煌石窟全集》 | 真实文档 | 敦煌石窟壁画 |
| muralDH1714 | 壁画图像 | 1,714张高质量敦煌壁画 |
| GLM4v-flash | 图注生成 | VLM自动生成描述性图注 |


## 📄 引用

如果本数据集对您的研究有帮助，请引用：

```bibtex
@misc{archdoc-wallpainting,
  title={ArchDoc-WallPainting: A Benchmark Dataset for Caption-Mural Association and Fine-grained Segmentation in Archaeological Documents},
  author={},
  year={2025},
  howpublished={\url{https://github.com/yyfl2zju/ArchDoc-WallPainting}}
}
```

## 📧 联系方式

如有问题或建议，请通过以下方式联系：
- GitHub Issues: [提交问题](https://github.com/yyfl2zju/ArchDoc-WallPainting/issues)

---

**关键词**: 文档理解 | 壁画分割 | 图文匹配 | 数字人文 | 计算考古学 | Alpha Matting
