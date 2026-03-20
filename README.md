#  Energy Grid Simulator

This is a solo project, where I am teaching myself how to code/simulate an energy grid and control system using Python (Jupyter Notebook).

---

##  Wind Power Energy Grid Simulator

I chose an energy system simulator as it is something I haven't worked with before. However, it is something that interests me, so this project was a good opportunity to combine the two.

---

#  Phase One

- Simulate electricity demand over time (demand curve)  
- Simulate wind power generation over time  
- Plot both  

---

#  1. Demand Curve

A sinusoidal function is used to approximate daily demand since electricity usage follows a periodic 24-hour cycle.

- Low electricity usage at night  
- Rises in the morning  
- Peaks during the day/evening  
- Falls again (cycle repeats)  

A phase shift is included to better match real human activity patterns.

---

## Equation

```python
demand = 50 + 20*np.sin((hours - 7) * np.pi / 12)
```

---

## Breakdown

- **50** → baseline demand (always some usage)  
- **20** → amplitude (how much demand varies)  
- **π / 12** → sets a 24-hour cycle  
- **(hours - 7)** → shifts the peak to the evening (≈ 6–8pm)  

If it was just `sin(hours * π / 12)`, the peak would occur at midday.

> Note: the `7` acts as a time/phase shift.

---

#  2. Wind Model

```python
wind = 30 + 10*np.sin(hours * np.pi / 6) + 5*np.random.randn(len(hours))
```

---

## Key Idea

```
Wind = baseline + smooth variation + random noise
     = average level + predictable structure + what can't be predicted
```

- Any real-world signal can be decomposed into structured behaviour + randomness  
- Any smooth repeating signal can be approximated using sinusoids  

---

## Breakdown

###  Baseline

```python
30
```

- Represents average wind generation  
- Keeps wind output positive  

---

###  Smooth Variation

```python
10*np.sin(hours * np.pi / 6)
```

- Sinusoidal variation → models changing wind conditions  
- Form: sin(ωt)

Where:
- ω = π / 6  
- T = 2π / ω = 12  

→ **Time period = 12 hours**

**Why 12 hours?**
- Wind varies faster than demand  
- Weather systems change throughout the day  

---

###  Random Noise

```python
5*np.random.randn(len(hours))
```

- Random numbers from a Gaussian distribution  
- Models turbulence + measurement noise  

Properties:
- Most values are small  
- Occasional larger deviations  
- Symmetric around zero  

**Effect of “5”:**
- Small → smoother wind  
- Large → chaotic wind  
- 5 → moderate randomness  

---

##  Note

This is a **phenomenological model**:
- It captures behaviour, not underlying physics  
- The goal is realism + simplicity, not perfect accuracy  

---

#  Next Steps

- Add battery storage system  
- Implement control logic  
- Improve realism (constraints, limits, efficiency)
