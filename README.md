# 单细胞/空间转录组数据库与多组学分析实战项目

本项目面向单细胞和空间转录组生信分析，从 Seurat/R 生态体系出发，演示如何将多个主流数据集（包括**pbmc3k**、**bmcite**、**stxBrain** 等）全流程分析后存储到 SQLite 数据库，并用 SQL 灵活查询/分析，同时涵盖多组学、空间、差异表达与功能富集等核心环节。

---

## 目录

- [项目简介](#项目简介)
- [依赖环境](#依赖环境)
- [主要分析流程与模块](#主要分析流程与模块)
  - [1. PBMC3K 数据集分析](#1-pbmc3k-数据集分析)
  - [2. bmcite 多组学数据分析](#2-bmcite-多组学数据分析)
  - [3. stxBrain 空间转录组分析](#3-stxbrain-空间转录组分析)
  - [4. SQL 数据管理与复杂查询](#4-sql-数据管理与复杂查询)
  - [5. 差异表达与功能富集分析](#5-差异表达与功能富集分析)
  - [6. 多组学联合降维与marker分析](#6-多组学联合降维与marker分析)
- [主要输出与可视化](#主要输出与可视化)

---

## 项目简介

- **涵盖数据类型**：常规单细胞（PBMC）、多组学（CITE-seq，bmcite）、空间转录组（stxBrain）
- **分析亮点**：全流程R分析、数据库化、SQL操作、空间可视化、多组学降维与联合marker、功能富集

---

## 依赖环境

- **R >= 4.1**
- 推荐 IDE：RStudio
- 主要R包：

  ```r
  install.packages(c("Seurat", "SeuratData", "DBI", "RSQLite"))
  BiocManager::install(c("clusterProfiler", "org.Hs.eg.db"))
## 主要分析流程与模块

### 1. PBMC3K 数据集分析

- 加载数据（`data("pbmc3k")`），更新对象
- 提取表达矩阵与元信息，长表转化
- 写入 SQLite，创建 `metadata`/`expression` 表
- SQL 查询：细胞类型分布、marker基因、分组聚合
- 差异表达与功能富集分析
- 查询结果导出，可视化统计

### 2. bmcite 多组学数据分析

- 加载 CITE-seq 数据（`data("bmcite")`），提取 RNA/蛋白等多组学矩阵
- 分别写入 SQLite，不同组学单独成表（如 `rna_expression`/`adt_expression`）
- 多组学联合降维（如WNN）、联合marker分析
- SQL 支持单组学或跨组学联合查询
- 多组学差异表达与富集，联合可视化

### 3. stxBrain 空间转录组分析

- 加载空间数据（`data("stxBrain")`），兼容空间坐标与元注释
- 空间坐标、表达量与元信息写入 SQLite
- SQL 查询空间区域细胞类型、marker、空间分布
- 支持空间特异性差异表达、富集、空间可视化

### 4. SQL 数据管理与复杂查询

- 元信息、表达量等全流程关系型结构化存储
- SQL 实现多表联合、分组、筛选、排序、表达聚合等
- 支持任意类型/组学/空间/时间的定制查询

### 5. 差异表达与功能富集分析

- 结合 SQL 查询输出结果与R下游分析（如 `FindMarkers`, `clusterProfiler`）
- 各细胞亚群/空间区域/组学的marker与功能条目自动整理
- 可一键生成富集气泡图/条形图

### 6. 多组学联合降维与marker分析

- 如CITE-seq联合降维（WNN等）
- 跨组学marker/亚群/功能注释的整合
- 联合降维坐标/marker/注释写入数据库

## 主要输出与可视化

- 每个数据集/分析环节对应的数据库文件（sqlite）
- 典型 SQL 查询与分析结果（可表格、导出、可视化）
- 多组学、空间、差异表达、富集等结果图（气泡图、空间分布图等）