# Campus Wi-Fi Coverage Optimization

**An interactive Python-based learning package for computational thinking, coding, debugging, and evidence-based design.**

This INT6064 project uses a simplified campus Wi-Fi planning scenario to help Secondary 3 students (adaptable to Secondary 4) learn how to translate a practical problem into a mathematical model, implement the model in Python, test their code, and justify an optimization decision. The package combines a three-lesson teaching sequence, a Tkinter application, printable learning resources, teacher references, and an optional command-line extension.

> **Educational simulation, not a real network-planning tool.** Each classroom is represented by one detection point. The model deliberately excludes walls, signal attenuation, interference, bandwidth, device capacity, and other real-world radio-frequency effects.

## Learning Goals

Students are guided to:

- Represent a physical setting with coordinates and detection points.
- Check router coverage using squared Euclidean distance and an inclusive boundary.
- Use sets to avoid counting overlapping coverage more than once.
- Calculate installation costs and normalized weighted scores.
- Compare all valid three-router combinations through guided exhaustive search.
- Debug logic errors using predictions, test evidence, and explanations.
- Explain how changing optimization priorities changes a recommended plan.

## The Optimization Challenge

The simulated campus contains **12 classroom detection points** and **7 candidate router sites (A–G)**. Students must choose **exactly 3 distinct router sites**. Each router has an ideal coverage radius of **3 grid units**, giving **35** unordered valid combinations.

A classroom point is covered when:

```text
(x_router - x_classroom)^2 + (y_router - y_classroom)^2 <= 9
```

For any valid selection, the model calculates:

- **Coverage ratio (Q):** uniquely covered detection points / 12
- **Installation cost (K):** sum of the selected router site costs
- **Normalized cost score (L):** 1 - K / 1100
- **Weighted score (F):** coverage_weight × Q + cost_weight × L

The default learning scenarios use coverage/cost weights of **100/0**, **70/30**, and **30/70**. Here, **1100** is the maximum cost of a valid three-router selection used for normalization; it is **not** a budget constraint. An optional extension explores hard budgets separately.

## Three-Lesson Learning Sequence

| Lesson | Focus | Learning activities |
| --- | --- | --- |
| **1 — From Campus to Model** | Unplugged reasoning throughout (no computers) | Plot detection points, calculate squared distances, handle boundary cases, and combine coverage sets. This lesson does not include TODO 1–2. |
| **2 — Basic Lab, Cost, and Scoring** | First use of the program; Basic lab | Open the GUI (Basic lab), complete TODO 1–2, then derive the 35 combinations and work through cost and scoring on paper. |
| **3 — Search and Evidence** | Optimization lab; algorithmic reasoning | In Optimization lab, implement cost and scoring expressions (TODO 3–5), run checks, investigate overlapping coverage, build guided exhaustive search (TODO 6), compare weight settings, debug decision logic, and export an evidence record. |

The sequence is designed around **three 40-minute lessons**, progressing from paper-based work to a coded model and then to evidence-based decision-making.

## Application Features

- **Basic Lab:** tasks for squared distance and the coverage condition.
- **Optimization Lab:** cost and score expressions, guided search blocks, debugging activities, and evidence export.
- **Student and teacher resources:** separate student-oriented materials and teacher reference answers/demonstrations.
- **Automated checks:** tests for the main application and its Stage 3 components.
- **Optional extension:** synthetic population coverage and hard-budget comparisons, run separately from the graphical application.

### Interface Preview

![Application menu](03_Illustrations/01_menu.png)

| Basic Lab | Optimization Lab |
| --- | --- |
| ![Basic Lab](03_Illustrations/02_basic_lab.png) | ![Optimization Lab](03_Illustrations/03_optimization_lab.png) |

Additional teacher-view screenshots are available in [`03_Illustrations/`](03_Illustrations/).

## Getting Started

### Requirements

- Python **3.10 or newer**
- **Tkinter** available in the Python installation
- No third-party Python package dependencies for the core application

Download or clone the repository, then open a terminal inside `02_Software/WiFi_Lab`.

**Windows:** double-click `Start_WiFi_Lab.bat` or run:

```powershell
py -3 main.py
```

**macOS / other supported environments:**

```bash
python3 main.py
```

From the main menu, choose **Basic Lab** or **Optimization Lab**. For classroom instructions, see [`INSTRUCTIONS.docx`](INSTRUCTIONS.docx) and [`00_Start_Here.docx`](00_Start_Here.docx).

## Project Structure

```text
INT6064_English_Package/
├── 00_Start_Here.docx
├── 00_Package_Index.docx
├── INSTRUCTIONS.docx
├── 00_Project_Coordination/     # Integration notes and historical verification
├── 01_Teaching_Materials/      # Three-lesson plans and student worksheets
├── 02_Software/
│   └── WiFi_Lab/
│       ├── main.py             # Application entry point
│       ├── Start_WiFi_Lab.bat  # Windows launcher
│       ├── run_tests.py        # Main test runner
│       ├── stage3/             # Guided optimization activities
│       ├── student_version/    # Student-facing version
│       └── teacher/            # Teacher demos and reference answers
├── 03_Illustrations/           # Application screenshots
├── 04_Mathematical_Model/      # Mathematical derivations and model tasks
└── 05_Optional_Extension/      # Synthetic population and budget resources
```

## Testing and Verification

Run the main test suite from `02_Software/WiFi_Lab`:

```bash
python3 run_tests.py
```

For the optional extension:

```bash
python3 -m unittest -v test_demand_extension
python3 demand_extension.py --budget 750
```

The packaged historical verification record reports **54 passing main-application tests** (10 base and 44 Stage 3) and **7 passing optional-extension tests**. These are recorded project results, **not a fresh verification of this uploaded package**. Automated test success does not establish GUI compatibility across screen sizes or effectiveness in a real classroom; no authentic classroom trial is documented in the supplied materials.

## Teaching and Responsible Use

The learning objective is not simply to find a set of router letters. Students should justify their answer with calculations and tests, distinguish an idealized model from reality, and explain trade-offs between coverage and cost. **Teacher answer keys and reference solutions should be kept separate from student handouts.**

This project is intended as a reusable classroom learning artifact, not as a validated system for real Wi-Fi deployment.
