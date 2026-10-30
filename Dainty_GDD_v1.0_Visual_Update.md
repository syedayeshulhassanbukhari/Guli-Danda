# DAINTY

**GAME DESIGN DOCUMENT · VERSION 1.0 (VISUAL UPDATE)**  
**Roblox · R15 Blocky · Sports / Physics · PvP / Co-op**  
**Status:** Requirements approved for GDD production · **Baseline:** 18 October 2026 · **Circle visuals added:** 26 October 2026

> **Design vision:** A modern multiplayer take on Pakistani Gulli Danda: simple to pick up, deeply satisfying to master, and endlessly replayable with friends. Traditional rules remain recognizable; optional arcade formats create fast, social sessions.

![Pakistani Street Dainty — original generated concept illustration](Dainty_GDD_assets/pakistani_street.jpg)

*Cover illustration — Pakistani Street Dainty. Concept art, not final Roblox assets.*

---

## Document control

| Field | Value |
|---|---|
| Working game title | Dainty |
| Primary platform | Roblox |
| Playable avatar | Standard R15 rig using blocky avatar proportions |
| Core modes | 1-minute, 3-minute, 5-minute, Traditional Unlimited, PvE Co-op |
| Default public mode | Street Clash, 3v3, approximately 3 minutes |
| Launch themes | Pakistani Street, Backyard Arcade, Japanese Festival |
| Main progression | Coins, quests, daily rewards, cosmetic collections, permanent mastery ranks |
| Competitive policy | Cosmetic purchases never increase bat reach, Gulli speed, or fielding accuracy |
| Document status | Baseline production GDD; numerical tuning is subject to playtesting |

### Interpretation note

The original play rules described by the project owner define the fundamental Pakistani Traditional Mode: **three hit opportunities per batting sequence; an immediate OUT when a returned Gulli directly hits the Danda; an under-arm/under-leg action performed by the batter when the return lands inside the marked circle; and player-by-player innings until the batting team is out.** Additional cases not explicitly established by those rules use the Roblox implementation defaults stated below. These defaults are **game-design choices**, not claims that all traditional communities play the same way.

### Contents

1. Vision and design pillars
2. First-session experience and core loop
3. Traditional game rules and scoring
4. Match modes and win conditions
5. Themes and environment requirements
6. Co-op, multiplayer and social play
7. Controls and gameplay camera
8. Physical simulation and server authority
9. Animation, audio and gameplay VFX
10. Gulli, Danda and cosmetic collection
11. Mastery rank progression
12. Day 3 / Day 7 rewards, quests and retention
13. Economy and monetization
14. UI/UX screen requirements
15. Matchmaking, bots and reconnection
16. Technical architecture and data model
17. Live operations and metrics
18. Roadmap, deliverables and QA
19. Visual asset inventory and appendix

---

## 1. Vision and design pillars

### 1.1 High concept

Dainty is a family-friendly, stylized Roblox team-sports game based on **Gulli Danda**, also known locally as Dainty. The batter pops a short wooden **Gulli** off the ground, strikes it in the air with a longer wooden **Danda**, and attempts to send it a long distance. The fielding side retrieves the Gulli and tries to throw it onto the Danda lying inside the starting circle. A direct hit means an immediate OUT. Field positioning and precise throws are as important as hitting power.

Players can choose a faithful-feeling unlimited Pakistani Street match, quick timed PvP rounds, or more playful co-op and arcade challenges. Three launch environments offer distinct aesthetics while sharing the same core batting and throwing systems.

### 1.2 Pillars

| Pillar | Player promise | Design implication |
|---|---|---|
| Instant physical fun | The first hit feels good before the first minute ends | Immediate practice, simple controls and dramatic Gulli flight |
| Traditional identity | Gulli, Danda, circle and team rotations matter | Do not replace the core sport with generic baseball |
| Skill over purchases | Better timing and aim win matches | Competitive physics shared by every skin |
| Everyone participates | Fielders have meaningful action and friends cooperate | Catching, retrieval, passing and PvE challenges |
| Reasons to return | Improvement, cosmetics and friends | Quests, records, ranks and rotating weekly events |
| Readability and speed | Short matches remain understandable on mobile | Clean HUD, clear OUT states and streamlined timed rules |

### 1.3 Target audience and style

- Core audience: Roblox sports/party players, friends playing together, and South Asian audiences familiar with Gulli Danda.
- Secondary audience: competitive timing-game players and cosmetic collectors.
- Visual direction: premium **R15 blocky** game look, colorful environments, crisp silhouettes, family-friendly faces, satisfying but controlled particles.
- Devices: PC, phone and tablet at launch; evaluate console-specific controls after the core experience is stable.

---

## 2. First-session experience and core gameplay loop

![Batter-to-fielder gameplay flow diagram](Dainty_GDD_assets/gameplay_flow.png)

### 2.1 Basic loop

1. Spawn near a practice lane with a Danda ready.
2. Pop the Gulli; time the airborne hit; watch it land.
3. Queue for **Play Now** or choose a specific mode.
4. Batting side scores distance; fielders catch/retrieve and perform return throws.
5. Award team score based on the mode's banking and OUT rules.
6. Display results, coins, Rank XP, personal records and quest progress.
7. Invite friends, change cosmetics, select another mode or rematch.

### 2.2 New-player timing requirements

| Elapsed time | Required experience | Reason |
|---|---|---|
| 0–20 seconds | Spawn, move, first guided pop and hit | Show the core fun before menus |
| By 1 minute | See a hit, distance feedback and sample return throw | Explain the sport through play |
| By 3 minutes | Complete or approach the end of a short match | Establish the social loop |
| By 5 minutes | Receive coins/quest progress and see next unlock | Give a return goal |

![First-session to Day 30 player journey](Dainty_GDD_assets/retention_timeline.png)

### 2.3 Onboarding design

The first visit starts with a compact interactive practice, not an unskippable text tutorial. Show **POP → SWING → THROW** using one contextual prompt at a time. Once the user lands a successful hit, expose **Play Now**, **Modes**, **Locker**, **Quests** and **Daily Rewards**. Players who already completed onboarding bypass it on later visits. Tutorials can be replayed from Settings.

---

## 3. Pakistani Traditional Mode: complete rules

### 3.1 Teams and turn order

- Typical match: **3 batters vs 3 fielders**.
- Exactly one batting-team player is the active batter; other teammates wait for their turns and can spectate or cheer.
- Opposing fielders may move across the playable field, retrieve the Gulli, and coordinate the return.
- Batter A begins with **three hit opportunities**, followed by the return-throw phase. If the batter is OUT, Batter B enters with a new three-hit sequence, then Batter C.
- Once **all batters on the batting team are OUT**, the teams swap roles. The other team completes its batting innings; total banked distance determines the winner.
- A 1v1 or 2v2 traditional variant uses the same logic with fewer batters.

### 3.2 Batting sequence

1. The active batter starts at the designated origin with the Gulli on the ground.
2. **Pop**: hit one end of the Gulli so it rises into the air.
3. **Swing**: strike the airborne Gulli toward the playable field.
4. A successful hit moves the Gulli's final valid landing position; the next hit begins at that position, up to **three attempts in the current sequence**.
5. An unsuccessful swing consumes one hit opportunity. If all three attempts fail to produce a valid hit, the batter is OUT. This is an arcade adaptation default.
6. After the sequence, the Danda is placed on the original starting position within a chalk circle. The fielding side performs a return throw from the Gulli's location.

**Clarification:** Three hits are **opportunities in a sequence**, not three hearts that absorb Danda OUTs. Batters may receive new sequences after a safe return.

### 3.3 Arena target geometry

![Top-down court schematic showing Danda target, fielders and return path](Dainty_GDD_assets/arena_schematic.png)

- The **Danda** lies flat and is the actual physical target.
- The **circle** is a separate, clearly marked area around the Danda.
- A return throw resolves the direct-Danda collision first; a valid circle landing without a Danda collision then triggers the special.
- Dimensions of the circle and Danda hit zone are identical for the same ruleset across all arena themes.

### 3.4 Three return outcomes

![Traditional return-throw resolution](Dainty_GDD_assets/return_outcomes.png)

| Return result | Ruling | Next step |
|---|---|---|
| Gulli physically hits the placed Danda | **Immediate OUT** | Current unbanked sequence does not score; next teammate bats |
| Gulli lands inside the marked circle but misses the Danda | **Circle special** | Batter performs the under-arm/under-leg hit; success continues play and triggers another return; failed special = OUT |
| Gulli lands outside the circle and misses Danda | **SAFE** | Bank current sequence distance; same batter starts a fresh three-hit sequence |

The **special hit belongs to the batter**, never the fielding player. It must have a distinct animation and timing interaction.


#### Circle special: illustrated gameplay sequence

**Visual 1 — The Gulli lands inside the chalk circle.** The fielding team's return throw misses the Danda itself, but the Gulli comes to rest within the marked circle. The batter is **not immediately OUT**; instead, the circle-special challenge starts. The scene below shows the relative location of the Gulli and batter, not a final collision-accurate screenshot.

![Circle-special trigger: Gulli resting inside the white chalk circle as the batter prepares to play](Dainty_GDD_assets/circle_special_gulli_in_circle.jpg)

*Gameplay illustration: the Gulli is inside the circle. A direct collision with the placed Danda would be an OUT instead.*

**Visual 2 — Batter performs the under-leg special hit.** Control returns to the **active batter**, who raises a leg and attempts a one-handed Danda swing beneath it to strike the Gulli back into the field. If successful, play continues and fielders prepare another return throw. If unsuccessful, the Roblox ruleset resolves it as an OUT.

![Circle-special execution: R15 batter swings the Danda under the raised leg and launches the Gulli](Dainty_GDD_assets/circle_special_under_leg_hit.jpg)

*Gameplay illustration: the under-leg action is performed by the batter, never the fielder. Visuals are concept art and can be refined for accurate one-handed R15 animation.*

**Implementation note:** The Danda lies flat during the return-throw collision check. When the circle special is triggered without a direct Danda hit, transition into the special animation/interaction. Resolve the next fielding throw only after the special Gulli flight and landing are complete.

### 3.5 Extra throw option in casual Traditional

To preserve the social choice described in the childhood rules, **Unlimited Casual** permits the active batter to offer one additional return throw after an outside-circle miss. Both sides must accept promptly. If not accepted, the default SAFE outcome applies and batting resumes. Timed and competitive matches do **not** permit this negotiation because it would prolong a round or make results hard to compare.

### 3.6 Valid landing, boundary and score banking

- A batting sequence records the Gulli's **furthest valid final position relative to the original origin**, measured in meters.
- Add valid **banked distance** across a team's safe sequences; do not also add each flight segment separately. Example: positions at 25m, 48m and 73m give an at-risk sequence value of **73 points**, not 146.
- A successful SAFE return banks those 73 points and restarts the batter's next sequence.
- A direct Danda OUT loses only the **current unbanked sequence**. Points banked in previous safe sequences remain.
- Out-of-bounds flights are invalid; they use the hit opportunity but preserve the last valid field position. If no valid field position was achieved, the sequence scores zero.
- No negative distance; backward hits may improve positioning but cannot generate negative or duplicated points.
- A player's batting innings end only at an OUT condition; Traditional Unlimited has **no round timer**, but supports an inactivity timeout to prevent griefing.

---

## 4. Modes and win conditions

| Mode | Players | Target session | Key rules | Winner |
|---|---|---|---|---|
| **Quick Dainty** | 1v1 | 1 minute | One short three-hit sequence per player, one return throw each | Highest banked valid distance |
| **Street Clash** (default) | 3v3 | 3 minutes | One three-hit sequence and return per player; batters rotate automatically | Greater total banked distance |
| **Championship** | 3v3 | 5 minutes | Normal team rotations followed by each team's top scorer in a bonus duel | Greater combined score |
| **Traditional Unlimited** | 1v1 to 3v3 | Until innings end | Full three-hit cycles, circle mechanic, continued batting until OUT | Greater total banked distance after both innings |
| **Co-op Distance** | 1–4 vs AI | 3 minutes | Simultaneous teammates contribute valid distance to a shared team target | Meet target before time expires |
| **Co-op Target Smash** | 1–4 vs objectives/AI | 3 minutes | Collaboratively hit targets, clear gates, chain special objectives | Complete objective set |

### 4.1 Timed arcade adjustments

A timed PvP mode **does not** loop every batter indefinitely. Each participant completes one compact three-hit sequence and one return-throw resolution; a SAFE return banks points then rotates to the next batter. An OUT loses that sequence. This consciously differs from Unlimited Traditional.

- Teams receive equal batting opportunities.
- If the visible timer reaches zero while the Gulli is airborne or being returned, the current action finishes before results; a short overtime badge explains the extension.
- Tie breaker: highest single valid banked sequence, then fewest missed swings, then draw.
- Quick Dainty's 60 seconds is a target: approximately 30 seconds per side, with transitional moments optimized.
- Street Clash's 180 seconds averages about 30 seconds for each of six batting turns; automated ball reset and fast animations keep the pace.
- Championship allocates its opening rotations before a final duel. Team sizes larger than 3v3 are custom or future modes, not standard launch queues.

### 4.2 Arcade modifiers

Available in custom matches and relevant co-op themes: **Catch Out**, **Long Shot Bonus**, **Perfect Swing**, **Team Fielding Combo**, **Trick Shot**, **Moving Targets**, **Target Smash**, **Precision Circle** and **Team Distance**. Danda Hit OUT and the under-leg circle special remain foundational.

- Catch Out: a clean airborne catch immediately eliminates the batter in arcade-enabled PvP.
- Team Fielding Combo: retrieve and pass to an eligible teammate positioned for the return throw; available only in marked arcade variants.
- Trick Shots / Target Smash: earn target points or progress; tournament distance-only ranking does not gain hidden bonus points from VFX.
- Every modifier must be displayed in the pre-match rules panel.

---

## 5. Three launch themes and map art direction

### 5.1 Theme A — Pakistani Street Dainty

![Pakistani Street generated illustration](Dainty_GDD_assets/pakistani_street.jpg)

**Role:** flagship and default traditional environment. **Look:** a dusty street/open neighborhood ground, brick and plaster buildings, rooftops with water tanks, local trees, everyday street props, charpai-inspired sitting spaces, spectators and colorful bunting. **Mood:** warm, authentic, festive, with readable play-space contrast.

**Gameplay:** standard chalk circle, long fielding lane and stable Danda target. No moving targets in Traditional Mode. Keep decorative spectators and structures outside the official flight boundary.

### 5.2 Theme B — Backyard Arcade

![Backyard Arcade generated illustration](Dainty_GDD_assets/backyard_arcade.jpg)

**Role:** cheerful arcade arena. **Look:** fresh lawn, wooden fences, target boards, crates, colorful distance markers, trees, small neighborhood houses and playful structures.

**Gameplay:** launch with Target Smash and co-op distance objectives; optional moving targets, pass combinations and target destruction. The traditional target-circle geometry is still available when the map hosts conventional matches.

### 5.3 Theme C — Japanese Festival

![Japanese Festival generated illustration](Dainty_GDD_assets/japanese_festival.jpg)

**Role:** ornate festival competition arena. **Look:** paper lanterns, decorated stalls, torii-inspired structures, pink blossom trees, wooden railings and clean ceremonial play grounds.

**Gameplay:** Precision Circle, special trick-shot events and moving-target challenges. This is a **fictional Dainty arena with Japanese festival styling**, not a claim of a historical Japanese Gulli Danda ruleset.

### 5.4 Shared map constraints

- All three maps support standardized batting origin, Danda circle, same gameplay distances and clearly distinguishable out-of-bounds areas.
- Obstacles affecting the Gulli are active only when the selected arcade mode explicitly requires them.
- Fielders need clear paths, fair sightlines and recovery points to prevent unreachable Gulli states.
- Keep large VFX and props away from the throwing target and flight trajectory.
- Arena choice is a **between-match vote** in general queues to avoid fragmenting matchmaking by map.

---

## 6. Co-op, PvP and social play

### 6.1 Traditional team versus team

Three players bat one at a time and three oppose as fielders. While waiting, teammates can cheer, follow a spectator camera, review scores and quickly practice aim in a non-scoring sideline zone. They cannot interfere with the live Gulli.

### 6.2 Cooperative formats

**Co-op Distance:** 1–4 friends strike Gulli simultaneously from designated lanes; their valid distances fill a common objective meter while AI fielders challenge the group. All players remain active.

**Co-op Target Smash:** partners clear a map-specific sequence of targets, moving gates and score thresholds. Teamwork unlocks a target or creates a better shot angle; success gives coins and quest progress.

### 6.3 Parties and rematches

- Up to **3 friends in PvP parties**, held together on the same team when possible.
- Up to **4 friends in PvE co-op parties**.
- Prominent **Invite Friend**, **Rematch**, **Stay as Team**, and **Join Friend** actions.
- Custom/private matches can select map, timer and optional arcade rules.
- Ranked matchmaking is **not** part of the launch scope; permanent rank is mastery, not skill rating.

---

## 7. Controls, accessibility and camera

### 7.1 PC and mobile input map

| Action | PC | Touch |
|---|---|---|
| Move | WASD | Left joystick |
| Rotate / aim | Mouse | Right-side drag |
| Pop Gulli | Left click | Pop button |
| Swing airborne Gulli | Left click again | Swing button |
| Under-leg / circle special | F | Special button |
| Fielding catch | F | Catch button |
| Pick up Gulli | E | Interact prompt |
| Charge / release return throw | Hold / release left click | Hold / release Throw |
| Pass Gulli to teammate | Q | Pass button |
| Spectate next teammate | A / D or UI arrows | Left / right spectator arrows |

Prompts adapt by device and phase; pop and catch buttons never appear simultaneously without a reason. Add adjustable sensitivity, reduced camera shake, optional reduced VFX and accessible UI scale.

### 7.2 Swing quality

![Pop-swing timing guide](Dainty_GDD_assets/timing_meter.png)

The Gulli must first be popped; the second press times the swing. A narrow **Perfect** zone yields maximum legitimate launch quality; **Good** has lower power and accuracy; a **Miss** consumes a hit. Aim direction and swing timing determine the trajectory. The meter communicates rather than replaces visual contact with the object.

### 7.3 Camera states

Standard third-person; batting focus; optional Gulli-follow flight shot for exceptional hits; return-throw aiming camera; fielding chase view; spectator camera; celebration shot. Never force a cinematic view that prevents an opposing fielder from acting. Camera moves must be short and interruptible where appropriate.

---

## 8. Gulli physics, outcomes and networking authority

- Simulate launch flight, air drag/arc, collision, bounce, rolling and rest detection.
- Server is authoritative for official hit timestamps, launch values, Danda collision, circle landing, catches, OUT status and rewards.
- Clients may predict short-term VFX and animations to reduce perceived latency; incorrect client predictions are corrected without awarding score.
- Use **continuous/swept collision queries** for fast-moving Gulli objects, preventing tunneling through the narrow Danda.
- Detect **Danda hit before circle hit**, with a stable resolution order to prevent ambiguous OUT states.
- Gulli skins and Danda skins share exactly the same competitive geometry, physical mass, speed caps and reach.
- Add bounds recovery for unreachable roofs, props, under-map falls and disconnected players.
- Anti-cheat validates timing windows, throw release origins, speed, field location, state changes, reward claims and abnormal match durations.

### 8.1 Throw skill

The return throw requires aim, a controllable charge meter and appropriate projectile arc. A projected landing marker helps beginners but does not provide guaranteed Danda hits. Modest input forgiveness is allowed on touch, balanced so players on different devices can compete.

### 8.2 Out-of-bounds and edge cases

A Gulli landing on a non-playable roof, leaving the boundary or clipping beneath the map resolves as invalid/recovered according to the current hit phase. Recovery never creates bonus distance. Simultaneous catch versus ground landing uses server timestamps. If a throw hits the Danda and circle in the same simulation step, **direct OUT wins**. A special-hit timeout counts as a failed special.

---

## 9. Animations, audio and VFX

### 9.1 R15 animation inventory

| Group | Required animations |
|---|---|
| Locomotion | Idle, walk, run, turn, quick stop |
| Batting | Ready stance, one-handed pop, one-handed swing, perfect swing, miss, follow-through |
| Special | Under-arm / under-leg special, special success, special fail |
| Fielding | Chase, pickup, one-handed throw, accurate-throw pose, catch, failed catch, pass, dive |
| Social | Cheering, waiting, OUT reaction, victory, loss, celebration, champion entrance |

Animations must read from a mobile-sized camera and work with R15 blocky proportions. The one-handed batting identity should remain recognizable even with cosmetic Dandas.

### 9.2 VFX categories

- **Hit VFX:** dust, leaf spark, clean impact slash, golden burst, crystal impact, confetti.
- **Flight trails:** default faint streak, green leaves, colored paint, gold streak, crystal shimmer.
- **Danda OUT VFX:** wooden splinters, gold sparks, confetti pop, crystal shatter, shockwave.
- **Catch OUT VFX:** separate catch indicator and effect in Catch-Out-enabled modes.
- **Special-hit VFX:** subtle under-leg event cue and success/failure feedback.
- **Rank VFX:** rank-up bursts, equipped aura, badge entry glows, champion entrance effects.

Use **effect intensity tiers** (standard, special, premium) rather than creating completely separate particle systems for every skin. An OUT label must be readable even if players select dramatic cosmetics; support reduced-VFX mode.

### 9.3 Audio identity

Crisp wooden pop, stronger perfect-contact sound, flying Gulli whoosh, bounce, pickup, charged throw, Danda hit/OUT stinger, circle challenge alert, cheers, win/loss cues and optional regional music for maps. Sound mixing must ensure gameplay cues are never hidden behind celebration effects.

---

## 10. Gulli, Danda and cosmetic collection

![Concept collection sheet for six Gulli and six Danda designs](Dainty_GDD_assets/cosmetic_collection.png)

### 10.1 Six initial Gulli variants

| Gulli | Rarity direction | Look / effect |
|---|---|---|
| Classic Wooden | Common | Plain timber, standard flight |
| Bamboo | Common | Bamboo texture, subtle green trace |
| Painted | Rare | Bold colored stripes and particles |
| Golden | Epic | Gold finish, soft sparkling trail |
| Crystal | Legendary | Translucent gem-like appearance and shimmer |
| Champion | Mythic | Animated premium material and unique celebratory trail |

### 10.2 Six initial Dandas

| Danda | Look | Example effect |
|---|---|---|
| Classic Wood | Plain polished wooden stick | Dust contact |
| Bamboo | Bound bamboo design | Leaf spark |
| Cricket Style | Sporty wrapped wooden finish | Clean white streak |
| Golden | Ornate gold-plated design | Golden impact |
| Crystal | Faceted translucent design | Crystal sparks |
| Champion | Elite animated decorative finish | Signature contact burst |

**Fairness rule:** Every appearance uses the same competitive Danda length and effective contact region. Visual mesh variations cannot enlarge a hitbox. No skin changes Gulli launch power, weight or spin behavior in competitive modes.

### 10.3 Dainty Locker

Equip and preview each of these slots separately: **Gulli Skin, Danda Skin, Hit Effect, Danda OUT Effect, Catch OUT Effect, Flight Trail, Rank Aura, Emote**. The Locker presents an R15 avatar, item rotation, rarity and effect preview with Equip / Unequip / Purchase / Earn Location. Unowned items are clearly labeled. Try-before-buy previews do not simulate unfair gameplay power.

### 10.4 Initial cosmetic content budget

| Item type | Launch quantity |
|---|---:|
| Gulli models/skins | 6 |
| Danda models/skins | 6 |
| Standalone hit effects | 5 |
| OUT effects | 4 |
| Flight trails | 5 |
| Permanent mastery tiers | 7 |
| Rank-up animation intensities | 3 |
| Named Rookie Journey sets | 2 |

---

## 11. Permanent mastery rank progression

![Proposed Dainty mastery rank ladder](Dainty_GDD_assets/rank_ladder.png)

| Tier | Mastery level | Rank presentation |
|---|---|---|
| Rookie | 1–9 | Starter badge |
| Street Player | 10–19 | Dust footsteps / nameplate accent |
| Skilled Hitter | 20–34 | Blue swing flair |
| Dainty Pro | 35–49 | Purple aura and stronger rank-up effect |
| Master | 50–74 | Gold badge and celebration burst |
| Grand Champion | 75–99 | Animated elite badge and entrance |
| Dainty Legend | 100+ | Prestige aura and champion entry |

Rank XP comes from valid match participation, completed quests, accurate throws, banking sequences, winning and fair team contributions. Losing still grants participation Rank XP to avoid punishing beginners. AFK or exploit-suspected play earns no progress.

Rank VFX are **display-only**. Mastery tiers do not increase hitting power, movement speed, throw accuracy or matchmaking priority. Cosmetic aura intensity can be toggled or reduced on mobile. Competitive MMR, if implemented later, must be independent of permanent mastery.

---

## 12. Daily rewards, Rookie Journey, quests and retention

### 12.1 Seven-day login calendar

| Claim day | Reward |
|---|---|
| Day 1 | 50 Coins |
| Day 2 | 75 Coins |
| Day 3 | 100 Coins |
| Day 4 | 125 Coins |
| Day 5 | 150 Coins |
| Day 6 | 200 Coins |
| Day 7 | 350 Coins |

**Missed logins pause progress rather than erasing the track.** The login calendar and the Rookie Journey are distinct: the login calendar gives Coins, while achievement-based milestone rewards provide the Day 3 and Day 7 exclusive cosmetic sets.

### 12.2 Day 3 and Day 7 signature rewards

![Day 3 Street Starter and Day 7 Golden Champion equipment rewards](Dainty_GDD_assets/reward_sets.png)

| Milestone | Permanent reward content | Unlock method |
|---|---|---|
| **Rookie Journey Day 3 — Street Starter Set** | Painted Gulli, Bamboo Danda, Leaf Hit VFX, **100 Coins** | Complete the third Rookie Journey milestone |
| **Rookie Journey Day 7 — Golden Champion Set** | Golden Gulli, Golden Danda, Golden Hit VFX, Golden Danda OUT VFX, **350 Coins**, Golden Champion title | Complete the final Rookie Journey milestone |

The milestones represent **progression stages**, not rigid consecutive-day login gates. Users who miss a day can continue the next time they play. Cosmetic rewards are permanently owned and cannot be lost during seasonal resets.

### 12.3 Rookie Journey objective ladder

| Stage | Main objective |
|---|---|
| Day 1 | Finish two matches and learn batting/fielding |
| Day 2 | Perform a long-distance valid hit |
| Day 3 | Achieve a Danda Hit OUT or complete a guided AI equivalent |
| Day 4 | Complete two co-op challenges |
| Day 5 | Play in a second theme |
| Day 6 | Win a team tournament or complete a team challenge alternative |
| Day 7 | Finish Rookie Championship objectives and receive Golden Champion Set |

Alternate AI paths prevent a user from getting stuck waiting for friends or a rare competitive event. Stages can progress over multiple sessions.

### 12.4 Daily and weekly quests

- **Daily:** three small objectives such as two matches, five valid hits, three pickups, one valid return throw or 100 meters of banked team distance.
- **Weekly:** five larger objectives such as co-op wins, accurate Danda throws, precision-circle challenges, themed-map participation or team distance totals.
- Quests update after each valid server-reconciled action and are claimable in the lobby or results screen.
- Rewards use Coins, mastery XP, cosmetics or small seasonal trophy points; avoid repeated pay-to-progress pressure.

### 12.5 30-day seasonal experience

Four-stage Championship Track: **Week 1 Rookie; Week 2 Challenger; Week 3 Expert; Week 4 Champion**. Weekly themed challenges rotate between the three maps and co-op objectives. Permanent achievements, lifetime personal bests and earned items stay after seasonal resets. Seasonal leaderboard standings, if implemented, reset separately.

D7 motivation: complete the Rookie set, improve skill, play with friends and see a new themed challenge. D30 motivation: finish mastery milestones, collect cosmetics, complete a seasonal track, improve personal records and return for changing weekly challenges.

---

## 13. Currency, earning rates and monetization

### 13.1 Coin rewards — initial balancing values

| Source | Coins |
|---|---:|
| 1-minute match | 20 |
| 3-minute match | 60 |
| 5-minute match | 100 |
| Successful 3-minute co-op challenge | 60 |
| Daily quest | 50–100 |
| Weekly quest | 150–300 |

Performance bonuses can add **up to 30%** of base rewards to celebrate skill but should not encourage sabotaging teammates. Unlimited Traditional rewards are capped by match and participation time to discourage farming; bot matches may use calibrated rewards.

### 13.2 Shop prices — initial balancing values

| Cosmetic | Coins |
|---|---:|
| Basic Danda skin | 250 |
| Standard Gulli skin | 350 |
| Flight trail | 600 |
| Celebration emote | 800 |
| Premium earnable cosmetic | 1,200–2,000 |

### 13.3 Monetization boundaries

Allowed: cosmetic bundles, emotes, non-competitive presentation effects, decorative items and optional private-server conveniences. **Never sell stronger bat reach, more Danda hit protection, throw precision, physics advantages or competitive power.** Avoid paid random loot boxes. Display clear pricing and prevent accidental purchases on touch devices.

---

## 14. UI/UX screen requirements

| Screen | Required elements |
|---|---|
| Home | Play Now, Modes, Locker, Quests, Daily Rewards, Profile, Settings |
| Practice lobby | Instant practice lane, party panel, theme vote, queue controls |
| Mode select | Mode description, duration, party size, traditional vs arcade rule labeling |
| Batting HUD | Three **HITS LEFT** icons, timing meter, direction, sequence distance, team total, current batter |
| Fielding HUD | Gulli marker, catch/pickup prompt, aim arc, throw meter, Danda-circle target |
| Special challenge | Circle alert, under-leg instruction, countdown and success state |
| Spectator | Active player, team score, next teammate, optional cheer/emote |
| Results | Winner/draw, total banked distance, individual highlights, OUTs, catches, earned rewards, rematch |
| Locker | Gulli/Danda model preview, individual VFX slots, rank aura, owned state |
| Progression | Quest tracker, Rookie Journey and Day 3/7 set previews, rank XP, seasonal track |

**UX priorities:** use clear Gulli-shaped icons for three hits instead of hearts; show OUT prominently in every effect skin; never place gameplay menus on top of the tiny flying Gulli; use large touch targets and color-blind-readable state text.

---

## 15. Matchmaking, bots and player interruptions

| System | Launch default |
|---|---|
| Public entry | **Play Now** queues 3v3 Street Clash |
| Casual queue fallback | After approximately **15 seconds**, fill available slots with labeled bots |
| PvP parties | Up to 3, same side when space permits |
| Co-op parties | Up to 4 |
| Disconnects | Bot takeover prevents hard match stalls |
| Reconnection | Attempt original-slot recovery for approximately 60 seconds |
| AFK | Warning, then bot takeover/queue removal |
| Map selection | Vote between rounds; avoid separate map queues |
| Ranked PvP | Post-launch possibility only |

AI levels: **Easy** (slow reaction/loose aim), **Normal** (reasonable pursuit and returns), **Hard** (better positioning and accurate throws). AI must chase, retrieve, throw and reasonably respect bounds; co-op AI also participates in set objectives. All bot players are visibly identified as bots.

---

## 16. Roblox technical architecture and persistent data

### 16.1 Server modules

| Module | Responsibility |
|---|---|
| MatchService | Queues, teams, countdowns, timeouts, rematches |
| RulesetService | Traditional, timed arcade and co-op state transitions |
| BattingService | Pop/swing validation, hit attempts, meter windows |
| GulliPhysicsService | Trajectories, rest state, swept Danda collisions and circle queries |
| FieldingService | Pickups, catches, passes, return throws |
| ScoreService | At-risk distance, banked team score, tie logic |
| AIService | Substitute players, AI fielders, co-op opponents |
| ProfileService | Coins, ownership, mastery, records, settings |
| QuestService | Daily, weekly, Rookie Journey and seasonal milestones |
| LockerService | Equipped cosmetics and VFX restrictions |
| RewardService | Anti-duplicate grants and receipt/claim validation |
| AnalyticsService | Funnel events and match outcome diagnostics |

Use documented remote APIs between client and server. Send player **intent**, not authoritative distance or reward values, from the client.

### 16.2 Persistent profile fields

Profile version, Coins, Rank XP/Level, owned Gulli IDs, owned Danda IDs, owned effect IDs, equipped slots, Rookie Journey stage, claim status, daily login streak progress, quest progress, personal-best valid distance, total match/win/catch/OUT stats, UI/accessibility options and seasonal progress.

Data saving must protect against duplicate reward claims, server shutdown, race conditions and reconnection duplicates. Version data layouts to support future content additions.

### 16.3 Performance and platform targets

- Aim for **60 FPS on capable desktops** and **30 FPS on supported lower-end phones**, measured on target devices.
- Keep particles scalable through quality settings and cull irrelevant distant cosmetics.
- Avoid unbounded Gulli physics simulation, heavy constant raycasts or expensive per-frame full-map pathfinding.
- Server tick and latency tests must specifically cover the Danda/circle precedence and fast return throws.

---

## 17. Analytics, balance and live operations

### 17.1 Internal launch targets

| Metric | Initial goal | Notes |
|---|---:|---|
| First valid hit within 60 seconds | 80%+ | Tutorial clarity |
| Active at 3 minutes | 55%+ | First-session survival |
| Active at 5 minutes | 40%+ | First-session survival |
| D1 return rate | 25%+ | Return on next day |
| D7 return rate | 8%+ | Return on seventh day |
| D30 return rate | 3%+ | Return on thirtieth day |
| Average session | 10–15 minutes | Long-term engagement hypothesis |

These are **working targets, not established Roblox benchmarks**. Use real cohort definitions and compare with Roblox Analytics after release.

### 17.2 Events to track

`tutorial_started`, `first_pop`, `first_valid_hit`, `first_throw`, `play_queue_entered`, `match_started`, `match_finished`, `out_direct_danda`, `circle_special_started`, `circle_special_succeeded`, `gulli_caught`, `distance_banked`, `quest_completed`, `daily_reward_claimed`, `rookie_set_claimed`, `locker_item_equipped`, `party_invite_sent`, `rematch_started`, `player_disconnected`.

Track time spent waiting on a batting turn, percentage of new players fielding successfully, failed throw rate, mobile hit accuracy relative to desktop, bot-fill rate, queue delay, co-op completion and reasons for match abandonment.

---

## 18. Roadmap, acceptance checks and QA

### 18.1 Phase 1 — playable core

**Deliver:** Pakistani Street greybox/polish pass; R15 batting, Gulli flight and bounce, retrieval/throw, Danda OUT, under-leg circle special, 3v3 Street Clash, basic AI, result screen and basic match telemetry.

**Gate:** six players can complete a fair match; fast collision outcomes are deterministic; a newcomer gets a first hit within one minute in structured playtests.

### 18.2 Phase 2 — full release scope

**Deliver:** all three selected themes and concept-art-driven environments; 1/3/5-minute and Traditional modes; co-op Distance/Target Smash; parties, quest and reward systems; complete cosmetic Locker; Day 3/7 sets; mastery ranks, shop and mobile HUD.

**Gate:** each mode completes without scoring/reward duplication; same cosmetics remain statistically equal; co-op and quests function across server restarts.

### 18.3 Phase 3 — ongoing content

**Deliver:** deeper rotating arcade challenges, additional cosmetic sets and OUT VFX, larger seasonal events, friend-team records, possible clubs and future ranked competition.

### 18.4 QA acceptance matrix

| Test | Pass criteria |
|---|---|
| Direct Danda throw | Immediate OUT, current at-risk points removed, correct next batter |
| Circle without Danda contact | Batter receives under-leg special, not direct OUT |
| Failed special | OUT state and next batter occur once |
| Safe outside-circle throw | Banks distance and continues in Traditional |
| Equal timed rotations | Both teams receive equal planned batting turns |
| Cosmetic equivalence | Same physical trajectories and reachable target geometry |
| Catch Out toggle | Only active in modes declaring the modifier |
| Player disconnect | Match continues with visible bot substitution |
| Double daily claim attempt | Rewards granted exactly once |
| Mobile device | Readable prompts, touch controls and acceptable performance |
| High ping throw | No phantom misses or duplicated Danda OUT |
| Out-of-bounds Gulli | Safe recover/reset without inflated score |

---

## 19. Visual appendix and production asset inventory

### 19.1 Illustrations included in this GDD

| Visual | Purpose | Asset |
|---|---|---|
| Pakistani Street concept art | Primary authentic-themed environment | `pakistani_street.jpg` |
| Backyard Arcade concept art | Bright target-focused arcade environment | `backyard_arcade.jpg` |
| Japanese Festival concept art | Festival event environment | `japanese_festival.jpg` |
| Gameplay flow | The five actions of a batting sequence | `gameplay_flow.png` |
| Arena schematic | Danda circle, origin, flight and return path | `arena_schematic.png` |
| Return outcomes | Direct OUT, special, SAFE | `return_outcomes.png` |
| Circle special: Gulli inside chalk ring | Trigger/positioning reference for traditional mode | `circle_special_gulli_in_circle.jpg` |
| Circle special: under-leg swing | Batter-exclusive follow-up action and Gulli launch | `circle_special_under_leg_hit.jpg` |
| Timing meter | Bad/Good/Perfect input concept | `timing_meter.png` |
| Cosmetic collection | Six Gulli and six Danda silhouettes | `cosmetic_collection.png` |
| Rank ladder | Seven permanent mastery tiers | `rank_ladder.png` |
| Day 3 and Day 7 rewards | Both signature collection sets | `reward_sets.png` |
| Retention timeline | Initial experience through D30 | `retention_timeline.png` |

**Art interpretation:** All included images are **concept illustrations or diagrams**, not screenshots of implemented gameplay or final production assets. The 3 arena illustrations were generated during requirements discussion; schematic diagrams were prepared specifically for this GDD.

### 19.2 Production asset breakdown

| Discipline | Needed assets |
|---|---|
| World art | 3 maps, target-circle materials, play boundaries, spectators, themed props, practice lane |
| Characters | R15-compatible equipment attachments and readable blocky avatar styling |
| Equipment | 6 Gulli, 6 Danda variants and their textures |
| Animation | Batting, pop, swing, under-leg special, movement, fielding, pickup, throw, catch, emotes |
| VFX | 5 hit bursts, 4 OUT effects, 5 flight trails, rank-up tiers, special/catch cues |
| UI | Main menu, lobby, mode selection, batting/fielding HUD, results, Locker, reward track, quests |
| Audio | Contact, pop, swing, flight, landing, OUT, special, UI feedback and map ambience |
| Engineering | State machine, authoritative physics, data storage, matchmaking, AI, analytics and anti-exploit |

### 19.3 Planned extension ideas (not required for launch)

Additional country-inspired maps, themed limited-time festival objectives, more Gulli skin collections, club progress, expanded co-op challenges and ranked seasonal PvP may follow once live usage data supports expanding the game.

---

*End of GDD — DAINTY, Version 1.0, updated with circle-special illustrations (26 October 2026).*
