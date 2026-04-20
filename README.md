# 生物样本库 & 医疗新技术日报生成器

## 📋 项目简介

自动从 PubMed 和 Bing 搜索收集生物样本库 (Biobank) 和医疗新技术相关信息，生成格式化的 HTML 日报，并通过邮件发送。

**功能特性：**
- ✅ 从 PubMed API 获取生物样本库研究文献
- ✅ 从 Bing 搜索获取国内医疗新技术信息
- ✅ 生成美观的 HTML 格式日报
- ✅ 自动邮件发送功能
- ✅ GitHub Actions 定时任务（每天早上 7 点）
- ✅ 自动保存日报到仓库

## 🚀 快速开始

### 本地运行

1. **克隆仓库**
```bash
git clone https://github.com/dq47dmc5hg-del/testlueluelue.git
cd testlueluelue
```

2. **安装依赖**
```bash
pip install -r requirements.txt
```

3. **运行脚本**
```bash
python daily_report_generator.py
```

生成的 HTML 报告会保存为 `daily_report.html`

### GitHub Actions 自动化设置

#### 第一步：设置邮箱密钥

1. 进入仓库 → **Settings** → **Secrets and variables** → **Actions**
2. 点击 **New repository secret** 创建两个密钥：

**密钥 1: `EMAIL_FROM`**
- 名称：`EMAIL_FROM`
- 值：你的邮箱地址（例如：`your-email@qq.com`）

**密钥 2: `EMAIL_PASSWORD`**
- 名称：`EMAIL_PASSWORD`
- 值：QQ 邮箱授权码（不是密码！）

#### 获取 QQ 邮箱授权码步骤：

1. 登录 [QQ 邮箱](https://mail.qq.com)
2. 点击 **设置** → **账户**
3. 找到 **POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务**
4. 点击 **开启** POP3/SMTP 服务
5. 会生成一个 **授权码**，复制这个授权码作为 `EMAIL_PASSWORD`

#### 第二步：配置工作流时区

编辑 `.github/workflows/daily_report.yml`，根据你的时区调整 cron 表达式：

```yaml
- cron: '0 23 * * *'  # UTC 23:00 = 北京时间 07:00 (UTC+8)
```

**时区转换：**
- 北京时间 07:00 → UTC 23:00 (前一天)
- 北京时间 14:00 → UTC 06:00
- 北京时间 20:00 → UTC 12:00

## 📊 报告格式

生成的 HTML 报告包含以下信息：

```
┌─────────────────────────────────────┐
│   生物样本库 & 医疗新技术日报       │
└─────────────────────────────────────┘

【条目 1】
类目：生物样本库 (Biobank)
标题（中文）：...
标题（英文）：...
摘要：...
信息源：[��接]
日期：2026-04-20

【条目 2】
...
```

**限制：** 最多 20 条信息

## 📁 文件结构

```
.
├── daily_report_generator.py      # 核心脚本
├── requirements.txt               # Python 依赖
├── .github/
│   └── workflows/
│       └── daily_report.yml       # GitHub Actions 工作流
├── daily_report.html              # 生成的报告（自动创建）
└── README.md                       # 本文件
```

## 🔧 自定义配置

### 修改搜索关键词

编辑 `daily_report_generator.py` 中的 `generate_report()` 方法：

```python
def generate_report(self):
    print("🔍 正在收集数据...")
    self.fetch_pubmed_biobank(query="你的关键词", max_results=10)
    self.fetch_bing_medical_tech(query="你的关键词", max_results=10)
    # ...
```

### 修改邮件收件人

编辑 `daily_report_generator.py` 的初始化部分：

```python
def __init__(self):
    # ...
    self.email_recipient = "你的邮箱@qq.com"
```

### 修改最大条目数

```python
def __init__(self):
    # ...
    self.max_items = 20  # 改为你需要的数量
```

## 📧 邮件发送常见问题

### Q: 收不到邮件？
- ✓ 检查 GitHub Secrets 是否正确设置
- ✓ 确认 QQ 邮箱授权码是否正确
- ✓ 检查 GitHub Actions 运行日志查看错误信息

### Q: 授权码错误？
- ✓ 确保复制的是 **16 位授权码**，不是密码
- ✓ 重新生成授权码并更新 Secrets

## 🐛 故障排除

**查看工作流日志：**
1. 进入仓库 → **Actions** 标签
2. 找到 "Daily Biobank & Medical Tech Report" 工作流
3. 点击最新的运行记录
4. 查看 **Generate daily report** 步骤的输出

## 📝 许可证

MIT License

## 💡 未来改进

- [ ] 支持更多数据源（Google Scholar、ArXiv 等）
- [ ] 添加情感分析和热点识别
- [ ] 支持数据库存储历史记录
- [ ] 添加订阅管理功能
- [ ] 支持多语言摘要翻译

---

**需要帮助？** 提交 Issue 或 Pull Request！
