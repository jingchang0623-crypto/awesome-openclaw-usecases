# OpenClaw Skill Security Scanner

**工具类型**: 🔐 安全工具  
**作者**: [miaoquai.com](https://miaoquai.com)  
**仓库**: [jingchang0623-crypto/openclaw-skill-security-scanner](https://github.com/jingchang0623-crypto/openclaw-skill-security-scanner)

## 使用场景

当你从 OpenClaw 社区下载 Skills 或自己编写 Skills 时，需要先做安全检查。超过 13.4% 的 Agent 技能市场包含有关键漏洞（参考 [Snyk Agent Scan](https://github.com/snyk/agent-scan)）。

这个工具帮你：
- 检测 SKILL.md 中的 API Keys、Token、私钥泄露
- 扫描危险命令模式（`rm -rf /`, `curl|sh` 等）
- 验证 Skill 结构完整性
- 检查可疑外部链接

## 快速上手

```bash
# 克隆仓库
git clone https://github.com/jingchang0623-crypto/openclaw-skill-security-scanner.git
cd openclaw-skill-security-scanner

# 扫描你的 Skill
python3 openclaw-skill-security-scanner.py ~/.openclaw/skills/my-skill/

# 批量扫描多个 Skills
for skill in ~/.openclaw/skills/*/; do
  python3 openclaw-skill-security-scanner.py "$skill"
done
```

## 输出示例

```
🔐 OpenClaw Skill Security Scan Report
============================================================

📂 Skill: /home/user/.openclaw/skills/my-skill
🎯 Security Score: 85/100
📊 Grade: B (Good)
⚠️  Total Issues: 3

🔴 Issue #1: [CRITICAL] sensitive_api_key
   Message: Found potential api_key in SKILL.md
   Evidence: sk-1234567890abcdef...
   Line: 16
```

## 检测能力

| 检测项 | 模式数量 | 威胁等级 |
|--------|----------|----------|
| API Key (OpenAI, AWS, GitHub等) | 20+ | 🔴 Critical |
| 私钥 (RSA, EC, SSH) | 2 | 🔴 Critical |
| 危险命令 (`rm -rf`, `chmod 777`) | 8 | 🟠 High |
| 恶意链接 (bit.ly, .exe 下载) | 5 | 🟡 Medium |
| 结构完整性 (缺失章节) | - | 🟡 Medium |

## 适用人群

- **Skill 开发者** — 发布前自查
- **企业用户** — 批量检测第三方 Skills
- **安全审计** — 评估 OpenClaw 生态安全
- **学习者** — 了解 Agent Skill 安全隐患

## 灵感来源

- [tech-leads-club/agent-skills](https://github.com/tech-leads-club/agent-skills) (1,244⭐ today) — 专业 Agent 技能注册表
- [Snyk Agent Scan](https://github.com/snyk/agent-scan) — Agent Marketplace 安全扫描
- [12-factor-agents](https://github.com/humanlayer/12-factor-agents) — 生产级 Agent 原则

## 配合使用

与我们系列的 OpenClaw 工具链配合效果最佳：

- [openclaw-skill-linter](https://github.com/jingchang0623-crypto/openclaw-skill-linter) — Skill 语法检查
- [openclaw-skill-quality-analyzer](https://github.com/jingchang0623-crypto/openclaw-skill-quality-analyzer) — Skill 质量分析
- **openclaw-skill-security-scanner** ✅ — *Skill 安全扫描（就是这个）*
- [openclaw-skills-dependency-graph](https://github.com/jingchang0623-crypto/openclaw-skills-dependency-graph) — Skill 依赖分析

---

> 💡 *世界上有两种 Skill，一种是安全的，一种是等着被 hack 的。你不确定是哪种？我帮你查。*

**License**: MIT
