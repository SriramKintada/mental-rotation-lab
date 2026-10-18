# Shepard & Metzler (1971) 3D Mental Rotation Lab

A mobile-friendly, high-precision cognitive psychology experimental suite replicating the classic Shepard and Metzler (1971) three-dimensional mental rotation paradigm with live server-side telemetry.

Live Demo: [https://authorities-memories-duration-chains.trycloudflare.com](https://authorities-memories-duration-chains.trycloudflare.com)

---

## Overview

In 1971, Roger Shepard and Jacqueline Metzler published a landmark study in *Science* demonstrating that visual imagery operations in the human brain rely on continuous, analog spatial transformations rather than discrete symbolic calculations.

This laboratory platform provides a browser-based, zero-latency replication of that experiment. It allows researchers and educators to measure individual and occupational differences in spatial rotation velocity across disciplines including Architecture, Software Engineering, Electronics Hardware, Mathematics, and Business Administration.

---

## Key Features

* **Mathematical 3D Isometric Polycubes:** Figures are rendered dynamically on an HTML5 canvas using true three-dimensional coordinate transformations, depth sorting (Painter's algorithm), and realistic multi-face lighting. No static images are used.
* **Balanced 20-Trial Factorial Matrix:** 
  $$\text{5 Angles } (0^\circ, 45^\circ, 90^\circ, 135^\circ, 180^\circ) \times \text{2 Parities } (\text{Identical vs. Mirrored}) \times \text{2 Repetitions} = 20 \text{ Trials}$$
* **Millisecond-Level Timing:** Response latency is captured to sub-millisecond precision using `performance.now()`.
* **Zero-Delay Touch Controls:** Uses `pointerdown` listeners and haptic feedback to prevent mobile tap delay.
* **Automated Linear Regression:** Automatically computes individual mental rotation slope ($k$ in milliseconds per degree) and plots the participant's empirical curve against the theoretical Shepard-Metzler benchmark.
* **Cloud Telemetry via Supabase:** All trial records and summary metrics sync in real time to a Postgres database with Row-Level Security.
* **Live Cohort Leaderboard:** An embedded telemetry viewer that groups and compares spatial rotation profiles across academic and professional disciplines.

---

## Experimental Protocol

1. **Onboarding:** The participant enters their name or alias and selects their professional background.
2. **Task Instruction:** The screen presents two 3D polycubes side by side (Figure A at $0^\circ$ baseline and Figure B rotated by angle $\theta$).
3. **Decision Rule:** Participants must decide as quickly and accurately as possible whether Figure B is identical to Figure A (can be rotated in 3D to match) or mirror-reversed (cannot match regardless of rotation).
4. **Data Acquisition:** The runtime captures reaction time (RT) and classification accuracy across all 20 randomized trials.
5. **Telemetry and Analysis:** The system calculates:
   * Mean reaction time at each angle ($0^\circ, 45^\circ, 90^\circ, 135^\circ, 180^\circ$)
   * Linear slope ($k$) via ordinary least squares regression
   * Overall accuracy percentage

---

## Empirical Observations (Cohort Findings)

In a live cross-disciplinary deployment ($N = 9$), the platform captured nuanced cognitive strategies:

* **Visual & Design Cohort:** Navya (Fine Arts) achieved 95% accuracy with steady 2 to 4 second reaction times ($k = +7.52\text{ ms}/^\circ$). Participants with spatial design backgrounds (Architecture and Electronics Hardware) exhibited flat or negative slopes (Saranya: $+1.95\text{ ms}/^\circ$, Vivek: $-9.79\text{ ms}/^\circ$, Devesh: $+1.21\text{ ms}/^\circ$).
* **Individual Trial Artifacts:** Analytical profiles (Mathematics and Software) showed positive slopes (Sriram: $+29.76\text{ ms}/^\circ$, Keertan: $+7.37\text{ ms}/^\circ$), though Sriram's slope was skewed by an accidental trial delay at $135^\circ$ ($10,230\text{ ms}$). Vignesh also exhibited an isolated spike at $45^\circ$.
* **Alternative Strategies & Fast Heuristics:** Anushka (Business Administration) attained 100% accuracy with an inverted slope ($-9.82\text{ ms}/^\circ$), relying on methodical corner feature verification. Harshith (Software Engineering) responded under 1,000 ms across all trials using a rapid visual heuristic.
* **Hobbies and Non-Academic Factors:** Beyond formal academic degrees, personal visual hobbies (such as fast-paced 3D video gaming and CAD modeling) strongly influence spatial rotation agility.

---

## Technology Stack

* **Frontend:** Vanilla HTML5, JavaScript (ES6+), Tailwind CSS
* **Vector Graphics:** HTML5 Canvas API with custom 3D isometric projection pipeline
* **Data Visualization:** Chart.js
* **Backend Database:** Supabase (PostgreSQL with Row Level Security)
* **Audio Feedback:** Web Audio API synthesizer

---

## Local Development

To run this experiment locally without external build tools:

```bash
# Clone the repository
git clone https://github.com/SriramKintada/mental-rotation-lab.git
cd mental-rotation-lab

# Start a local static file server
python -m http.server 3355

# Open your browser at http://localhost:3355
```

---

## Citation & Academic References

* Shepard, R. N., & Metzler, J. (1971). Mental rotation of three-dimensional objects. *Science*, 171(3972), 701-704.
* Cooper, L. A. (1975). Mental rotation of random two-dimensional shapes. *Cognitive Psychology*, 7(1), 20-43.
* Hegarty, M., et al. (2004). Spatial abilities at different scales of space. *Cognitive Processing*, 5(2), 69-80.
* Peters, M., et al. (1995). A redrawn Vandenberg and Kuse mental rotations test. *Brain and Cognition*, 28(1), 39-58.
