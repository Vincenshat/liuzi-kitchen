# 留子厨房

一个为海外留学生设计的动态厨房 Skill。

它不是一本静态菜谱，也不是“番茄炒蛋第 1 步、第 2 步”的复读机。留子厨房的目标，是让 Agent 像一个真正懂留学生活的人一样工作：先问清你的预算、厨房、身体需求和冰箱库存，再结合食品安全、健康合理性、全球菜系、社区攻略和真实采购成本，给出能买、能做、好吃、划算、可持续的方案。

一句话概括：

> 在有限预算、有限厨具、有限时间里，把“今天到底吃什么”变成一个安全、美味、健康、性价比清楚的决策。

## 为什么需要它

留学生做饭的难点往往不是“不知道菜谱”，而是：

- 超市太多：Aldi、Walmart、Costco、Trader Joe's、亚洲超市，到底去哪买？
- 攻略太乱：小红书说这个最划算，Reddit 说那个更便宜，知乎又有另一套经验。
- 厨房太现实：一个锅、一口锅、共用冰箱、没车、没烤箱、没有那么多调料。
- 食材会坏：买多了浪费，买少了不够吃，大包装便宜但没地方冻。
- 安全不能赌：鸡肉、海鲜、剩饭、解冻、复热、交叉污染都不是玄学。
- 健康因人而异：高蛋白、少盐、少糖、素食、孕期、过敏、训练、控糖、肠胃敏感，答案都不一样。

所以这个 Skill 的核心不是“给一道菜”，而是做动态判断：看你是谁、在哪里、有什么、能买什么、现在饭做成什么样，然后给下一步。

## 核心能力地图

| 模块 | 它解决什么 | 产出 |
|---|---|---|
| `Recommend / 推荐` | 不知道吃什么 | 按预算、健康、口味、厨具推荐 3-7 道菜 |
| `Plan / 计划` | 想做一日/一周饭 | 菜单、备餐顺序、储存复热、食材复用 |
| `Shop / 买菜` | 不知道买多少、去哪买 | 具体采购量、店铺分区、包规调整、替换方案 |
| `Scout / 攻略侦察` | 想读小红书/知乎/Reddit/店铺攻略 | 来源矩阵、价格校验、横向对比、最终建议 |
| `Cook-Live / 做饭中救场` | 做到一半出问题 | 太咸、太淡、太辣、糊底、水多、没熟、缺材料的即时处理 |
| `Reuse / 剩菜再创造` | 冰箱里有剩菜和边角料 | 安全检查后的二次创作：饭碗、汤面、卷饼、炒饭、炖菜 |

## 动态工作流

留子厨房默认按这条链路思考：

```text
用户需求
  -> 个人限制和厨房条件
  -> 食品安全闸门
  -> 健康合理性检查
  -> 菜系和口味选择
  -> 采购量与性价比计算
  -> 社区攻略和店铺信息校验
  -> 最小可执行方案
  -> 做饭中动态救场或剩菜再利用
```

它会优先问这些问题：

- 几个人、几顿饭、饭量大不大？
- 有没有过敏、不耐受、宗教/文化饮食限制？
- 健康目标是什么：均衡、高蛋白、少盐、少糖、控糖、心血管友好、训练、孕期、肠胃友好？
- 有什么厨具：炉灶、微波炉、电饭锅、烤箱、空气炸锅、冰箱/冷冻？
- 预算多少、能去哪家店、有没有车或会员？
- 冰箱和调料里现在有什么？
- 想吃什么菜系，能接受多辣，愿意做多久？

如果用户没时间回答，它会采用保守默认值：美国超市环境、低到中预算、一锅一锅可做、食品安全优先、健康均衡、不假设用户没有过敏。

## 真正的性价比：不只看价格

留子厨房的“划算”不是单纯选最便宜，而是做横向比较：

| 维度 | 为什么重要 |
|---|---|
| 每份成本 | 总价要除以真实可吃的份数 |
| 单位价格 | 不同店可能用 lb、oz、g、pack，必须统一 |
| 时间成本 | 排队、交通、洗切、清理也算成本 |
| 损耗风险 | 大包装便宜，但坏掉就是亏 |
| 复用率 | 同一个食材能跨 3 道菜才是真划算 |
| 食品安全 | 生肉、海鲜、剩饭、冷链和复热都要算风险 |
| 健康适配 | 低价但高钠、低蛋白、没蔬菜，不一定适合你 |
| 口味坚持度 | 再便宜，不想吃也会变成浪费 |
| 来源可信度 | 小红书/知乎/Reddit/店铺页面需要分层验证 |

对应脚本：

```bash
python scripts/value_compare.py --option "Aldi tofu bowls|9.50|4|35|5|1|3" --option "Costco chicken prep|24.00|10|90|4|2|4" --option "Takeout lunch|13.00|1|10|1|1|1" --lang zh-en
```

## 攻略侦察：读社区，但不盲信社区

当用户要求参考小红书、知乎、Reddit、博客、店铺页面或截图时，Skill 会进入 `Scout / 攻略侦察` 模式。

它会把攻略拆成结构化证据：

- 来源：平台、链接、作者/社区
- 时间：是不是近期信息
- 地点：是否适用于用户所在城市或国家
- 价格：总价、单位价格、包规、份数
- 条件：会员、车程、冷冻空间、厨具、优惠券
- 隐形成本：交通、排队、一次性调料、损耗
- 风险：食品安全、过敏、高钠、高糖、高脂
- 可信度：官方店铺页、多源一致、单一经验帖、旧帖分别处理

如果小红书或知乎内容无法公开访问，它不会假装读过，而是会要求用户提供链接、截图或粘贴文本。Reddit 和公开网页则优先读取近期帖和店铺页面，并用官方价格或安全信息交叉校验。

## 食品安全底线

留子厨房会强制执行食品安全检查：

- 肉类、禽类、鱼、蛋类、剩菜必须有安全温度或处理规则。
- 生熟分开，避免切菜板、盘子、手和调料瓶交叉污染。
- 不建议室温解冻；优先冰箱、冷水密封或微波后立刻烹饪。
- 剩菜 2 小时内冷藏，高温环境 1 小时内冷藏。
- 剩菜复热到 `165 F / 74 C`。
- 孕期、免疫低下、老人、儿童等高风险人群使用更保守建议。

它不会承诺“绝对安全”，但会把安全风险显式检查出来，避免把高风险步骤藏在菜谱里。

## 健康合理性检查

健康建议不是一刀切。Skill 会根据用户目标调整：

- 均衡饮食：蛋白质 + 蔬菜/水果 + 主食 + 适量脂肪
- 高蛋白：鸡蛋、豆腐、豆类、鸡肉、鱼、希腊酸奶等
- 少盐：减少酱油、高汤粉、加工肉，用酸味和香料补味
- 少糖：减少甜饮和甜酱，避免把糖当主调味
- 控糖友好：更重视纤维、蛋白质、无糖饮品和碳水搭配
- 心血管友好：关注蔬菜、豆类、鱼、全谷物、钠和饱和脂肪
- 素食/纯素：主动补蛋白，并提醒 B12 等需要专业建议
- 过敏：筛查美国九大过敏原，包括芝麻

对应脚本：

```bash
python scripts/meal_check.py --ingredients "chicken,rice,broccoli,soy sauce,sesame oil" --allergies sesame --protein chicken --veg yes --starch rice --risk none --goal balanced --sodium moderate --lang zh-en
```

## 全球菜系支持

留子厨房不是只会中餐。它支持把全球菜系转成留学生厨房能执行的版本：

- 中式与地方风味
- 日式/韩式
- 东南亚
- 南亚
- 地中海
- 中东与北非
- 墨西哥与拉美
- 非洲与加勒比
- 美式与欧洲家常

每个菜系不是只列菜名，而是拆成：

- 风味底层逻辑：香味、咸鲜、酸味、脂肪、口感
- 留学生友好菜：少工具、少时间、少浪费
- 采购包：核心调味和高复用食材
- 安全提醒：肉类、蛋类、海鲜、剩菜的处理方式
- 替换方案：买不到或预算不够时怎么换

## 买菜量计算

生成具体购物量：

```bash
python scripts/grocery_planner.py --servings 2 --meals 4 --profile budget --protein beans --starch tortillas --veg mixed --cuisine mexican-latin --lang zh-en
```

它会输出：

- 覆盖几餐、几份
- 蛋白质、主食、蔬菜、调味、油的数量
- 菜系调味包
- 菜品方向
- 食品安全提示
- 健康合理性提示
- 性价比提示

## 项目结构

```text
liuzi-kitchen/
├── SKILL.md                         # Skill 核心流程和触发说明
├── README.md                        # 项目说明
├── agents/
│   └── openai.yaml                  # Skill UI 元数据
├── assets/
│   └── icon.svg                     # 自生成图标
├── references/
│   ├── dynamic-cooking.md           # 动态救场、替换、库存、剩菜
│   ├── flavor-budget.md             # 调味纠偏和性价比策略
│   ├── food-safety.md               # USDA/FDA 食品安全规则
│   ├── global-cuisines.md           # 全球菜系和留学生友好菜
│   ├── health-checks.md             # 过敏和健康合理性检查
│   ├── meal-catalog.md              # 基础菜品模板
│   └── social-intel.md              # 社区攻略研究和横向对比
└── scripts/
    ├── grocery_planner.py           # 中英双语采购量计算
    ├── meal_check.py                # 食品安全和健康 PASS/WARN/FAIL 检查
    └── value_compare.py             # 真性价比横向比较
```

## 安装

通过 GitHub URL 安装：

```bash
npx skills install https://github.com/Vincenshat/liuzi-kitchen
```

或者把本目录放到 Codex skills 目录：

```text
~/.codex/skills/liuzi-kitchen
```

## 使用示例

```text
Use $liuzi-kitchen to plan 5 cheap, healthy, bilingual dinners for one student with a rice cooker and one pan.
```

```text
Use $liuzi-kitchen. I have eggs, tofu, cabbage, rice, kimchi, and soy sauce. Make dinner and tomorrow's lunch.
```

```text
Use $liuzi-kitchen. My stir-fry is too salty and watery. Tell me what to do next.
```

```text
Use $liuzi-kitchen to compare Xiaohongshu, Zhihu, Reddit, and store-page advice for the best-value groceries near me.
```

## 边界

留子厨房提供的是实用饮食规划，不是医学诊断，也不是个人医疗营养治疗。

如果用户涉及孕期、免疫低下、肾病、糖尿病、心血管疾病、严重食物过敏、进食障碍史、药物相互作用等高风险情况，Skill 会采用保守饮食建议，并建议咨询医生或注册营养师。

## English Summary

Liuzi Kitchen is a dynamic bilingual kitchen skill for international students. It goes beyond static recipes by combining intake questions, food-safety gates, health checks, grocery math, social-guide research, global cuisine planning, cooking rescue, and leftover transformation.

It supports six core modes:

1. `Recommend` - dish ideas across cuisines and constraints.
2. `Plan` - meal plans with prep, storage, and reheating.
3. `Shop` - concrete grocery quantities and value swaps.
4. `Scout` - Xiaohongshu/REDnote, Zhihu, Reddit, blog, and store-page research with horizontal comparison.
5. `Cook-Live` - real-time cooking rescue.
6. `Reuse` - safe leftover and pantry transformation.

Install:

```bash
npx skills install https://github.com/Vincenshat/liuzi-kitchen
```

## Sources

- USDA FSIS Safe Minimum Internal Temperature Chart
- USDA FSIS Food Thermometers
- FDA Safe Food Handling
- FDA Food Allergies
- Dietary Guidelines for Americans
- USDA MyPlate
