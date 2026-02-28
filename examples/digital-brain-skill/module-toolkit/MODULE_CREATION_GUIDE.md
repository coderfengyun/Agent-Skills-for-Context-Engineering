# Digital Brain - 模块创建指南

本指南提供创建新模块的核心规范和完整流程。

## ⭐ 核心规范 (必须遵守)

### 1. 命名规范

**模块入口文件必须遵循以下命名规则**:

```
✅ 正确: <MODULE>.md  (模块名全大写 + .md)
   示例: PAPERS.md, KNOWLEDGE.md, MODULE-TOOLKIT.md

❌ 错误: README.md, readme.md, Papers.md, papers.md
```

**为什么?**
- 统一性: 所有模块遵循相同命名规范
- 可识别: 大写文件名立即表明这是模块入口文档
- 避免冲突: 不与项目根目录的 README.md 混淆

### 2. 模块入口文件职责

所有模块的入口文件 (`<MODULE>.md`) 必须遵循统一的职责定位:

✅ **标准职责** (参考 identity/IDENTITY.md, content/CONTENT.md):
- 📋 模块概述 (1-2句)
- 📁 文件清单 (标准表格)
- 🎯 使用场景 ("When to Use")
- 📊 数据格式 (完整的JSONL schema)
- 🔄 工作流程 (核心操作步骤)
- 🤖 Agent指令 (`<instructions>` 标签)
- ⚡ 快速命令 (可选)

❌ **不应包含**:
- 详细教程 (放到单独的 GUIDE.md)
- 大量示例 (放到 EXAMPLE.md)
- 开发记录 (放到 SUMMARY.md)
- 过长内容 (入口文件应 100-200行)

### 3. 标准模块入口文件格式

```markdown
---
name: module-name
description: Brief description - what it does, when to use it
---

# Module Name

Brief introduction (1-2 sentences).

## Files in This Module

| File | Format/Type | Purpose |
|------|-------------|---------|
| `file1.jsonl` | JSONL | Description |
| `file2.md` | Markdown | Description |

## When to Use

- **Scenario 1**: When to use file/feature X
- **Scenario 2**: When to use file/feature Y

## Data Schemas

### Schema Name
```json
{
  "field": "description",
  ...
}
```

## Workflows

### Workflow 1: Name
1. Step 1
2. Step 2
3. Step 3

## Agent Instructions

<instructions>
When working with this module:

1. **Rule 1**: Description
2. **Rule 2**: Description
3. **Common operations**: How to perform them

Key points:
- Point 1
- Point 2
</instructions>

## Quick Commands (optional)

```bash
# Common operation 1
command here
```
```

### 4. 必需元素检查清单

- [ ] ✅ YAML前置元数据 (name + description)
- [ ] ✅ Files in This Module 表格
- [ ] ✅ When to Use 章节
- [ ] ✅ Workflows 章节
- [ ] ✅ Agent Instructions (`<instructions>` 标签)
- [ ] ✅ 数据Schema (如果有JSONL文件)

**验证方法**:
```bash
# 检查集成完整性
python module-toolkit/check_module_integration.py <module_name> <keyword>

# 对比标准格式
diff <(head -50 your-module/<MODULE>.md) <(head -50 identity/IDENTITY.md)
```

---

## 📋 6阶段创建流程

### 阶段一: 需求分析与设计 (30分钟)

#### 1. 明确需求
- [ ] 与用户讨论核心需求和期望
- [ ] 确定模块的主要功能
- [ ] 了解用户的工作流偏好
- [ ] 确定数据组织方式

**提问模板**:
- 您期望这个模块解决什么问题?
- 您希望如何组织数据? (格式、结构)
- 您希望记录哪些信息?
- 您希望如何与其他模块集成?

#### 2. 设计数据模型
- [ ] 设计JSONL元数据格式
- [ ] 确定ID命名规则
- [ ] 设计标签体系
- [ ] 设计与其他模块的集成点

---

### 阶段二: 核心文件创建 (2-3小时)

#### 1. 创建模块目录和基础文件

**必需文件**:
```bash
<module_name>/
├── <module>.jsonl         # 核心数据库 (REQUIRED)
└── <MODULE>.md            # 入口文档,大写命名 (REQUIRED)
```

**可选文件** (仅在确实需要时添加):
```bash
<module_name>/
├── TEMPLATE.md            # 仅当内容结构复杂时
└── EXAMPLE.md             # 仅当示例能显著帮助理解时
```

**⛔ 避免创建**:
- ❌ 多个README类文件
- ❌ 开发文档 (SUMMARY.md, COMPLETION_REPORT.md)
- ❌ 超过3个文档文件

**文档大小规范**:
- `<MODULE>.md`: 100-200行
- `TEMPLATE.md`: < 200行
- `EXAMPLE.md`: < 250行
- 总文档量: < 600行/模块

#### 2. 编写模块入口文件

**检查点**:
- [ ] ⭐ 文件名正确: `<MODULE>.md` (全大写)
- [ ] ✅ YAML前置元数据: name + description
- [ ] ✅ 标准章节: Files in This Module, When to Use, Workflows
- [ ] ✅ Agent指令: `<instructions>` 标签
- [ ] ✅ 数据Schema: 如有JSONL,必须完整定义
- [ ] 长度在100-200行之间
- [ ] 职责清晰:是"入口和参考",不是"教程和示例"
- [ ] 与其他模块风格一致

#### 3. 创建自动化脚本 (可选)

**至少需要**:
- [ ] 添加操作脚本 (如 `add_*.py`)
- [ ] 查询操作脚本 (如 `search_*.py`)

**脚本规范**:
- 支持 `--help` 参数
- 错误处理完善
- 输出信息清晰友好

---

### 阶段三: 文档体系完善 (1-2小时)

#### 创建扩展文档 (可选)

**推荐文档**:
- [ ] `EXAMPLE.md` - 完整使用示例
- [ ] `INTEGRATION.md` - 跨模块集成指南

---

### 阶段四: 系统集成 (1-2小时) ⭐ **最重要**

**⚠️ 这是最容易遗漏的部分!**

#### 必需更新的文件

##### ✅ SKILL.md
- [ ] `description` 添加新模块触发词
- [ ] `When to Activate` 添加使用场景
- [ ] `Trigger phrases` 添加触发短语
- [ ] `Module Overview` 更新目录结构
- [ ] `Examples` 添加使用示例

##### ✅ AGENT.md
- [ ] `When User Asks To` 表格添加新命令
- [ ] 添加模块章节和使用指南
- [ ] 如有脚本,添加到自动化列表

##### ✅ README.md
- [ ] 目录结构图添加新模块
- [ ] Quick Start 添加使用示例
- [ ] 自动化脚本列表更新 (如有)

##### ✅ 父模块文档 (如 KNOWLEDGE.md)
- [ ] 添加新子模块说明
- [ ] 更新数据格式描述

#### 验证系统集成完整性

**使用集成检查脚本**:
```bash
python module-toolkit/check_module_integration.py <module_name> <keyword>
```

**期望结果**:
- SKILL.md: ≥5次引用
- AGENT.md: ≥5次引用
- README.md: ≥5次引用
- 集成度: 100%

---

### 阶段五: 跨模块集成 (1-2小时)

#### 1. 设计数据流向

识别新模块与现有模块的关系:
```
示例:
bookmarks → papers (发现)
papers → research (综合)
papers → ideas (启发)
```

#### 2. 创建INTEGRATION.md (可选)

```markdown
# 新模块集成指南

## 🔗 模块间联动

### 模块A → 新模块
**场景**: ...
**数据流**: ...
**示例**: ...

## 🎯 最佳实践
[引用一致性、标签管理等]
```

#### 3. 更新其他模块文档

- [ ] 在相关模块的文档中提及新模块
- [ ] 在notes/research中使用新模块ID格式

---

### 阶段六: 质量保证 (1小时)

#### 1. 功能测试

```bash
# 添加功能测试
python scripts/add_*.py [测试参数]

# 查询功能测试
python scripts/search_*.py --各种参数

# 边界情况测试
# - 空输入
# - 重复ID
# - 无效参数
```

#### 2. 数据一致性检查

- [ ] ID格式统一
- [ ] 日期格式统一 (`YYYY-MM-DD`)
- [ ] 标签命名与其他模块一致
- [ ] JSONL格式正确(每行一个完整JSON对象)

#### 3. 模块入口文件格式验证 ⭐

```bash
# 检查YAML前置元数据
head -5 <module>/<MODULE>.md | grep -E "^---$|^name:|^description:"

# 检查必需章节
grep "## Files in This Module" <module>/<MODULE>.md
grep "## When to Use" <module>/<MODULE>.md
grep "## Workflows" <module>/<MODULE>.md
grep "## Agent Instructions" <module>/<MODULE>.md

# 检查Agent指令标签
grep "<instructions>" <module>/<MODULE>.md

# 对比现有模块格式
diff <(head -30 <module>/<MODULE>.md) <(head -30 identity/IDENTITY.md)
```

**格式检查清单**:
- [ ] ✅ YAML前置元数据存在且格式正确
- [ ] ✅ 包含 "Files in This Module" 章节
- [ ] ✅ 包含 "When to Use" 章节
- [ ] ✅ 包含 "Workflows" 章节
- [ ] ✅ 包含 "Agent Instructions" 章节
- [ ] ✅ 如有JSONL,必须有完整的数据Schema
- [ ] ✅ 文档长度100-200行之间
- [ ] ✅ 与其他模块风格一致

#### 4. 文档链接验证

```bash
# 检查所有内部链接
grep -r "\[.*\](.*.md)" <module>/

# 检查所有脚本引用
grep -r "scripts/" <module>/
```

---

## 🎯 成功标准

### 模块入口文件格式 ✅ ⭐ **最重要**
- [ ] 命名正确: `<MODULE>.md` (全大写)
- [ ] YAML元数据: 包含 name + description
- [ ] 标准章节: Files in This Module, When to Use, Workflows
- [ ] Agent指令: 包含 `<instructions>` 标签
- [ ] 数据Schema: 如有JSONL,必须完整定义
- [ ] 长度合适: 100-200行之间
- [ ] 职责清晰: 是"入口参考",不是"详细教程"
- [ ] 风格一致: 与其他模块格式保持一致

### 功能完整性 ✅
- [ ] 核心功能全部实现
- [ ] 脚本测试通过 (如有)
- [ ] 数据格式统一

### 文档完整性 ✅
- [ ] 所有必需文档存在
- [ ] 文档内容详尽清晰
- [ ] 示例真实可用 (如有)
- [ ] 没有过多冗余文档

### 系统集成 ✅
- [ ] 必需系统文件全部更新 (SKILL.md, AGENT.md, README.md)
- [ ] 集成检查脚本通过 (100%)
- [ ] 每个文件有足够引用

### 质量保证 ✅
- [ ] 所有测试通过
- [ ] 数据格式一致
- [ ] 文档链接有效
- [ ] 模块入口文件格式验证通过

---

## 💡 最佳实践

### 1. 先完成MVP,再扩展功能

**MVP (最小可用产品)**:
- 1个JSONL文件
- 1个`<MODULE>.md`
- 更新3-4个系统文档 (SKILL.md, AGENT.md, README.md, 父模块文档)

### 2. 对比现有模块

参考已有模块的文件结构:
```bash
# 对比文件数量
ls -1 identity/ content/ network/

# 对比文档章节
grep "^##" identity/IDENTITY.md
grep "^##" content/CONTENT.md
```

### 3. 使用检查清单

- 打印本指南作为检查清单
- 逐项完成并标记
- 不要跳过任何步骤

---

## 🔍 常见遗漏检查

### ⚠️ 最容易遗漏的地方

1. **系统集成文件未完全更新** ⭐⭐⭐
   - SKILL.md, AGENT.md, README.md
   - 每个文件需要多处更新

2. **模块入口文件格式不规范** ⭐⭐
   - 使用README.md而非`<MODULE>.md`
   - 缺少YAML前置元数据
   - 缺少`<instructions>`标签

3. **跨模块引用不一致** ⭐⭐
   - ID引用格式不统一
   - 在其他模块文档中未提及新模块

### 集成检查脚本

**使用方法**:
```bash
python module-toolkit/check_module_integration.py <module_name> <keyword>
```

此脚本会检查所有必需文件的集成完整性,确保模块已正确集成到系统中。

---

## 📚 参考资料

### 标准模块示例

查看这些模块了解标准格式:
- `identity/IDENTITY.md` - 身份与声音模块
- `content/CONTENT.md` - 内容创作模块
- `network/NETWORK.md` - 关系管理模块
- `knowledge/KNOWLEDGE.md` - 知识库模块
- `module-toolkit/MODULE-TOOLKIT.md` - 模块工具包

---

## 🔄 持续改进

本指南应该随着每次创建新模块而更新:

1. 记录遇到的新问题
2. 补充新的检查点
3. 优化工作流程
4. 更新标准格式

---

**使用本指南创建新模块,可以确保质量一致性和完整性! ✨**
