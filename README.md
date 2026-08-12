# unit-cma-lite

**A free, open-source Claude skill that researches Australian apartments like a buyer's agent.**
用买家代理的方法、只用免费公开数据,给澳洲公寓做一份专业级尽调报告。

Give Claude a realestate.com.au / Domain link (or an address), and it produces a structured HTML due-diligence report:

- 🏷️ **A falsifiable price verdict** — anchored to the property's *own* sale history indexed to today, never the vendor's costs
- 🏢 **Land content analysis** — official Valuer General land values, the hidden engine of unit growth
- 📊 **Five-tier comparable sales** on an interactive map, with condition reads (original / updated / renovated)
- 📸 **Before/after renovation photo pairs** mined from past listing campaigns
- 📈 **Market context** from free sources (SQM Research, AreaSearch, ABS), qualitative reads only
- 🚩 **Red flags + an inspection checklist** — because the only true deal-killer is flood; everything else is a price adjustment

## Install 安装

Requires [Claude Code](https://claude.com/claude-code) (or the Claude desktop app with skills support).

```bash
git clone https://github.com/theshuailuo/unit-cma-lite.git
cp -r unit-cma-lite ~/.claude/skills/unit-cma-lite
```

Windows: copy the folder to `C:\Users\<you>\.claude\skills\unit-cma-lite`.

Then in Claude Code:

```
/unit-cma-lite https://www.realestate.com.au/property-apartment-nsw-...
```

or just say **"research this unit"** / **「帮我尽调这个公寓」** with a link.

## What it can't see 局限

Free data has no automated valuations, no year-built/strata-entitlement records, no street-level noise grading. The skill flags every gap honestly and tells you what to verify with the agent, the contract, and your own ears. NSW land values are best supported; QLD/VIC equivalents are linked in the skill.

## Who made this 出品

Methodology by **Shuai Luo**, licensed buyer's agent at [Avocado Wealth](https://avocadowealth.com.au) (Sydney). This is the same decision framework we run with paid data (CoreLogic, HtAG, Stash, SuburbsFinder) for clients — published free because better-informed buyers make better decisions, with or without us.

If you're buying within the next 3 months and want it run professionally: [avocadowealth.com.au](https://avocadowealth.com.au/free-consultation-team?utm_source=github&utm_medium=readme&utm_campaign=unit-cma-lite)

## License

MIT — use, share, adapt. Attribution appreciated.
