# 智能农业监控系统 - GitHub 跟踪日志自动化工具

## 项目概述

`smart-agriculture-monitor-system` 是一个自动化工具，用于为智能农业监控系统生成标准化的 GitHub 问题跟踪日志。该工具能够自动：

1. 爬取 GitHub 仓库中的特定问题（Bug）和 PR
2. 生成三类标准化文档：
   - 传感器变更日志 (`sensor_change_log.md`)
   - 模型迁移指南 (`model_migration.md`)
   - 故障分析报告 (`failure_analysis.md`)
3. 管理文档分支 (`docs/agri-tracking-logs`)
4. 确保文档符合格式规范和数据一致性要求

## 主要功能

### 1. 数据爬取
- 自动筛选已关闭的 Bug 问题（标签：`传感器数据异常`、`灌溉控制失败`、`环境告警错误`）
- 自动筛选待合并的 PR（标签：`作物生长模型优化`、`灌溉算法升级`、`数据采集协议更新`）
- 提取专属字段：设备ID、区域归属（温室/大田）、固件版本

### 2. 文档生成
- **传感器变更日志**：记录设备修复历史，格式：`日期｜设备ID｜区域｜描述`
- **模型迁移指南**：按环境监测/灌溉控制/作物分析模块组织适配指南
- **故障分析报告**：包含异常现象、根因定位和技术优化方案

### 3. 分支管理
- 自动创建/检测文档分支：`docs/agri-tracking-logs`
- 确保文档安全隔离和历史记录保护

### 4. 合规校验
- 格式规范：中文日期、区域分类标识（温室区域/大田区域）
- 数据一致性：文档内容与 GitHub 问题/PR 字段完全匹配
- 操作白名单：仅允许操作指定文件

## 使用说明

### 前置要求
- Python 3.8+
- GitHub 个人访问令牌（需 `repo` 权限）
- 目标仓库：`smart-agriculture-monitor-system`

### 安装步骤
```bash
# 克隆仓库
git clone https://github.com/linluo67/smart-agriculture-monitor-system.git
cd smart-agriculture-monitor-system

# 安装依赖
pip install -r requirements.txt
```

### 配置环境
1. 创建 `.env` 文件并添加 GitHub Token：
   ```
   GITHUB_TOKENS=your_personal_access_token_here
   ```

### 运行脚本
```bash
python github_agri_tracking_generator.py
```

### 输出文档
脚本将在 `docs/agri-tracking-logs` 分支生成以下文件：
```
docs/agri-tracking-logs/
├── sensor_change_log.md
├── model_migration.md
└── failure_analysis.md
```

## 文档规范

### 传感器变更日志 (`sensor_change_log.md`)
- 格式：`2025年09月15日 | 设备ID：AGRI-20250915-003 | 温室区域 | 修复描述`
- 要求：
  - 单行不超过100字符
  - 必须包含日期、设备ID、区域和描述
