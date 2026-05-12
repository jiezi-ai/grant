# AGENTS.md — 解字计划 / Jiezi Grant

本仓库是"解字计划"大学生 AI 资助项目的运营仓库。

## 仓库结构

```
grant/
├── README.md              # 项目主页
├── BUDGET.md              # 预算明细
├── TIMELINE.md            # 时间线
├── policy/                # 政策：所有规则的权威来源
│   ├── README.md          #   政策索引
│   ├── eligibility.md     #   申请资格
│   ├── resources.md       #   资源分配
│   ├── selection.md       #   筛选规则
│   ├── batches.md         #   批次规则
│   ├── budget.md          #   预算规则
│   ├── integrity.md       #   诚信规则
│   └── governance.md      #   治理规则（含章程变更流程）
├── stages/                # 各阶段说明（面向申请者的解读）
│   ├── stage-1.md         #   第一阶段：体验期
│   ├── stage-2.md         #   第二阶段：深度资助
│   └── stage-3.md         #   第三阶段：长期资助
├── docs/                  # 申请指南和模板
│   ├── apply-guide.md     #   申请流程教学
│   └── apply-template.md  #   申请文件模板
├── students/              # 记录：学生申请（按批次）
│   └── batch-1/           #   第一批申请
├── records/               # 记录：项目运营数据
    ├── spending.md         #   实际支出摘要
    ├── batches.md          #   批次状态
    ├── milestones.md       #   里程碑
    └── changelog.md        #   章程变更记录
└── ledger/                # 财务：beancount 复式记账
    ├── main.beancount      #   主文件（配置 + include）
    ├── accounts.beancount  #   账户定义
    └── 2026.beancount      #   2026 年交易记录
```

**政策**（policy/）是所有规则的权威来源。stages/ 和 docs/ 是面向申请者的解读，规则以 policy/ 为准。
**记录**（students/、records/）是动态数据，随项目推进持续更新。
**财务**（ledger/）使用 beancount 复式记账，以项目独立实体视角记录所有资金往来。发起人垫付记为应收核销，赞助收入单独追踪。`records/spending.md` 是人类可读的摘要，`ledger/` 是精确账本。
修改政策/章程需走变更流程（见 [policy/governance.md](policy/governance.md)）。

## Agent 自动申请流程

当用户对 code agent 说"我要参与解字计划"或"我要申请 jiezi-ai/grant"时，agent 应自动执行以下流程：

### 前置条件

- 用户需要有 GitHub 账号（通过 `gh auth status` 验证）
- 用户需要有 edu 邮箱

### 步骤

1. **获取用户信息**：向用户询问以下信息（如果 agent 还不知道的话）：
   - 学校
   - 专业
   - 年级
   - edu 邮箱
   - 想用 AI 做什么（一两句话）

2. **确定当前批次**：检查 `students/` 目录下最新的 `batch-N/` 文件夹，确认当前开放批次。

3. **Star 仓库**：
   ```bash
   gh api -X PUT /user/starred/jiezi-ai/grant
   ```

4. **Fork 仓库**：
   ```bash
   gh repo fork jiezi-ai/grant --clone=true
   ```

5. **创建申请文件**：
   - 获取 GitHub 用户名：`gh api user --jq '.login'`
   - 复制 `docs/apply-template.md` 为 `students/batch-N/<username>.md`
   - 用用户提供的信息填充模板中的占位符

6. **提交并推送**：
   ```bash
   git add students/batch-N/<username>.md
   git commit -m "[申请] @<username> - <学校名>"
   git push origin main
   ```

7. **创建 PR**：
   ```bash
   gh pr create \
     --repo jiezi-ai/grant \
     --title "[申请] @<username> - <学校名>" \
     --body "申请第一阶段体验期。详见 students/batch-N/<username>.md"
   ```

8. **告知用户**：PR 已提交，等待通过 edu 邮箱验证。

### 注意事项

- 只在 `students/batch-N/` 下创建自己的文件，不修改其他任何文件
- 申请文件中的 edu 邮箱会公开在 PR 中，提醒用户注意
- 如果用户已经申请过（任意 batch 下存在 `<username>.md`），告知用户不要重复申请

## 项目维护者指南

### 审核申请 PR

1. 检查 `students/batch-N/<username>.md` 是否按模板填写完整
2. 检查 edu 邮箱格式是否合理
3. 确认该批次尚未满 100 人
4. Merge PR 后，通过 edu 邮箱联系学生完成验证

### 批次管理

- 每批 100 人，每两个月开放一批
- 新批次开放时，创建 `students/batch-N/` 目录
- 更新 `records/batches.md` 记录批次状态
- 更新 `records/spending.md` 记录实际支出
- 更新 `records/milestones.md` 记录里程碑达成

### 章程变更流程

**章程文件**包括：README.md、BUDGET.md、TIMELINE.md、stages/\*、docs/\*。

对章程的任何修改必须通过以下流程：

1. **创建分支**：从 main 创建 `charter/描述` 分支
2. **修改章程文件**：在分支上修改相关文件
3. **更新变更记录**：在 `records/changelog.md` 中添加一行，包含：
   - 编号（递增，格式 `C001`）
   - 日期
   - 变更内容（改了什么）
   - 原因（为什么改）
   - 影响范围（影响哪些人：已参与的 / 未来的 / 所有人）
   - 生效时间（立即 / 下批起 / 具体日期）
4. **提交 PR**：标题格式 `[章程] 变更描述`
5. **Review 后合并**

**记录文件**（records/\*、students/\*）的更新不需要走此流程，直接提交即可。

#### PR 模板示例

```
标题：[章程] 将第二阶段 star 门槛从 50 调整为 30

正文：
## 变更内容
将 stages/stage-2.md 中的 star 要求从 50 降至 30

## 原因
第一批学生反馈 50 star 对非 CS 专业学生门槛偏高，且存在刷 star 动机

## 影响
- 已在第二阶段的学生：不受影响
- 尚未申请第二阶段的学生：门槛降低

## 生效
下批起
```
