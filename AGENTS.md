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
│   └── governance.md      #   治理规则（含章程变更流程 + checkpoint）
├── stages/                # 各阶段说明（面向申请者的解读）
│   ├── stage-1.md         #   第一阶段：体验期
│   ├── stage-2.md         #   第二阶段：深度资助
│   └── stage-3.md         #   第三阶段：长期资助
├── docs/                  # 申请指南
│   └── apply-guide.md     #   申请流程教学
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── apply.yml      #   申请 Issue 模板
├── records/               # 记录：项目运营数据
│   ├── spending.md        #   实际支出摘要
│   ├── batches.md         #   批次状态
│   ├── milestones.md      #   里程碑
│   └── changelog.md       #   章程变更记录
└── ledger/                # 财务：beancount 复式记账
    ├── main.beancount      #   主文件（配置 + include）
    ├── accounts.beancount  #   账户定义
    └── 2026.beancount      #   2026 年交易记录
```

**政策**（policy/）是所有规则的权威来源。stages/ 和 docs/ 是面向申请者的解读，规则以 policy/ 为准。
**记录**（records/）是动态数据，随项目推进持续更新。学生申请数据存储在数据库中，不在仓库文件里。
**财务**（ledger/）使用 beancount 复式记账，以项目独立实体视角记录所有资金往来。
修改政策/章程需走变更流程（见 [policy/governance.md](policy/governance.md)）。

## 申请流程（自动化）

申请通过 jiezi.ai 网站 + GitHub Issue + 自动化 webhook 完成，全程无需人工干预：

```
学生访问 jiezi.ai/apply → 填写信息 → 获得申请码 JZ-XXXX
    ↓
学生到 grant 仓库提交 Issue（内容为申请码）
    ↓
webhook 触发 → 提取申请码 → 匹配数据库 → LLM 审核
    ↓ 通过
自动打 label（approved + batch-N）→ 发验证邮件
    ↓
学生点击验证链接 → 自动打 verified label → 自动关闭 Issue
    ↓
学生添加发起人微信 → 领取 AI Coding Plan
```

个人信息存储在数据库中，Issue 里只有申请码，不暴露隐私。

## Agent 自动申请流程

当用户对 code agent 说"我要参与解字计划"或"我要申请 jiezi-ai/grant"时，agent 应自动执行以下流程：

### 前置条件

- 用户需要有 GitHub 账号（通过 `gh auth status` 验证）
- 用户需要有 edu 邮箱

### 步骤

1. **获取用户信息**：向用户询问以下信息（如果 agent 还不知道的话）：
   - 姓名
   - 学校
   - 专业
   - 年级
   - edu 邮箱
   - 想用 AI 做什么（一两句话）

2. **提交申请表单**：
   ```bash
   curl -X POST https://api.jiezi.ai/api/apply \
     -H "Content-Type: application/json" \
     -d '{"name":"姓名","school":"学校","major":"专业","grade":"年级","edu_email":"邮箱","motivation":"动机"}'
   ```
   返回值中的 `apply_code` 即为申请码。

3. **提交 GitHub Issue**：
   ```bash
   gh issue create --repo jiezi-ai/grant \
     --title "[申请] JZ-XXXX" \
     --body "JZ-XXXX"
   ```

4. **告知用户**：Issue 已提交，等待自动审核。审核通过后验证邮件会发送到 edu 邮箱。

### 注意事项

- 不需要 Fork 仓库或创建文件
- 个人信息通过 API 提交，不出现在 Issue 中
- 如果 API 返回 409，说明该邮箱已有申请记录，告知用户已有的申请码

## 项目维护者指南

### 申请审核

审核完全自动化（LLM + webhook）。维护者只需：
- 监控 Issue 列表，关注 `rejected` 标签的 Issue
- 在 `records/batches.md` 中定期更新批次状态
- 更新 `records/spending.md` 记录实际支出
- 更新 `records/milestones.md` 记录里程碑达成

### 章程变更流程

详见 [policy/governance.md](policy/governance.md)。
