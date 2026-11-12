# PURRTRESS: Cucumber Siege. Game Plan

## 1. Pitch (one sentence)
Cats defend their cozy home from an endless cucumber invasion. It's tower defense where you **summon cats and merge matching ones** to evolve them, played one-handed in short runs.

## 2. Why this can work
| Proven mechanic | Our twist |
|---|---|
| Lane tower defense (Kingdom Rush: path, waves, spells) | Fewer decisions per second, so it fits a phone and a commute |
| Merge games (Merge Dragons, Merge TD) have high retention | Towers are *cats*: a viral, ad-friendly theme (cats vs cucumbers is a known meme) |
| Endless wave modes are replayable | "Just one more wave" loop, daily modifier runs, rankings |

Differentiator: **Summon -> Merge -> Spell** in 90-second micro-decisions. The player is never idle and never confused.

## 3. Core loop (3 to 8 minute run)
1. Tap **Summon**: a random cat lands on a free pad (cost rises each time).
2. **Drag identical cats together** (same type + tier) to merge into a stronger one. Different cats swap places.
3. Place cats side by side for **neighbor synergies**; store spares in storage slots (stored cats don't shoot).
4. Use **Hairball Bomb** (tap-to-aim spell, cooldown) on bosses or rushes.
5. Every 5th wave is a **boss** (two bosses from wave 20). Beating one offers a **run perk** (pick 1 of 3).
6. Die -> earn **Gems, XP, cat fragments (chest)** -> upgrade, shop, cards -> run again, stronger.

## 4. Content (status: built in `game.html`)
| Area | What exists |
|---|---|
| Cats | 10 types: 4 basic, 3 special (about 10% of summons), 3 shop cats. Tiers 1-6 with visible evolution (collar, cape, rays, crown/halo, wings). Tier 4 passive + Tier 6 ultimate for every cat. |
| Synergies | 8 named neighbor combos plus Twin Bond, Lucky Charm and Tip Jar. Glowing links on the board, panel info, Guide tab in the Shop. |
| Enemies | Cucumber, Mini, Pickle Tank, **Armored** (halves weak hits, burn ignores it), **Flying** (straight line to home, Claw Cats deal 40%), 4 bosses. "NEW ENEMY" banner on first sight. |
| Maps | Kitchen (no hazard), Garden (fertilizer speed patches), Bathroom (steam: cat range -12%), Rooftop (thunderstorm stuns cats). Unlock by reaching a wave on the previous map or skip with gems/ads. Reward multiplier x1 / 1.3 / 1.6 / 2. |
| Bosses | Robot Vacuum (regrowing dust shield), Lawn Mower (rev + dash), Mecha Duck (summons ducklings), Storm Drone (EMP stun), Frost Golem (event, chill aura). Coin burst, gem drops, first-kill bonus, fragment drops. |
| Run perks | 18 perks (damage/speed, economy, survival, risky trade-offs) in Common/Rare/Epic, stackable. Ad reroll. |
| Meta | Player level + XP, upgrades (damage, start coins, bomb, storage slots), Shop (3 cats, 6 skins), **Cat Cards** (10 levels, fragments from run chests and boss drops, milestones at Lv3/6/10). |
| Daily | Daily modifier run on a rotating map (8 rules, 1 free try + up to 3 ad retries), 7-day login streak, lucky wheel (1 free + 1 ad spin). |
| Missions | 3 daily missions (easy/medium/hard, x2 ad claim, +15 gem bonus), 16 achievements with Bronze/Silver/Gold, boss list. |
| Hero | **Captain Whiskers** (Shop: 150 gems or 8 ads, 5 upgrade levels). Guards the home with auto-slashes and has 2 tap abilities: 📣 Rally (cats shoot faster) and 😾 Yowl (stun + damage on all enemies). Ad recharge on cooldown. |
| Polish | First-run tutorial (5 steps, skippable, replay in Settings), pause + Settings screen, Nightmare mode (unlocks at wave 20: +60% HP, +15% speed, rewards ×2.5), Remove Ads (simulated IAP, interstitials only), buy fragments with gems, share score, `Analytics` seam (run_start, run_end, ad_view, purchase, share, tut_done). |
| Live | Season Pass (30 tiers, free + premium track, simulated purchase), **Frost Siege** event (Nov 1 - Jan 7: own map, blizzards, boss, snowflake milestones, exclusive skin), rankings (offline demo with simulated rivals). |

## 5. Monetization (ads-first)
| Placement | Type | Notes |
|---|---|---|
| Revive after defeat (once per run) | Rewarded | Highest-value, fully opt-in |
| Double gems + chest on game over | Rewarded | |
| Bomb recharge (instant) | Rewarded | Offered while the spell is on cooldown |
| Perk reroll | Rewarded | Once per perk offer |
| Mission claim x2 | Rewarded | |
| Daily extra attempts (max 3), bonus wheel spin | Rewarded | |
| Storage slot, map skip, shop cat/skin, bomb upgrade (progress counters) | Rewarded | Gem alternative for every unlock |
| Interstitial | Every 3rd game over, never mid-run, never in the first 3 runs | Protects retention |
| Premium Season Pass | IAP (stubbed, about $4.99) | `IAP.buy` seam |
| Remove Ads | IAP ($3.99, planned) | Removes interstitials only; rewarded stays |

Realistic expectation: a hyper-casual-style title earns roughly $1 to $4 eCPM-weighted per 1,000 sessions with rewarded video. Profit depends mostly on cheap installs (organic/viral clips), D1 retention above 35%, and 6+ rewarded views per 10 players per day. Plan to **test, measure, and iterate**, not to launch once.

## 6. Tech and release plan
- Prototype: single-file HTML5 canvas (`game.html`), portrait 9:16, no dependencies.
- Mobile wrap: **Capacitor** (Android first) + **AdMob** plugin. Integration seams already in the code: `Ads` (rewarded/interstitial), `IAP` (Play Billing), `Leaderboard` (Firebase / Play Games).
- Saves are in `localStorage` (`purrtress`). Missing fields migrate from defaults; verified with an old-format save.
- Daily/season/event logic uses the device clock. For launch, move those dates to a server (anti-cheat) together with rankings.
- Analytics: Firebase (D1/D7, ad impressions per session, funnel by wave).
- Android first (cheaper UA, faster review), iOS after the numbers look healthy.

## 7. Legal / IP
- Mechanics (path defense, waves, spells) are not protectable. We use **none** of Kingdom Rush's names, characters, art, or audio.
- All art/sound must be original or properly licensed (use CC0/commercial packs or generate custom art).
- Need: privacy policy, GDPR/UMP consent for AdMob, COPPA decision (target 13+ to avoid child-ad limits).

## 8. Open items before soft launch
1. Playtest on real phones (touch, performance on low-end devices).
2. Balance pass: gem/fragment/pass XP rates, Rooftop and event difficulty, perk strength, ability strength (Claw T6 is very strong in sims).
3. Art and sound pass (all art is procedural canvas drawing; sound is a placeholder synth with a mute toggle in the menu, plus vibration; replace with real music and SFX).
4. Hero balance: Captain Whiskers (built) needs a playtest pass: ability cooldowns, upgrade costs, Rally/Yowl strength.
4b. Heroes now: Captain Whiskers (Rally/Yowl), Merlin Meow (Meteor/Frost, 220 gems), Shadow Paw (Heist/Stab, 220 gems); equip one per run in the Shop. Not built yet: translations (needs a string table first), real privacy policy link, Firebase wiring for `Analytics`.
5. Capacitor + AdMob test ads, then closed beta on Google Play.
6. Soft launch in 2-3 small countries, measure D1/D7/ARPDAU. Scale only if D1 > 35% and ARPDAU > UA cost per user, otherwise iterate or sell the prototype/idea.
