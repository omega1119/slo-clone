# SLO Clone 100W Bias Guide (EL34 Tubes)

## CRITICAL SAFETY WARNING

**HIGH VOLTAGE - LETHAL CURRENT**

- This amplifier contains voltages **EXCEEDING 500V DC** that can be **FATAL**
- High voltage remains in capacitors even after power is turned off
- **NEVER work inside the amp unless you are qualified and experienced**
- If you are not comfortable working with high voltage, **TAKE YOUR AMP TO A QUALIFIED TECHNICIAN**
- Always discharge filter capacitors before working inside
- Use only one hand when probing (keep other hand in pocket)
- Work on an insulated surface
- Have someone nearby in case of emergency

**By proceeding, you accept all risks. The author assumes no liability for injury, death, or equipment damage.**

---

## What is Tube Bias?

Biasing sets the idle current flowing through the power tubes. Proper biasing ensures:
- Optimal tone and performance
- Maximum tube life
- Prevents tube failure and damage to output transformer
- Prevents excessive heat and "red plating"

### EL34 Specifications
- **Maximum Plate Dissipation:** 25W per tube
- **Safe Operating Range:** 60-75% of max (15W - 18.75W per tube)
- **Typical Bias Current:** 30-45mA per tube
- **Recommended "Sweet Spot":** ~70% (17.5W per tube)

---

## Required Equipment

1. **Digital Multimeter (DMM)** - capable of measuring:
   - DC Voltage up to 600V
   - DC milliamps (or voltage across test points)
2. **Insulated test probes** - rated for high voltage
3. **Small flat-head screwdriver** - for adjusting bias pot
4. **Safety glasses**
5. **Insulated work surface**

---

## Measurement Points

Your SLO clone (per the schematic you shared earlier in this project) uses **paired** bias sense resistors:

- **Test Point J12** measures the **TOTAL current for the top pair** (V6.1 + V7.1) through **R49 (1Ω)**
- **Test Point J11** measures the **TOTAL current for the bottom pair** (V8.1 + V9.1) through **R50 (1Ω)**
- **Chassis ground** is the reference for both readings

You take **2 readings total** (J12 and J11). Each reading is for **both tubes combined**, so you **divide by 2** to estimate per-tube current.

---

## Measurement Procedure

### Step 1: Initial Setup
1. Turn off amplifier and unplug from mains
2. Remove back panel to access bias adjustment pot(s)
3. Ensure all tubes are properly seated
4. Set multimeter to **DC Voltage** mode
5. Connect black probe to chassis ground/common test point

### Step 2: Measure Plate Voltage
1. Power on amplifier (STANDBY ON, no signal)
2. **Let amp warm up for 2-3 minutes**
3. Locate plate voltage test point (if available) or:
   - Carefully measure from tube pin 3 (plate) to ground
4. Record plate voltage (typically 450-500V DC)
5. **This is B+ voltage - BE EXTREMELY CAREFUL**

### Step 3: Measure Bias Voltage
1. Keep amplifier on and warmed up
2. Measure voltage at each bias test point:
   - Place **RED probe** on test point (**J12**, then **J11**)
   - Place **BLACK probe** on ground/common
3. Record the voltage reading in **millivolts (mV)** or **volts (V)**

### Understanding the Reading:
- This SLO clone uses a **1Ω** (1 ohm) resistor per tube *pair* for bias measurement
- With a 1Ω resistor: **mV reading = mA of TOTAL pair current**
- Example: **60mV at J12 = 60mA total** through R49 = about **30mA per tube** (60mA ÷ 2)

Important nuance: this is **cathode current**, which includes a small amount of screen current. So the *true* plate current is slightly lower than the calculated cathode current.

### Step 4: Use the Calculator
1. Input your measured values into the Python calculator
2. Calculator will tell you:
   - Current bias current (mA) per tube
   - Current plate dissipation (W) per tube
   - Percentage of maximum dissipation
   - Whether adjustment is needed

### Step 5: Adjust Bias (if needed)
1. Locate bias adjustment pot(s)
   - The “hot” direction is whichever direction makes the **mV test-point reading go UP**
   - Pot direction is not universal; if turning clockwise makes the reading drop, your pot wiring/orientation is simply reversed
2. Make **SMALL adjustments** (1/8 turn at a time)
3. Wait 10-15 seconds for reading to stabilize
4. Re-measure and check calculator
5. Repeat until in optimal range

### Step 6: Final Check
1. Verify all tubes are in optimal range
2. Tubes in a matched pair should be within 2-3mA of each other
3. Turn off amplifier
4. Replace back panel
5. Document your readings and date

---

## Target Bias Settings

### Conservative (Cool) - 65% Dissipation
- **Plate Dissipation:** ~16W per tube
- **Bias Current:** ~32-35mA (at 480V plate voltage)
- **Tone:** Tighter, more headroom, longer tube life
- **Best for:** Clean tones, new tubes, hot environments

### Optimal (Recommended) - 70% Dissipation
- **Plate Dissipation:** ~17.5W per tube
- **Bias Current:** ~35-38mA (at 480V plate voltage)
- **Tone:** Balanced warmth and headroom
- **Best for:** All-around use, manufacturer recommendation

For this amp’s **paired test points** (single 1Ω resistor per pair), the **test point target is ~2× the per-tube current**:

- Example at **486V** plate voltage:
   - 70% target ≈ **36mA per tube** → **72mA per pair** → **~72mV at J11/J12**
   - 60% target ≈ **31mA per tube** → **62mA per pair** → **~62mV at J11/J12**
   - 75% target ≈ **39mA per tube** → **77mA per pair** → **~77mV at J11/J12**

### Warmer - 75% Dissipation
- **Plate Dissipation:** ~18.75W per tube
- **Bias Current:** ~38-42mA (at 480V plate voltage)
- **Tone:** Warmer, more compression, earlier breakup
- **Best for:** High-gain tones, experienced users

**NEVER exceed 75% dissipation - risk of tube failure**

---

## Troubleshooting

### Reading is Unstable/Fluctuating
- Tube may be microphonic or failing - replace tube
- Poor tube socket connection - clean socket contacts
- Inadequate warm-up time - wait longer

### Cannot Achieve Target Bias
If you can’t reach the target mV reading even with the pot turned fully “hot”, work through these in order:

1. **Confirm you’re measuring the correct node**
   - Meter in **DC mV**
   - Black lead on **chassis ground**
   - Red lead on **J11/J12**
   - If the test point is accidentally on the *ground side* of the 1Ω resistor, you’ll read near 0mV. If it’s on the correct side, you’ll read tens of mV.

2. **Confirm R49/R50 are actually 1Ω (power OFF, caps discharged)**
   - If the resistor value is not what you think, the “mV = mA” shortcut breaks.

3. **Confirm the pot is actually changing bias voltage**
   - Measure EL34 **control grid** voltage at **pin 5** (referenced to ground) while turning the bias pot.
   - You should see a meaningful sweep (often roughly around -35V to -55V depending on design).
   - If the voltage barely changes, the issue is likely in the bias supply/pot wiring/component values.

4. **Weak/aging tubes are extremely common**
   - Tubes can be biased “as hot as possible” and still not draw the expected current.
   - Quick test: try a known-good matched set and see if the attainable mV rises.

5. **Bias supply / component value issue** (tech-level)
   - Wrong resistor value in the bias divider, wrong pot value, failing diode/cap in the bias supply can all limit range.
   - If you’re not comfortable measuring the bias supply safely, this is the point to involve a qualified tech.

### One Tube Much Different Than Others
- Tubes may not be matched - get matched set
- Tube may be weak or failing - test/replace
- Socket or resistor issue - check connections

### Tubes Red Plating
- **TURN OFF IMMEDIATELY**
- Bias is too high (too much current)
- Possible short or failure
- Do not operate until corrected

---

## Maintenance Schedule

- **Check bias:** Every 3-6 months or when changing tubes
- **With new tubes:** Check bias immediately, then after 1 week, then after 1 month
- **Before important gigs/recordings:** Quick bias check
- **After long storage periods:** Check bias before extended use

---

## Notes

1. **Bias drifts over time** as tubes age - regular checks are essential
2. **Matched tubes** will track together and last longer
3. **Room temperature** affects bias - hotter room = hotter bias
4. Always use **matched quartet** of EL34s for best results
5. Keep records of your measurements with dates

---

## Quick Reference Card

```
EL34 Maximum Dissipation: 25W
Safe Operating Range: 15W - 18.75W (60-75%)
Optimal Target: 17.5W (70%)

Formula: Plate Dissipation (W) = Plate Voltage (V) × Bias Current (A)
Current (mA) = Voltage (mV) across 1Ω resistor

Example:
- Plate Voltage: 480V
- Bias Reading: 36mV (across 1Ω) = 36mA = 0.036A
- Dissipation: 480V × 0.036A = 17.28W
- Percentage: (17.28W / 25W) × 100 = 69% GOOD
```

---

## Support

For questions or issues, consult:
- Qualified tube amp technician
- The Amp Garage or other tube amp forums
- Original Soldano SLO specifications

**Stay safe and enjoy your tone!**
