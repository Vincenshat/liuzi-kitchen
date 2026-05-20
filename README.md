# 留子厨房 / Liuzi Kitchen

A dynamic bilingual kitchen skill for international students cooking abroad. It helps an agent do more than return static recipes: it asks for personal constraints, adapts to pantry inventory and grocery prices, checks food safety and health fit, recommends global dishes, rescues cooking problems, and turns leftovers into safe next meals.

## What This Skill Covers

- **Dynamic intake** - people, meals, allergies, diet rules, health goals, kitchen equipment, budget, time, spice tolerance, and pantry stock
- **Global cuisine planning** - Chinese, Japanese-Korean, Southeast Asian, South Asian, Mediterranean, Middle Eastern/North African, Mexican/Latin American, African/Caribbean, American, and European home-cooking lanes
- **Food safety checks** - thermometer targets, cross-contamination prevention, safe thawing, leftover timing, reheating, high-risk-user warnings
- **Health checks** - allergy screening, balanced plate review, protein/vegetable/starch/fat fit, sodium/sugar/saturated-fat flags, goal-specific adjustments
- **Grocery math** - concrete quantities by servings and meals, cuisine seasoning kits, value tactics, freezer and package-size thinking
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
│   └── meal-catalog.md              # Starter meal templates
└── scripts/
    ├── grocery_planner.py           # Bilingual grocery quantity planner
    └── meal_check.py                # Safety and health PASS/WARN/FAIL checker
```

## Core Modes

1. **Recommend** - suggest dishes across cuisines for the user's constraints.
2. **Plan** - build a meal plan with prep order, storage, reheating, and substitutions.
3. **Shop** - calculate grocery quantities and value-focused swaps.
4. **Cook-Live** - diagnose and rescue cooking problems in progress.
5. **Reuse** - transform leftovers and pantry items into safe next meals.

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

## Scripts

Generate concrete shopping quantities:

```bash
python scripts/grocery_planner.py --servings 2 --meals 4 --profile budget --protein beans --starch tortillas --veg mixed --cuisine mexican-latin --lang zh-en
```

Run a safety and health screen:

```bash
python scripts/meal_check.py --ingredients "chicken,rice,broccoli,soy sauce,sesame oil" --allergies sesame --protein chicken --veg yes --starch rice --risk none --goal balanced --sodium moderate --lang zh-en
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
