# SLO Clone - Bias Calculator

A comprehensive tool for biasing EL34 power tubes in your SLO Clone 100W amplifier.

I built my SLO clone in 2021, and this repo is a small piece of practical knowledge I picked up along the way while getting deeper into amp-building as a hobby. There are a few photos from the build in the [img/](img/) folder.

## Contents

- [BIASING_GUIDE.md](BIASING_GUIDE.md) - Complete safety guide and measurement procedures
- [bias_calculator.ipynb](bias_calculator.ipynb) - Interactive Jupyter notebook calculator (Recommended)

## Quick Start

### Prerequisites

- Python 3.8 or higher
- Basic understanding of tube amplifier maintenance
- **Knowledge of high voltage safety procedures**

### Setup Instructions

1. **Clone or download this repository**
   ```bash
   cd ~/Documents/repos
   git clone <your-repo-url> slo-clone
   cd slo-clone
   ```

2. **Create a Python virtual environment**
   
   On **macOS/Linux**:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
   
   On **Windows**:
   ```bash
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install required packages**
   ```bash
   pip install --upgrade pip
   pip install jupyter matplotlib numpy ipywidgets
   ```

4. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook
   ```
   
   This will open your browser. Navigate to `bias_calculator.ipynb` and start calculating!

### Alternative: Using the Python Script

If you prefer a command-line tool instead of the notebook:

```bash
# Activate your venv first (see step 2 above)
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Interactive mode - walks you through each tube
python bias_calculator.py

# Quick calculation mode - single tube
python bias_calculator.py 480 36
# (480V plate voltage, 36mV bias reading)
```

## How to Use

1. **Read the [BIASING_GUIDE.md](BIASING_GUIDE.md) first!** It contains critical safety information and step-by-step measurement procedures.

2. **Take your measurements** with your amplifier warmed up:
   - Measure plate voltage (typically 450-500V)
   - Measure bias voltage at each test point (typically 30-45mV with 1Ω resistor)

3. **Enter values in the notebook**:
   - Open [bias_calculator.ipynb](bias_calculator.ipynb)
   - Run all cells up to "Your Turn: Enter Your Measurements"
   - Edit the values with your actual readings
   - Run the remaining cells to see analysis and visualizations

4. **Interpret the results**:
   - OPTIMAL: 65-75% dissipation - perfect
   - TOO COLD: Below 60% - increase bias
   - TOO HOT: Above 75% - decrease bias immediately

## Target Values for EL34

- **Maximum Dissipation:** 25W per tube
- **Safe Range:** 60-75% (15W - 18.75W)
- **Optimal:** 70% (~17.5W)
- **Typical Plate Voltage:** 450-500V
- **Typical Bias Current:** 30-45mA

## Safety Reminders

- Tube amplifiers contain **LETHAL VOLTAGES** (500V+)
- Only work inside the amp if you are qualified
- Always discharge filter capacitors before working
- Use one hand when probing
- If unsure, take your amp to a professional technician

## Features

- Calculates bias current from voltage readings
- Computes plate dissipation and percentage
- Color-coded status indicators
- Visual charts and graphs
- Multi-tube comparison and matching analysis
- Detailed recommendations for adjustment

## Deactivating the Virtual Environment

When you're done, deactivate the virtual environment:

```bash
deactivate
```

## Notes

- Check bias every 3-6 months or when changing tubes
- Use matched tubes for best performance
- Tubes in a pair should be within 2-3mA of each other
- Document your readings with dates

## Enjoy Your Tone

Stay safe and happy biasing!
