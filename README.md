# 留子厨房 / Liuzi Kitchen

A dynamic bilingual kitchen skill for international students cooking abroad. It helps an agent do more than return static recipes: it asks for personal constraints, reads current community guides when available, adapts to pantry inventory and grocery prices, checks food safety and health fit, recommends global dishes, rescues cooking problems, and turns leftovers into safe next meals.

## What This Skill Covers

- **Dynamic intake** - people, meals, allergies, diet rules, health goals, kitchen equipment, budget, time, spice tolerance, and pantry stock
- **Global cuisine planning** - Chinese, Japanese-Korean, Southeast Asian, South Asian, Mediterranean, Middle Eastern/North African, Mexican/Latin American, African/Caribbean, American, and European home-cooking lanes
- **Food safety checks** - thermometer targets, cross-contamination prevention, safe thawing, leftover timing, reheating, high-risk-user warnings
- **Health checks** - allergy screening, balanced plate review, protein/vegetable/starch/fat fit, sodium/sugar/saturated-fat flags, goal-specific adjustments
- **Grocery math** - concrete quantities by servings and meals, cuisine seasoning kits, value tactics, freezer and package-size thinking
- **Social guide research** - read Xiaohongshu/REDnote, Zhihu, Reddit, blogs, store pages, or user-provided screenshots and turn them into verified comparison tables
- **Horizontal value comparison** - compare options by cost per serving, time, waste risk, reuse, safety, health fit, and source confidence
- **Live cooking rescue** - fixes for bland, salty, watery, burnt, undercooked, overcooked, too spicy, missing-ingredient, or timing problems
- **Leftover and inventory reuse** - safe time-temperature screening plus transformations into rice bowls, soups, wraps, pasta, tacos, fried rice, and stews

## Skill Structure

```text
liuzi-kitchen/
├── SKILL.md                         # Core workflow and mode selection
├── README.md                        # Project overview
├── agents/
│   └── openai.yaml                  # UI metadata
├── assets/
│   └── icon.svg                     # Generated skill icon
├── references/
│   ├── dynamic-cooking.md           # Live rescue, substitutions, inventory, leftovers
│   ├── flavor-budget.md             # Taste correction and value strategy
│   ├── food-safety.md               # USDA/FDA-based safety rules
│   ├── global-cuisines.md           # Global cuisine lanes and student-friendly dishes
│   ├── health-checks.md             # Allergy and health-fit checks
│   ├── meal-catalog.md              # Starter meal templates
│   └── social-intel.md              # Community guide research and horizontal comparison
└── scripts/
    ├── grocery_planner.py           # Bilingual grocery quantity planner
    ├── meal_check.py                # Safety and health PASS/WARN/FAIL checker
    └── value_compare.py             # True-value horizontal comparison
```

## Core Modes

1. **Recommend** - suggest dishes across cuisines for the user's constraints.
2. **Plan** - build a meal plan with prep order, storage, reheating, and substitutions.
3. **Shop** - calculate grocery quantities and value-focused swaps.
4. **Scout** - read current community guides and compare claims against the user's real constraints.
5. **Cook-Live** - diagnose and rescue cooking problems in progress.
6. **Reuse** - transform leftovers and pantry items into safe next meals.

## Installation

Install from a GitHub URL with `skills`:

```bash
npx skills install https://github.com/Vincenshat/liuzi-kitchen
```

Or place this folder under your Codex skills directory:

```text
~/.codex/skills/liuzi-kitchen
```

## Usage

Invoke the skill directly:

```text
Use $liuzi-kitchen to plan 5 cheap, healthy, bilingual dinners for one student with a rice cooker and one pan.
```

Other useful prompts:

```text
Use $liuzi-kitchen. I have eggs, tofu, cabbage, rice, kimchi, and soy sauce. Make dinner and tomorrow's lunch.
```

```text
Use $liuzi-kitchen. My stir-fry is too salty and watery. Tell me what to do next.
```

```text
Use $liuzi-kitchen to make a Mexican/Latin grocery list for 4 meals, high-protein, low budget.
```

```text
Use $liuzi-kitchen to compare Xiaohongshu, Zhihu, Reddit, and store-page advice for the best-value groceries near me.
```

## Scripts

Generate concrete shopping quantities:

```bash
python scripts/grocery_planner.py --servings 2 --meals 4 --profile budget --protein beans --starch tortillas --veg mixed --cuisine mexican-latin --lang zh-en
```

Run a safety and health screen:

```bash
python scripts/meal_check.py --ingredients "chicken,rice,broccoli,soy sauce,sesame oil" --allergies sesame --protein chicken --veg yes --starch rice --risk none --goal balanced --sodium moderate --lang zh-en
```

Compare true value across strategies:

```bash
python scripts/value_compare.py --option "Aldi tofu bowls|9.50|4|35|5|1|3" --option "Costco chicken prep|24.00|10|90|4|2|4" --option "Takeout lunch|13.00|1|10|1|1|1" --lang zh-en
```

## Safety And Health Boundary

This skill supports practical food planning, not medical diagnosis or individualized medical nutrition therapy. It uses conservative safety gates and points users to clinicians or registered dietitians for pregnancy, immunocompromise, kidney disease, diabetes, cardiovascular disease, severe allergies, eating disorder history, medication interactions, or other high-stakes personal health needs.

## References

- USDA FSIS Safe Minimum Internal Temperature Chart
- USDA FSIS Food Thermometers
- FDA Safe Food Handling
- FDA Food Allergies
- Dietary Guidelines for Americans
- USDA MyPlate
