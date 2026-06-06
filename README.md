# 蛊真人 TRPG 规则系统 (Gu Zhen Ren / Reverend Insanity TTRPG)

基于《蛊真人》原著小说全文拆解、逐章检索后编写的**单人硬核跑团规则**。共30个JSON文件，适配LLM全自动主持。

## 核心特点

- **原著驱动**：所有规则、数据、设定均来源于《蛊真人》全六卷、2335节、22万行原文的关键词检索与段落摘录，不凭空编造
- **适配LLM**：JSON结构化，AI主持人可模块化按需加载，不占用过量上下文
- **硬核还原**：完整九转体系、真元颜色表、空窍窍壁进化、三气升仙、道痕互斥、灾劫系统——忠实还原小说设定
- **单人跑团**：AI全自动主持，涵盖角色创建/蛊虫炼化/战斗/成长/世界探索的完整循环

## 数据规模

| 内容 | 数量 |
|------|------|
| 仙蛊（六转至九转） | 125+ 只，分16个流派 |
| 凡蛊（一转至五转） | 70+ 只，含效果/消耗/饲养 |
| 流派/道途 | 二十二道 |
| 五域+两天地理 | 完整覆盖 |
| 开局模组 | 5个（南疆/北原/中洲/东海/西漠） |
| AI主持工具 | 6张随机表 + 10种任务类型 + 动态难度系统 |

## 文件结构

```
蛊真人跑团规则/
├── index.json                     # 总索引与加载指南
├── core_rules.json                # 核心引擎（d100判定/属性/技能/回合）
├── rank_advancement.json          # 九转体系（突破条件/真元表/灾劫）
├── character/
│   ├── template.json              # 角色卡 Schema（含古月方源示例）
│   ├── aptitudes.json             # 资质系统（甲乙丙丁 + 十绝体）
│   ├── origins.json               # 出身系统（五域两天 × 六类出身）
│   ├── paths.json                 # 二十二流派 + 流派协同
│   └── special_identities.json    # 穿越者/重生者可选规则
├── gu_system/
│   ├── encyclopedia.json          # 凡蛊百科（70+只，按转数分类）
│   ├── immortal_gu.json           # 仙蛊百科（125+只，16流派分类）
│   ├── crafting.json              # 炼蛊规则（单炼/合炼/逆炼/喂养）
│   └── killer_moves.json          # 杀招系统（核心蛊+辅助蛊+反噬）
├── combat/
│   ├── mechanics.json             # 战斗机制（回合制/真元消耗/伤害）
│   ├── injuries.json              # 伤势系统（肉身+魂魄双轨HP）
│   └── formations.json            # 蛊阵系统
├── world/
│   ├── regions.json               # 五域+两天完整地理
│   ├── factions.json              # 势力全览（正道/魔道/散修）
│   ├── economy.json               # 经济系统（元石/宝黄天）
│   └── timeline.json              # 青茅山时代时间线
├── gm_engine/
│   ├── oracle.json                # 6张随机表（遭遇/天气/NPC/掉落）
│   ├── narrative.json             # AI叙事风格约束（黑暗/智斗/不圣母）
│   ├── challenge_builder.json     # 动态难度生成
│   └── quest_generator.json       # 任务自动生成
├── scenarios/
│   ├── start_nanjiang.json        # 南疆开局（青茅山/白骨山）
│   ├── start_beiyuan.json         # 北原开局（部族/王庭之争）
│   ├── start_zhongzhou.json       # 中洲开局（十大古派/天庭）
│   ├── start_donghai.json         # 东海开局（海岛/鲛人/海商）
│   ├── start_ximo.json            # 西漠开局（绿洲/商队/沙狼城）
│   └── events_random.json         # 通用随机事件库
└── reference/
    └── terminology.json           # 50+专有术语释义
```

## 制作流程

```mermaid
graph LR
    A[原著23MB TXT] -->|结构分析| B[拆分为6卷MD]
    B -->|关键词检索| C[并行Agent提取规则相关段落]
    C -->|带回原文行号| D[编写JSON规则]
    D -->|交叉验证| E[30个JSON文件]
```

1. **拆分原著**：将22万行TXT按六大卷（魔道/逆天/北原/争天/魔王雄霸/魔尊永生）拆分为6个Markdown文件
2. **关键词检索**：5个并行Agent对全六卷执行覆盖性检索——九转体系、资质系统、蛊虫机制、战斗规则、地理势力、经济等14个主题
3. **规则编写**：每条规则/数据均带有原著卷号+行号出处标注，不凭空编造
4. **交叉验证**：JSON语法校验通过，所有文件可被Python `json.load()` 正常解析

## 使用方式

### 作为LLM的规则引擎

将本文件夹中的所有JSON作为上下文喂给任意支持长上下文的LLM，LLM即可作为GM主持跑团：

```
加载顺序：index.json → core_rules.json → character/template.json → world/regions.json → scenarios/start_XXX.json → gu_system/encyclopedia.json
```

根据游戏进行中遇到的情况动态加载相应模块（战斗时加载combat/、炼蛊时加载gu_system/crafting.json）。

### 适配平台

- **任意Agent**：直接作为system prompt + 规则上下文加载
- **酒馆/SillyTavern**：转换为World Info / Lorebook格式导入
- **Dify/Coze**：作为知识库RAG检索
- **自定义前端**：可配合LLM API构建交互式终端跑团

## 世界观设定

时代设定为与主角古月方源同期的**青茅山时代**（早期），玩家从一转初阶起步。但出身地域可任选五域两天，不局限于青茅山。支持长期跑团，从一转凡人到九转尊者均有完整规则覆盖。

## 免责声明

本项目为同人作品，基于网络小说《蛊真人》（作者：蛊真人）的世界观制作。所有规则数据均来源于对原著文本的拆解分析。本项目与原作者无关，仅用于跑团游戏娱乐。

## License

MIT
