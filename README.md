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

In a live cross-disciplinary deployment ($N = 9$), the platform captured rich qualitative and quantitative cognitive strategies:

* **No Binary Disciplinary Separation:** Performance did not divide cleanly along formal academic lines. Instead, participants represented combinations of formal coursework, cognitive heuristics, and personal visual hobbies.
* **Standout Visual Performance (Navya):** A Fine Arts student was the fastest deliberate responder (mean 3,122 ms) and achieved the highest accuracy among visual disciplines (95%), calmly resolving complex orientations without stumbling at large angles.
* **Abstract Coordinate Projection (Vivek):** Working in abstract mathematics and topology, Vivek was exceptionally fast (mean 2,801 ms, dropping to 1,491 ms at 90° and 1,515 ms at 135° with 70% accuracy), applying instantaneous mental coordinate transformations rather than manual degree-by-degree rotation.
* **Architecture and Hardware (Saranya & Devesh):** Saranya was medium-fast (median 2,058 ms), but her accuracy dropped to 65% after being tripped up by the 45° oblique view (7,623 ms). Devesh was deliberate and flat ($k = +1.21\text{ ms}/^\circ$) with 75% accuracy (4,500 ms average). Formal architecture training alone did not guarantee both top speed and accuracy.
* **3D Gamers (Harshith & Keertan):** Software students with active 3D gaming hobbies showed strong spatial competence. Harshith exhibited sub-second twitch reflexes (605 ms average, 65% accuracy), while Keertan was deliberate and methodical (5,039 ms, 85% accuracy).
* **Future Methodological Directions:** Future studies should recruit larger, dedicated cohorts of professional architects and competitive 3D gamers with a 100-trial battery to rigorously isolate gaming reflexes from formal architectural drafting skills.

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
