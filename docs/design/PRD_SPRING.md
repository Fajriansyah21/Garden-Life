# PRD · Spring Season

| Field | Value |
|---|---|
| Status | DRAFT — for owner review only |
| Version | v0.1 |
| Date | 2026-11-21 |
| Product | Garden Life (Roblox) |
| Author | Hermes, based on approved owner discussions and repository decisions |
| Owner approval | Pending |
| Scope target | First Release; Vertical Slice scope remains undecided |
| Related decisions | D-022, D-028, D-030–D-040, D-047–D-050 |
| Dependencies | Plant data, season calendar, plot occupancy, weather system, Mutation/Variant persistence, inventory, Life Coin economy, UI, multiplayer permissions, DataStore |

> This PRD is a product requirements draft, not an implementation-ready feature spec. It does not change any decision status, grant implementation approval, or set a spec to READY. Items marked **ASUMSI** or **BELUM DIPUTUSKAN** require follow-up. Four seasons are targeted for First Release by owner direction; Vertical Slice scope remains open.

## 1. Product purpose

Spring should feel fresh, lively, and relaxing: a season to enjoy and personalize a garden, with weather creating variety and optional collection opportunities. Farming, weather management, and risk support the cozy decoration-first experience; they must not become mandatory daily chores.

## 2. Goals

- Deliver Spring as part of the four-season First Release target.
- Give Spring a distinct Fresh Nature identity and readable weather rhythm.
- Let players enjoy weather-driven fruit Mutation while limiting offline Mutation generation.
- Provide understandable, optional protection and recovery choices for seasonal and Thunderstorm risks.
- Keep seasonal collection rewards fair across plot sizes and preserve Variant/Mutation distinction.
- Keep economy parameters explicit and balanceable; do not invent prices or fruit multipliers.

## 3. Non-goals

- Defining the other three seasons' final weather rosters or gameplay effects.
- Defining Vertical Slice scope or implementation schedule.
- Final plant roster, including the three proposed seasonal-exclusive plants; owner deferred that discussion.
- Seasonal events in First Release. Owner said seasonal events are for a later update.
- Final fruit base prices, Mutation multipliers, item prices (except the Season Pill ratio below), shop inventory, and monetization catalog contents.
- Final Luau/code design.

## 4. Player experience and user needs

Players should be able to:
- Recognize Spring's Fresh Nature identity and current weather.
- Understand why plant growth, WaterLevel, fruit Mutation, or plant condition changed.
- Choose between outdoor weather rewards and Greenhouse seasonal safety.
- Understand seasonal plant compatibility and receive warnings before Dormant, Wilt, or death stages.
- Recover a wilted Strict plant through a clear, non-repetitive care action.
- Leave an empty plot without seasonal timers, fertilizer timers, plant growth, weather effects, or weather Mutation continuing there.
- Collect seasonal Variants without needing a larger plot or more plants.

## 5. Scope and product rules

### 5.1 Calendar and season transitions

- A season lasts 30 in-game days.
- One day is 720 ticks; one tick is 30 seconds. Therefore one in-game day is 6 real-time hours and one 30-day season is 180 real-time hours.
- Spring begins with Sunny.
- Days 28–30 use Soft Transition. Environment visuals change gradually. A 20% weather-selection chance may use the next season's weather table for visuals only; gameplay effects of the next season begin on day 1 of that season.
- Details of cross-season visual blending and next-season weather tables are **BELUM DIPUTUSKAN** until all four seasons have definitions.

### 5.2 Plant seasonal compatibility

When a plant is incompatible with the new season, it enters Dormant:

1. Dormant lasts 7 in-game days of active plot occupancy.
2. Dormant timer runs while at least one player occupies the plot; it freezes when plot is empty.
3. Plant growth freezes while Dormant.
4. Existing fruit remains eligible for weather Mutation while the plot is occupied.
5. At Dormant expiry, tolerance rules apply:

| Tolerance | Growth speed | Harvest yield | Seasonal death |
|---|---:|---:|---|
| Tolerant | 0.7× | 80% | No |
| Sensitive | 0.4× | 50% | No |
| Strict | Wilt phase | No new production during Wilt | May die after Wilt timer |

These numeric growth/yield values are approved concept values but still require balance validation. Rounding rules for fractional harvest yield are **BELUM DIPUTUSKAN**.

- Strict plants enter Wilt for 1 in-game day of active plot occupancy (6 hours online).
- During Wilt, plant growth, new fruit production, and weather Mutation stop.
- If untreated until the Wilt timer expires, plant dies. Dead-plant choices follow D-038: remove/discard, convert to ordinary fertilizer, or Robux recovery.
- Timer pause/resume behavior across server changes, co-op occupancy and save/load requires technical specification.

### 5.3 Season Pill, Greenhouse, and Wilt recovery

**Season Pill**
- Applies to one living plant and protects it from seasonal incompatibility through the end of the current season.
- Effect ends if plant is removed/discarded.
- Does not clear unrelated conditions or apply to dead plants.
- Target price direction: 80% of target mature plant's sale value. This is an approved design direction; formula details and price validation against Mutation/Variant value are **BELUM DIPUTUSKAN**.

**Greenhouse**
- Target First Release building; capacity 18 plants.
- Prevents seasonal Dormant/Wilt effects for plants inside.
- Greenhouse plants do not receive weather Mutation.
- Plants still require water and can become Overwatered from excessive watering or prolonged Sprinkler use.
- Does not clear pre-existing conditions.
- Capacity 18 originates from the concept backlog; placement footprint, cost, unlock, inventory/build rules and transfer behavior are **BELUM DIPUTUSKAN**.

**Wilt care item**
- Current agreed name in D-047 is Herbal Tea. An earlier brainstorm proposed Bloom Tea; final naming needs owner clarification before asset/UI naming.
- One use starts 30 minutes of online care and requires one watering action.
- Successful care returns plant to Dormant for another 7 active in-game days.
- Does not cure other conditions. Item price, source, stack and interruption details are **BELUM DIPUTUSKAN**.

### 5.4 Spring weather

One weather state is shared server-wide. All plots see the same sky and weather identity.

| Weather | Duration | Approved concept gameplay |
|---|---:|---|
| Sunny | 40 ticks / 20 min | Spring start; neutral; no WaterLevel, growth, fruit-size, plant-condition or Mutation effect |
| Cloudy | 20 ticks / 10 min | At start, +0.25 WaterLevel once; high-sunlight plants receive 15% added remaining grow time; no Mutation |
| Drizzle | 20 ticks / 10 min | +0.05 WaterLevel/tick; Wet roll 2.5% per eligible fruit/tick; 15% added grow time |
| Rainy | 20 ticks / 10 min | +0.075 WaterLevel/tick; Wet roll 5% per eligible fruit/tick; Wet→Flooded roll 2.5%/tick; 20% added grow time |
| Windy | 20 ticks / 10 min | WaterLevel −0.005 every 2 ticks; all plants/fruits grow at 1.5×; no Mutation |
| Misty | 20 ticks / 10 min | +0.25 WaterLevel once at start; 15% added grow time; Misty roll 6.697%/eligible fruit/tick; Misty→Foggy 0.809%/eligible tick |
| Thunderstorm | 20 ticks / 10 min | +0.075 WaterLevel/tick; 20% added grow time; lightning risk, Shocked/Charged and protections per D-038 |

- Non-Sunny duration follows D-031. Weather tick is 30 seconds.
- Growth modifiers were agreed in discussion to change from “added grow time” to speed multipliers, but that change has not yet been recorded in DECISIONS/GDD. Therefore the table above preserves recorded D-028–D-038 mechanics; exact replacement multipliers for Cloudy, Drizzle, Rainy, Misty and Thunderstorm are **BELUM DIPUTUSKAN** pending a decision-log update. Windy 1.5× remains recorded in D-036.
- D-048 weather weights are **ASUMSI balancing**: Sunny 34, Cloudy 16, Drizzle 14, Windy 12, Rainy 10, Misty 8, Thunderstorm 6.
- Transition constraints from D-048: no immediate repeat; Sunny may follow any weather; Thunderstorm only after Cloudy or Rainy, max 2 per in-game day; Misty only after Cloudy/Drizzle/Rainy; Drizzle and Rainy may follow each other; Windy may follow any weather except Windy; after Thunderstorm, Sunny or Cloudy at 50/50.
- Exact algorithm for applying weights after eligibility filters is **BELUM DIPUTUSKAN**. Must define normalization and behavior when an eligible list is empty.
- Weather sky/calendar continues when a plot is empty; plant effects, WaterLevel changes, growth and weather Mutation freeze for that plot.

### 5.5 Mutation, Variant, and fruit multiplier

- Variant and Mutation remain distinct systems per D-022; both are stored persistently on fruit and can coexist.
- Variant seasonal roll is one roll per plot per in-game day, base 0.5%. Each failed daily roll adds 0.05 percentage points to the next roll in that season. Chance resets to 0.5% at season change.
- Seasonal Variant chance is per plot, not per plant. Candidate names Pastel Spring, Fresh Green, and Rain-kissed are **proposals**, not confirmed content.
- The exact eligible target plant/fruit when a plot-level roll succeeds is **BELUM DIPUTUSKAN**. Avoid rewarding one player multiple Variants from a single plot roll.
- Variant is persisted on the plant/fruit data as applicable; exact ownership/data field is subject to D-022 and spec.
- A fruit may hold at most 15 unique Mutations. This is the agreed correction to the earlier mistaken interpretation of “15×”; it is a count cap, not a multiplier cap. The addition is in D-049.
- Mutation multipliers contribute to sale value under D-022, but individual values are not set here.
- Wet is the universal prerequisite for Flooded across wet-weather paths, including Wet acquired in Drizzle. This agreement is not yet recorded in DECISIONS.md; it requires a new decision entry before implementation.
- Existing Rainy Flooded probability from WaterLevel follows D-035: 2.5% per 2-minute eligible exposure at WaterLevel 4.00–4.99, and 2.5% per 1-minute exposure at 5.00; at most one Flooded per fruit lifetime.
- Whether Flooded from high WaterLevel also requires Wet, and how exposure timer carries across WaterLevel bands, remain **BELUM DIPUTUSKAN**; resolve against the approved universal-Wet principle.
- The agreed fruit multiplier cap is 15 unique Mutation count, not sale multiplier. A separate fruit sale-multiplier cap of 15× has not been approved. Do not implement one based on this PRD.
- Roll order when Wet and Wet→Flooded are both eligible in the same tick remains **BELUM DIPUTUSKAN**.

### 5.6 Thunderstorm, risk and protection

- D-038 baseline: lightning roll 1% per plot per tick, maximum 5 strikes per plot per episode; impact radius 8 studs; Shocked 100% to fruit on struck plant, Charged 15% per fruit; plant outcome is mutually exclusive: 60% unharmed, 25% Scorched, 15% dead.
- During Thunderstorm, WaterLevel +0.075/tick and recorded growth-time increase 20% (replacement speed multiplier unresolved).
- Scorched appearance is charred black; harvest yield is 50% of normal, rounded down; no automatic recovery. D-040: one Vitamin cures one Scorched plant and preserves age/size/growth progress. Rebranding Vitamin to Scorch Balm was agreed in discussion but not yet recorded; name in repo remains Vitamin until decision entry.
- Dead plant choices: remove/discard, convert to ordinary fertilizer, or Robux recovery. No Thunder Fertilizer.
- Lightning Rod rebranding to Storm Catcher agreed; maximum 2 per plot. D-038 baseline radius 24 studs, 50% redirection and durability 3 redirected strikes remains unless superseded by owner-approved decision.
- Thunderstorm Relief rebranding to Storm Shield agreed; maximum 1 per plot. Radius/effect upgradeable to 3 levels; one additional Shield consumed per upgrade, requiring 3 total units for maximum level. Exact level values, radius, durability and interaction with D-038 stacking rules are **BELUM DIPUTUSKAN**; do not silently overwrite D-038.
- Small Protection Kit uses Life Coin. Medium Protection Kit uses Robux and contains more items only; no mechanical advantage. Contents/quantities are **BELUM DIPUTUSKAN**.
- Shocked/Charged sale multipliers, Scorch Balm price/source/stack and Robux recovery price are **BELUM DIPUTUSKAN**.

### 5.7 Fertilizer

D-049 approved concept:
- Basic Fertilizer: +0.2× growth-rate bonus for 120 ticks.
- Premium Fertilizer: +0.5× growth-rate bonus for 240 ticks.
- Timers/effects freeze when plot is empty; resume when at least one player occupies it.
- One active fertilizer per plant; no stacking or replacement while active.
- Can coexist with Season Pill, weather modifiers and Greenhouse. Cannot be used on Dormant, Wilted or dead plants.
- Does not alter WaterLevel, Mutation, Variant, fruit quality or plant condition.
- Fertilizer prices, source, inventory stack, and exact growth formula are **BELUM DIPUTUSKAN**. Weather-plus-fertilizer calculation must not be assumed from illustrative arithmetic.

## 6. Product requirements

### Functional requirements

1. **FR-01 Calendar:** Maintain one 30-day season calendar with 720 30-second ticks per in-game day.
2. **FR-02 Spring entry:** Start Spring in Sunny, with server-wide weather state.
3. **FR-03 Weather duration/selection:** Apply Sunny/non-Sunny durations and D-048 transition constraints; expose no invalid transition. Weight normalization remains a blocking design detail.
4. **FR-04 Plot occupancy:** When plot occupancy becomes zero, freeze per-plant season timers, plant growth, fertilizer effects/timers, weather effects and weather Mutation. Keep global calendar/sky/weather running.
5. **FR-05 Dormant/Wilt:** Track compatibility, tolerance, Dormant and Wilt timers, pause on empty plot, and apply approved outcomes.
6. **FR-06 Protection:** Apply Season Pill, Greenhouse, Herbal Tea and protection-building rules without clearing unrelated conditions.
7. **FR-07 WaterLevel:** Respect 0–5 limits and 0.001 internal precision (D-033); greenhouse does not bypass Overwatered.
8. **FR-08 Mutation:** Roll independently per eligible fruit and weather tick as applicable; respect D-022 uniqueness and max 15 unique Mutations per fruit. Resolve Wet/Flooded prerequisites and same-tick order before implementation.
9. **FR-09 Variant:** Roll once per plot per in-game day with season-specific pity, reset at season change, persist result, and prevent duplicate/ambiguous targets.
10. **FR-10 Thunderstorm:** Apply strike, protection, condition, recovery and dead-plant outcomes consistently with D-038 plus approved superseding decisions.
11. **FR-11 Fertilizer:** Apply two fertilizer tiers and freeze timers/effects on empty plots.
12. **FR-12 Player feedback:** Show current weather, remaining duration, season phase, plant compatibility/status, timer pause reason, Mutation/Variant feedback, WaterLevel/Overwatered, active protection and fertilizer timer.
13. **FR-13 Economy:** Validate all purchase and reward transactions server-side. Do not ship price/multiplier values that remain undecided.
14. **FR-14 Persistence:** Persist season/plant/fruit states and prevent offline tick catch-up from applying prohibited plot effects. Persistence rules for shared plot occupancy and server migration require technical design.

### Non-functional requirements

- Server authoritative for weather state, plot occupancy, timers, WaterLevel, plant growth, Mutation/Variant rolls, item use and transactions.
- PC and touch UI support; status information must remain understandable without relying on color alone.
- Graceful handling of disconnect, server shutdown, DataStore failure, rejoin, owner/guest presence, and concurrent co-op actions.
- Performance budget for 4 plots, weather ticks, per-fruit rolls, and persisted plant states must be validated; numbers/budgets are **BELUM DIPUTUSKAN**.
- No daily-login obligation: all plot-scoped timers and effects pause when plot is unoccupied.

## 7. Economy and retention analysis

### Sources
- Fruit sales using the existing base-price × Variant × Mutation valuation model (D-022); values not yet set.
- Seasonal Variant collection as a non-cash collection reward; possible sale value only through D-022 multipliers, still undecided.
- Ordinary fertilizer conversion from dead plants; yield/value undecided.

### Sinks
- Season Pill, target 80% of target mature plant sale value (approved direction; price formula needs validation).
- Herbal Tea, Scorch Balm, Basic/Premium Fertilizer, Greenhouse, Storm Catcher, Storm Shield, Small Protection Kit; all prices/sources unresolved except Small kit Life Coin purchase and Medium kit Robux purchase.
- Other plant/shop purchases are outside this PRD's unresolved economy table.

### Risks and mitigations

| Risk | Impact | Mitigation / requirement |
|---|---|---|
| Seasonal risk feels punitive, especially Strict death | Cozy identity/retention harmed | Clear compatibility labels and escalating warnings; 7-day active Dormant and 1-day active Wilt; pause timers when plot empty |
| Greenhouse becomes mandatory | Reduces outdoor weather play and creates a paywall perception | Greenhouse is safety, not weather Mutation; validate capacity 18 and Life Coin path; do not make Robux protection mechanically superior |
| Weather Mutation supply inflates fruit economy | Sale-value inflation | Freeze rolls on empty plots; validate odds, 15-Mutation cap and D-022 multiplier sum in simulation |
| Spring weather weights create too much wet/Thunderstorm supply | Overwater, item costs, or loss frustration | Simulate expected episode counts and exposure; tune weights only with owner approval |
| 80% Season Pill ratio is too expensive/cheap | Either plant retention pain or seasonal risk bypass | Model against plant lifecycle sales, yield, mutations and recovery; keep ratio as approved direction, not a hardcoded price before model |
| Pity Variant creates late-season reward spike | Variant supply/economy imbalance | Simulate daily probability over 30 days and define one recipient target per plot roll; reset per season |
| Robux kit is perceived as pay-to-win | Trust/fairness damage | Medium Kit may only increase quantity; verify Small kit offers viable Life Coin path |
| Watering/sprinkler overflows Greenhouse plants | Unexpected plant deaths and support burden | Clearly show WaterLevel/Overwatered alerts in Greenhouse; preserve existing D-018/D-033 rules |
| Online-only active timers are confusing in co-op | Guest activity may advance owner plant state | Define plot occupancy: any player present; communicate timer state and permissions; test owner/guest cases |
| Seasonal events leak into First Release | Scope creep | Seasonal events are explicitly post-release update; do not include event reward dependencies |

### Metrics to evaluate (targets TBD)
- First-session comprehension of weather, seasonal compatibility and plant status.
- Share of players who understand why plot timers pause when empty.
- Percentage of players who use outdoor planting, Season Pill and Greenhouse (without one option dominating).
- Seasonal plant death rate, Scorched rate and recovery-item usage.
- Mutation/Variant generation per occupied plot-hour and resulting Life Coin earned/spent.
- Return-session rate after seasonal transition; player reports of unfair loss or unclear state.
- Economy inflation and price-to-earn ratios once prices/base values exist.

## 8. Dependencies and unresolved decisions

### Blocking before implementation-ready spec

1. Record approved growth-speed multiplier conversion in DECISIONS; set exact Cloudy, Drizzle, Rainy, Misty and Thunderstorm speed multipliers and clarify interaction with Sun-loving/Neutral/Shade-loving classification.
2. Resolve universal Wet prerequisite for Flooded against D-035 WaterLevel route; define same-tick Wet/evolution roll order and exposure timer carry-over.
3. Define eligible recipient plant/fruit for successful per-plot Seasonal Variant roll; define whether the roll occurs once per plot-day independent of occupancy and whether a plant/fruit needs to exist.
4. Formalize occupancy and timer rules for multiple occupants, plot ownership changes, server transfer, and reconnect.
5. Reconcile item naming: D-047 says Herbal Tea; discussion proposed Bloom Tea. D-040 says Vitamin; discussion proposed Scorch Balm. Storm Catcher/Storm Shield rename and upgrade values are not yet in decision log.
6. Define Storm Shield level values, radius/effect/durability, and replacement of D-038 Relief stacking; define Small/Medium kit contents and quantities.
7. Define weather-weight algorithm after eligibility filtering, normalization, daily Thunderstorm cap reset, and behavior when no candidate remains.
8. Define shop refresh interaction with seasonal inventory. Existing brainstorm rates: seed shop 5 min, building/decor 30 min, event/season shop 15 min; no other shops decided. Seasonal event shop/season event scope is post-release; clarify whether Season Pill uses a regular shop.
9. Define rounding for Tolerant/Sensitive fractional yield and exact growth-modifier composition, including fertilizer.
10. Define persistence of variant pity and timers across server shutdown/DataStore failure.
11. Validate economy with plant sale values, yield, Mutation multipliers, and costs; do not infer missing values.
12. Confirm all four seasons' calendars/weather tables before defining final Soft Transition cross-season behavior.

### Other open items

- Spring's three exclusive plants are deferred; no names/stats/content are approved.
- Candidate seasonal Variant names are proposals only.
- Exact visual assets, seasonal palette implementation, animation/audio feedback, and warning cadence are open.
- Season events are planned for a later update, not First Release.
- Vertical Slice inclusion is unconfirmed.

## 9. Acceptance criteria for PRD review

This is a product-level review checklist, not an implementation test plan.

- [ ] Owner confirms Spring is part of First Release; four-season target is reflected without implying Vertical Slice approval.
- [ ] All approved decisions and current repo baseline reconcile without silently replacing D-028–D-050.
- [ ] Every unapproved number, name, probability, price or system rule is marked **ASUMSI**, **PROPOSAL**, or **BELUM DIPUTUSKAN**.
- [ ] Season, weather, Dormant, offline, Mutation/Variant, Greenhouse and Overwatered rules are mutually consistent.
- [ ] Economy source/sink, retention risk, Robux fairness and event exclusion are reviewed.
- [ ] All blockers needed for later feature specs have owners and decisions.
- [ ] Owner reviews and approves the PRD; status remains DRAFT until owner changes it.

## 10. Revision history

| Version | Date | Change | Status |
|---|---|---|---|
| v0.1 | 2026-11-21 | Initial product requirements draft from repository decisions and approved brainstorming; unresolved conflicts explicitly flagged | DRAFT |
