---
name: health-interpreter
description: >
  Evidence-based Apple Watch and wearable health data interpreter. Transforms raw
  biometric data into actionable insights using personal baselines, composite scoring,
  cross-metric pattern detection, and research-backed decision trees. Covers HRV, resting
  HR, SpO2, sleep staging, respiratory rate, VO2max, walking HR, heart rate recovery,
  training load, and body composition. Calibrates to YOUR body — not population averages.
  Use when: interpreting health data, analyzing Apple Watch metrics, making training
  decisions from biometrics, understanding health trends, or any question like "what do
  my numbers mean?" NOT for: diagnosing medical conditions or replacing medical advice.
metadata:
  author: kris-puckett
  version: '1.0'
  evidence-date: '2026-03'
  license: MIT
---

# Health Interpreter

An evidence-based framework for interpreting wearable health data. Built from real
experience tracking health metrics through chronic illness, recovery, and performance
training — then abstracted into a system anyone can use.

**Core philosophy: orientation, not optimization.** Weekly trends matter more than
daily scores. Your body is your own reference point. Population norms are context,
not targets.

## Setup

1. Copy `profile-template.md` to your project and fill in your personal data
2. Establish your baselines over 14-28 days of normal life (instructions in the template)
3. Point the skill at your profile: reference the filled-in profile in your conversations

The skill works without a profile, but it's dramatically more useful with one.

---

## 1. The Orientation Model

Don't optimize. Orient. Every morning, check three things:

### The Three Questions

1. **Sleep duration** — Enough or not? (7+ hours is the goal)
2. **HRV trend** — 3-day direction (rising, stable, falling)
3. **Active disruptors** — GI issues, medication changes, illness, yesterday's strain, alcohol, poor sleep, high stress

### What the Answers Mean

| Sleep | HRV Trend | Disruptors | Capacity |
|-------|-----------|------------|----------|
| Good (7+ hr) | Rising or stable | None | **Full.** Push if you want to. |
| Good | Rising or stable | Minor (1 drink, mild stress) | **Near full.** Proceed but don't max out. |
| Short OR | Falling | — | **Reduced.** Protect energy. High-value work only. |
| Any | Any | Multiple active | **Recovery day.** Triage obligations. |
| — | Falling 3+ days | — | **Investigate.** Something changed — find it. |

This isn't a prescription to avoid things. It's situational awareness.

---

## 2. Metric Interpretation Framework

For every metric below, the same hierarchy applies:

### Comparison Order (Always)
1. **Your 28-day personal median** = primary anchor
2. **Your 7-day median vs 28-day median** = current state
3. **14-day slope** = intermediate trend direction
4. **Population norms** = secondary context only
5. **Illness/disruptor context** = if active, interpret metrics as temporarily suppressed

### Rolling Windows
- **7-day** = "How am I doing this week?" (acute state)
- **14-day** = "Are interventions working?" (require ≥10 valid data points)
- **28-day** = "What is my normal right now?" (re-lock only during stable periods)

**Re-baseline rule:** Only recalculate your 28-day baseline when ≥21 of 28 days are free from flares, travel, alcohol, acute illness, or major disruptions. Otherwise, keep the older stable baseline.

---

### 2A. Heart Rate Variability (HRV / SDNN)

**What it measures:** Parasympathetic nervous system tone. Higher = better recovery capacity.

**Critical device note:** Apple Watch reports **SDNN**, not RMSSD. Most competitors (Garmin, Oura, WHOOP) report RMSSD. These are different measurements with different norms — cross-device HRV comparisons are meaningless. The ESC Task Force 24-hour SDNN thresholds (50/100 ms) do NOT apply to Apple's short-epoch averaged SDNN [23].

**Apple Watch accuracy:** Underestimates SDNN by ~8 ms (MAPE 29%) [13]. Use 7-day rolling medians, never single readings. Trend direction is reliable; absolute values are not.

#### Threshold Zones (vs YOUR 28-day baseline)

| Zone | Range | Action |
|------|-------|--------|
| 🟢 Green | ≥ baseline | Planned training may proceed |
| 🟡 Yellow | 5-10% below | Reduce intensity one zone. Zone 2 only. |
| 🟠 Orange | 10-20% below | Easy movement or rest |
| 🔴 Red | >20% below, or 2-day collapse >25% | Full rest. Assess sleep, GI, stress, illness. |

#### Decision Rules
- HRV ≥ baseline → full planned training [2][3]
- HRV falls below 10-day mean minus 1 SD or 2-day downward trend → swap intensity for low intensity or rest [2]
- HRV >20% below for 3+ days → no threshold/tempo work, no hard lifting
- HRV improves for 14 days while RHR falls → interventions are working, even if VO2max lags
- HRV falling while deep sleep falls and GI symptoms worsen → likely vagal withdrawal from inflammatory stress [8][9]

#### What Tanks HRV
- Alcohol (even 1-2 drinks can suppress next-day HRV by 20-30%)
- Poor sleep (<6 hours or fragmented)
- Acute stress / sympathetic activation
- Illness / immune response
- Overtraining without recovery
- Stimulants close to sleep (pseudoephedrine, late caffeine)
- GI distress

#### What Improves HRV
- Consistent sleep timing (circadian alignment)
- Aerobic base training (zone 2)
- Cold exposure (evidence for acute parasympathetic activation)
- Iron repletion if deficient (restores oxygen delivery)
- Stress management / nervous system downregulation

---

### 2B. Resting Heart Rate (RHR)

**What it measures:** Cardiovascular efficiency and systemic strain. Lower is generally better.

**Why it matters:** RHR is independently and linearly associated with inflammatory markers (hs-CRP, IL-6, fibrinogen) in a dose-response relationship [7]. A rising RHR often signals inflammation before you feel sick.

#### Threshold Zones (vs YOUR baseline)

| Zone | Range | Interpretation |
|------|-------|---------------|
| 🟢 Green | Within +2 bpm | Stable |
| 🟡 Yellow | +3 to +4 bpm | Mild strain |
| 🟠 Orange | +5 to +7 bpm | Moderate strain |
| 🔴 Red | >+7 bpm for 3 days, or +10 bpm single day | Investigate immediately |

#### Decision Rules
- RHR rises >3 bpm AND HRV falls >10% → real physiologic strain, not device noise
- RHR rises >5 bpm but HRV unchanged and sleep was short → likely acute sleep debt
- RHR rises >5 bpm for >3 days with worsening symptoms → likely inflammatory process
- RHR rises while respiratory rate rises and SpO2 worsens → prioritize sleep/breathing investigation
- RHR drops toward pre-illness baseline → green light to cautiously add training volume

---

### 2C. Sleep

**Key components:**
- **Deep sleep (N3):** Physical restoration, growth hormone release. Target: 1-2 hours/night
- **REM:** Cognitive consolidation, emotional processing. Target: 1.5-2 hours/night
- **Sleep efficiency:** Time asleep / time in bed. Target: >85%
- **HR dip during sleep:** Heart rate should drop 10-20% (parasympathetic dominance)

**Apple Watch accuracy:** Deep sleep sensitivity is only 50.5% vs polysomnography — it systematically underestimates by ~43 minutes [14]. Treat Apple Watch deep sleep as a **floor estimate**. Sleep/wake detection accuracy is 93%, which is solid. Trust trends, not absolutes.

**Critical parsing note:** Apple Health stores "InBed" and "Asleep" as separate values. InBed ≠ Asleep. Including InBed in sleep totals inflates duration by 2-6 hours/night. This is the #1 Apple Health data parsing error.

#### Flags Worth Investigating
- HR dip <10% during sleep = sympathetic overdrive, poor recovery
- Deep sleep <45 min (Apple Watch reading) consistently = recovery debt building
- REM suppression = often alcohol, stress, or early waking
- Sleep efficiency <85% with low SpO2 and elevated respiratory rate = suspect sleep-disordered breathing

#### Decision Rules
- Total sleep <6 hr → automatically downgrade one training intensity level regardless of HRV
- Deep sleep <45 min (Apple Watch) for 3 of 7 nights and RHR elevated → incomplete parasympathetic recovery
- Deep sleep rises while HRV rises and RHR falls over 14 days → recovery genuinely improving
- Bedtime midpoint varies >90 min → circadian disruption; reset to ±30 min window

---

### 2D. SpO2 (Blood Oxygen)

**Apple Watch accuracy:** Limits of agreement ±2.7% to ±5.9%, with outliers up to 15% [15]. 14% of readings show <95% in healthy subjects when medical-grade oximeters read normal [16]. **Isolated low readings are meaningless.**

**Altitude matters:** See the altitude adjustment table in `profile-template.md`. At higher altitudes, SpO2 is naturally lower. Don't panic at 94% if you live at 5,000+ feet.

#### Pattern-Based Interpretation

| Pattern | Meaning | Action |
|---------|---------|--------|
| Overnight avg within your baseline range | Normal | Continue monitoring |
| Overnight avg drops 2+ points from personal norm | Something changed | Investigate: illness, sleep position, alcohol, congestion |
| Isolated reading of 92-93% but weekly mean stable | Device artifact | Ignore [15][16] |
| Low SpO2 clusters align with awakenings + elevated overnight HR | Sleep-disordered breathing | Sleep study recommended |
| Low SpO2 concentrated 11pm-6am with normal daytime | Possible sleep apnea | Overnight oximetry or home sleep study |
| Low SpO2 scattered across all hours equally | Sensor artifact | Check wrist contact, band tightness |

#### Decision Rules
- Never diagnose sleep apnea from Apple Watch SpO2 alone — use wearables to trigger testing urgency
- Single SpO2 readings <95% are not emergencies (especially at altitude)
- 3-night mean dropping ≥2 points → investigate
- Overnight mean <92% on repeated nights → urgent medical evaluation regardless of altitude

---

### 2E. Respiratory Rate

Respiratory rate during sleep is a sensitive but often overlooked metric.

| Zone | Range vs Baseline |
|------|-------------------|
| 🟢 Green | Within ±0.5 br/min |
| 🟡 Yellow | +0.6 to +1.0 |
| 🟠 Orange | +1.1 to +1.5 |
| 🔴 Red | >+1.5 for 3+ nights |

#### Decision Rules
- RR rises with low HRV and high RHR → systemic stress or inflammation
- RR rises with low SpO2 and fragmented sleep → breathing-related sleep disruption
- RR rises with GI symptoms (bloating, pain, reflux) → consider diaphragm restriction, sympathetic activation
- RR >20 sustained → assess for respiratory infection, worsening sleep-disordered breathing

---

### 2F. Walking Heart Rate

Walking HR is one of the most sensitive markers of cardiovascular fitness and systemic strain. It responds faster than VO2max to deconditioning or recovery.

| Zone | Range vs Baseline |
|------|-------------------|
| 🟢 Green | Within ±3 bpm |
| 🟡 Yellow | +4 to +6 bpm |
| 🟠 Orange | +7 to +10 bpm |
| 🔴 Red | >+10 bpm sustained for 7+ days |

#### Decision Rules
- Walking HR rises >5 bpm with unchanged step count → deconditioning, fatigue, or inflammation
- Walking HR rises while weight rises and HRV falls → reduced efficiency under inflammatory/metabolic load
- Walking HR falls over 14-28 days while cardiac drift stays low → aerobic recovery returning before VO2max improves
- Walking HR is often the FIRST metric to improve when an intervention is working — watch it weekly

---

### 2G. Heart Rate Recovery (HRR)

The drop in heart rate during the first minute after stopping exercise.

| HRR1 | Classification | Action |
|------|---------------|--------|
| >25 bpm | Good autonomic recovery | Positive signal |
| 18-25 bpm | Acceptable for most contexts | Continue protocol |
| 13-17 bpm | Below expected | Assess overtraining, illness, sleep quality |
| <12 bpm | **Abnormal** — associated with 4x increased mortality risk [11] | Rest. If persistent >1 week, medical evaluation. |

#### Decision Rules
- HRR1 <12 bpm on 2 standardized tests a week apart → autonomic recovery is impaired, reduce intensity [11]
- HRR worsens with low HRV and high RHR → autonomic dysfunction is real, not just detraining
- HRR worsens while overnight SpO2 is poor → sleep-disordered breathing becomes high priority

---

### 2H. VO2max (Watch Estimate)

**Apple Watch accuracy:** Underestimates by ~6 mL/kg/min (MAPE 13%) [18]. Underestimates fitter individuals more.

This is a **28-56 day trend metric only.** Ignore week-to-week fluctuations.

#### Decision Rules
- VO2max falls while weight rises but cardiac drift stays good → body-mass effect, not cardiac decline
- VO2max falls with rising walking HR, suppressed HRV, rising RHR, and lower capacity → true cardiorespiratory decline
- Ferritin <50 ng/mL and VO2max stalls → possible iron limitation, especially at altitude [19][20]
- Weight loss alone improves VO2max (same absolute capacity ÷ lower body mass = higher mL/kg/min)

---

### 2I. Cardiac Drift and Aerobic Decoupling

During sustained aerobic exercise, heart rate gradually rises even at constant effort. The rate of this drift indicates aerobic fitness.

| Drift % (over 50+ min) | Meaning | Action |
|------------------------|---------|--------|
| <3% | Excellent aerobic stability | Can extend duration or progress |
| 3-5% | Strong | Continue protocol |
| 5-8% | Moderate; possible high-strain day | If repeated: reduce intensity, check HRV/sleep |
| >8% | Significant | Probably above true aerobic zone, or: dehydration, poor fueling, illness |
| >10% | Above threshold or acute fatigue | Full rest day follows |

#### Cardiac Efficiency
Calculate per exercise session: average speed ÷ average heart rate. Track over time. Improving efficiency with the same HR = genuine aerobic adaptation.

---

### 2J. Training Load (TRIMP) and ACWR

The acute-to-chronic workload ratio (ACWR) is the most evidence-based tool for load management [10].

#### TRIMP Calculation
For cardio: TRIMP = duration(min) × HRr × 0.64 × e^(1.92 × HRr)
Where HRr = (avg HR - resting HR) / (max HR - resting HR)

For strength: sRPE Load = duration(min) × session RPE (0-10 scale)

#### ACWR Thresholds

| ACWR | Zone | Action |
|------|------|--------|
| 0.85-1.35 | Productive | Proceed with plan [10] |
| 1.36-1.50 | Caution | Monitor closely |
| 1.51-1.70 | High risk | Only if readiness is clearly green |
| >1.70 | Spike | Reduce load for next 3-7 days |
| <0.60 | Detraining risk (if >2 weeks) | Reintroduce load gradually |

#### Decision Rules
- ACWR >1.35 AND HRV down >10% → cap all training at easy/zone 2 for 72 hours
- ACWR >1.50 regardless of HRV → cancel hard workouts for the week [10]
- Low chronic load + acute spike = higher injury risk than same ACWR from high base
- ACWR <0.7 for >14 days → reintroduce gradually; don't perpetuate underloading

---

## 3. Composite Scores

### 3A. Morning Readiness Score (0-100)

Purpose: decide training intensity for the day.

| Component | Max Points | What It Measures |
|-----------|-----------|------------------|
| HRV vs 28-day baseline | 30 | Autonomic state |
| Resting HR vs 28-day baseline | 20 | Inflammatory strain |
| Sleep (quantity + efficiency + stages) | 20 | Recovery quality |
| Respiratory rate vs baseline | 10 | Systemic stress |
| Overnight oxygenation | 10 | Sleep-breathing burden |
| Prior-day training load vs chronic | 10 | Load management |

#### HRV Subscore (0-30)
- 7-day SDNN ≥ 28-day median → 30
- 5-10% below → 22
- 10-20% below → 12
- >20% below → 0

#### RHR Subscore (0-20)
- 7-day RHR ≤ baseline +1 bpm → 20
- +2 to +3 bpm → 14
- +4 to +5 bpm → 7
- >+5 bpm → 0

#### Sleep Subscore (0-20)
Start at 20, subtract:
- -6 if total sleep <6.5 hr (single night)
- -10 if total sleep <6.0 hr or <6.5 hr for 2+ consecutive nights
- -5 if deep sleep <45 min (Apple Watch reading)
- -5 if sleep efficiency <85%
- -4 if bedtime midpoint shifts >90 min from 28-day norm

#### Respiratory Rate Subscore (0-10)
- Within ±0.5 br/min of baseline → 10
- +0.6 to +1.0 → 7
- +1.1 to +1.5 → 3
- >+1.5 → 0

#### Oxygenation Subscore (0-10)
- Overnight mean SpO2 within normal range, no clustering → 10
- Slightly below normal or scattered lows → 7
- Below normal range or recurrent lows with fragmentation → 3
- Well below normal or frequent clustered lows → 0

#### Training Load Subscore (0-10)
- ACWR 0.85-1.35 → 10
- ACWR 1.36-1.50 or 0.70-0.84 → 7
- ACWR 1.51-1.70 or 0.60-0.69 → 3
- ACWR >1.70 or <0.60 → 0

#### Interpretation

| Score | Action |
|-------|--------|
| 85-100 | Proceed with planned training. Hard day allowed if no symptom flare. |
| 70-84 | Keep volume, reduce intensity one zone. Tempo → upper Zone 2. |
| 55-69 | Recovery-focused. Zone 1-2 only, easy lifting, or walk. |
| <55 | Rest or very easy walk. Investigate what's driving the low score. |

---

### 3B. Recovery Stability Score (Weekly, 0-100)

Purpose: detect whether your body is stabilizing or becoming fragile.

| Component | Target | Max Points |
|-----------|--------|-----------|
| HRV coefficient of variation (7-day) | ≤6% | 20 |
| RHR coefficient of variation (7-day) | ≤8% | 20 |
| Sleep midpoint standard deviation | ≤45 min | 20 |
| Sleep duration standard deviation | ≤45 min | 20 |
| Respiratory rate standard deviation | ≤0.7 br/min | 20 |

| Score | Interpretation |
|-------|---------------|
| 80-100 | Stable adaptation — your recovery environment is consistent |
| 60-79 | Unstable but manageable — look for the variable causing noise |
| <60 | Unstable recovery environment — reduce hard training 30-50% if sustained 2+ weeks |

---

### 3C. Systemic Strain Composite (0-12)

Purpose: detect wearable signatures of systemic inflammatory or autonomic strain.

Score 1 point for each present:

1. HRV 7-day median >10% below 28-day baseline
2. HRV 14-day slope still negative
3. RHR 7-day median >3 bpm above baseline
4. Walking HR >5 bpm above 28-day baseline at similar activity level
5. Respiratory rate >1 br/min above baseline
6. Deep sleep <45 min on 3 of last 7 nights
7. Sleep efficiency <85% on 3 of last 7 nights
8. Overnight mean SpO2 below your normal range on 3 of last 7 nights
9. HRR1 <12 bpm after standardized moderate effort
10. Active symptom flag (whatever your condition manifests as)
11. Weight up >1.5% over 7 days with lower activity and worse HRV
12. ACWR >1.35 while HRV is suppressed

| Score | Level | Action |
|-------|-------|--------|
| 0-2 | Low systemic strain | Continue protocol |
| 3-5 | Mild strain | Favor lifestyle correction (sleep, diet, stress) |
| 6-8 | Likely active inflammatory/autonomic strain | Reduce training, review triggers |
| 9-12 | High-probability flare state | Prioritize recovery and medical review if >72 hours |

---

## 4. Cross-Metric Pattern Detection

These patterns emerge when multiple metrics move together. Individual metrics fluctuate; clusters tell the story.

### Pattern 1: Inflammatory / GI Flare
**Cluster:** HRV ↓>10-20% + RHR ↑>3-5 bpm + deep sleep ↓ + RR ↑>1 br/min + walking HR ↑>5 bpm + symptoms
**Mechanism:** Inflammatory cytokines activate vagal afferents, triggering autonomic withdrawal. Sympathetic dominance raises HR and suppresses recovery [7][8][9].
**Action:** Remove hard training 48-72 hr. Clean up diet. No alcohol, late meals, or known triggers. If >7 days, escalate medically.

### Pattern 2: Sleep-Disordered Breathing
**Cluster:** Overnight SpO2 below normal or clustered dips + RR elevated + deep sleep low + fragmented sleep + RHR elevated on waking + HRV suppressed + daytime fatigue
**Mechanism:** Cyclical hypoxemia fragments sleep and triggers sympathetic activation.
**Action:** Prioritize overnight oximetry or home sleep study. Avoid alcohol and large late meals. Favor side-sleeping. Reduce training intensity.

### Pattern 3: Iron-Limited Adaptation
**Cluster:** Ferritin <50 ng/mL + VO2max stagnant over 28-56 days + higher exercise HR at usual effort + fatigue despite some good HRV mornings + slower recovery after hard work
**Mechanism:** Low iron limits erythropoietic response, especially at altitude [19][20].
**Action:** Keep most work aerobic until ferritin improves. Track exercise HR at a fixed route for decoupling trends. If oral iron fails in 4-6 weeks, discuss IV iron with your doctor.

### Pattern 4: Overreaching / Load Spike
**Cluster:** ACWR >1.35 (especially >1.50) + HRV ↓>10% + RHR ↑>3 bpm + cardiac drift worsening + subjective soreness/fatigue
**Action:** Cut weekly load 30-50%. Easy movement only. Resume intensity after HRV/RHR normalize for 3+ days [10].

### Pattern 5: Positive Adaptation
**Cluster:** HRV trending up over 14 days + RHR trending down + walking HR decreasing + sleep duration/regularity stable + cardiac drift ≤3-4% + VO2max stable or rising over 28-56 days
**Meaning:** Genuine improvement in autonomic efficiency and aerobic economy.
**Action:** Progress volume 5-10% per week max. Add intensity only if ACWR ≤1.35 and recovery metrics stable.

### Pattern 6: Pre-Symptomatic Relapse Detection
**Cluster:** Gradual HRV decline over 3-5 days + slow RHR elevation + increased sleep fragmentation + reduced deep sleep — all BEFORE overt symptoms appear
**Mechanism:** Autonomic withdrawal often precedes symptom onset by days. If you have a chronic condition with flare patterns, your wearable may catch the decline before you feel it.
**Action:** If these markers trend negatively for 3-5 consecutive days, pre-emptively tighten your management protocol. Don't wait for symptoms to confirm what the data already shows.

---

## 5. Daily Decision Tree

### Step 1: Medical Red-Flag Gate
IF ANY of the following → skip training, seek medical attention:
- Chest pain, syncope, new irregular heartbeat
- Severe shortness of breath at rest
- Persistent resting SpO2 ≤90%
- Overnight mean SpO2 <92% on repeated nights with symptoms
- HRR1 <10 bpm repeatedly plus marked exercise intolerance
- RHR >10 bpm above baseline for >3 days with systemic illness signs

### Step 2: Compute Morning Readiness Score
- ≥85 → full planned training
- 70-84 → reduce intensity one category
- 55-69 → recovery session only
- <55 → rest

### Step 3: Condition-Specific Overrides
These are personal — fill them in based on your health profile:
- IF [your condition] flares AND Strain Composite ≥6 → no hard training even if readiness >70
- IF overnight oxygenation poor → no threshold/VO2 work
- IF ACWR >1.50 → no intensity regardless of readiness
- IF ferritin low and fatigue high → aerobic maintenance, not performance chasing

### Step 4: Choose Activity Level
| Readiness + Context | Activity |
|-------------------|----------|
| Green + stable recovery + ACWR ≤1.35 | Hard training OK (tempo, threshold, heavy lifting) |
| Yellow | Moderate only (zone 2, moderate lifting) |
| Orange | Easy movement (walking, mobility, technique work) |
| Red | Full recovery |

---

## 6. Research Integrity Rules

These rules are non-negotiable. They're what separate useful health interpretation from noise.

1. **No fabricated citations.** Every claim references real, published research. If no evidence exists, say so. See `references/evidence-base.md` for the full citation list with study quality ratings.

2. **Classify evidence strength.** Always note whether a recommendation is based on:
   - **Strong** evidence (RCT, meta-analysis, large prospective cohort)
   - **Moderate** evidence (observational, systematic review of observational)
   - **Limited** evidence (expert consensus, case series, mechanistic reasoning)

3. **Individual baselines over population norms.** Your 28-day median is more informative than any percentile chart. Population norms provide context; they don't define your health.

4. **Device accuracy awareness.** Apple Watch is a consumer device, not medical equipment. Know its limits (see accuracy table below) and don't over-interpret noise.

5. **Never diagnose.** Interpret and flag for medical review. "This pattern is consistent with X — discuss with your doctor" is appropriate. "You have X" is not.

6. **Actionable thresholds must clear BOTH physiologic and device noise.** A single-day HRV change of 5% could be real or could be measurement error. Sustained changes over 3+ days that exceed device noise margins are meaningful.

### Apple Watch Accuracy Reference

| Metric | Accuracy vs Gold Standard | Key Limitation | Practical Rule |
|--------|--------------------------|----------------|----------------|
| Heart Rate (rest/walk) | Mean bias -0.27 bpm, LoA ±7 bpm [17] | Worsens at high intensity | Trust for Zone 2 and resting. Caution during HIIT. |
| HRV (SDNN) | Underestimates ~8 ms, MAPE 29% [13] | Not clinically equivalent | 7-day rolling medians only. Trend > absolute. |
| SpO2 | LoA ±2.7% to ±5.9%; 14% false-lows [15][16] | Isolated dips are artifacts | Overnight averages and clustering only. |
| Sleep staging | 93% sleep/wake; deep sleep sensitivity 50.5% [14] | Underestimates deep by ~43 min | Treat as floor estimate. Trends > absolutes. |
| VO2max | Underestimates ~6 mL/kg/min, MAPE 13% [18] | Underestimates fitter people more | 28-56 day trend metric only. |

### Actionable Threshold Rules
A single-day deviation is actionable ONLY if it exceeds both physiologic and device noise:
- HRV change >20%
- RHR change >5 bpm
- Respiratory rate change >1.5 br/min
- SpO2 drop >3 points from personal baseline
- Deep sleep change >30 min

Below these thresholds, wait for 3+ day trends before acting.

---

## 7. Iron Deficiency — A Special Note

Iron deficiency without anemia is one of the most under-recognized performance limiters, especially for:
- People living at altitude (increased erythropoietic demand)
- Active individuals (exercise increases iron losses)
- People on PPIs or acid-reducing medications (impaired absorption)
- Women with regular menstrual cycles

**Key timeline for supplementation response:**
- Hemoglobin response: 2-4 weeks
- Ferritin repletion: 3-6 months
- HRV improvement: typically follows ferritin recovery by 4-8 weeks
- Target ferritin: ≥50 ng/mL for active individuals; ≥50 ng/mL minimum at altitude [19][20]

People often give up iron supplementation after 4-6 weeks because they don't feel different yet. Ferritin recovery takes months. Stay the course.

---

## 8. Fringe-But-Plausible Interventions

These have emerging evidence but aren't fully mainstream:

- **Mouth taping for sleep:** May improve nasal breathing, reduce snoring. Some evidence for better sleep quality and SpO2.
- **Morning sunlight exposure:** Strong circadian evidence. 10-30 min within 1 hour of waking.
- **Cold exposure:** Acute HRV boost, mental resilience. Evidence is real but effect is transient.
- **Continuous glucose monitoring:** Useful for identifying personal glycemic responses. Not necessary for everyone.

---

## Output Format

When interpreting data, produce:

```
STATUS: [Green/Yellow/Orange/Red] — Readiness: [X]/100
TOP DRIVERS: [Top 3 metrics driving the score]
PATTERN: [inflammatory / sleep-breathing / load spike / iron-limited / positive adaptation / pre-symptomatic / mixed / none detected]
TRAINING TODAY: [full / modified / recovery / rest] — [specific suggestion]
MEDICAL FLAGS: [none / monitor / test soon / seek care] — [details if any]
TREND READOUT:
  7-day: [summary]
  14-day: [summary]
  28-day: [summary]
THRESHOLDS CROSSED: [list any exceeded thresholds]
```

---

## Citation Key

All bracketed numbers (e.g., [7]) reference entries in `references/evidence-base.md`.
Every recommendation in this skill traces back to published research with quality ratings.

---

*Built from real experience interpreting health data through chronic illness, recovery,
and performance training. The methodology is what matters — fill it with your own data
and it becomes yours.*
