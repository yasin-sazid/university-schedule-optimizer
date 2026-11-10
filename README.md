# University Schedule Optimizer

A constraint-programming notebook for assigning university classes to rooms and time slots while balancing scheduling preferences. The project translates spreadsheet-based academic scheduling information into an OR-Tools CP-SAT model.

## Scheduling approach

The notebook reads classroom, time-slot, faculty, and existing schedule information, normalizes course/section identities, expands weekday representations, and encodes candidate rooms and slots as integer decision variables.

The model combines allowed assignments with weighted preference penalties. Implemented preference logic includes room/time continuity for senior academic designations, adjunct time preferences, ordinary time preferences, building selection, and back-to-back building transitions. The notebook exposes these rules alongside their penalty weights, making the mapping from scheduling policy to solver expressions inspectable.

## Data workflow

```text
Excel inputs → pandas preparation → Room/slot encoding → CP-SAT constraints
                                                              |
                                                    Weighted objective
                                                              |
                                                      Solver output
```

## Input artifacts

Provide the spreadsheets referenced by [university_scheduling.ipynb](university_scheduling.ipynb):

- `data.xlsx`, with `classrooms`, `slots`, and `faculties` sheets.
- `sample_schedule.xlsx`, with the schedule in `Sheet1`.

The notebook uses classroom attributes such as `Room`, `Theory/Lab`, and `Size`; slot information includes `Time From`, `Time To`, and `Weekday`. Schedule preparation uses `Course`, `Section`, and `Instructor`, while faculty data supplies instructor initials and designation.

## Explore and run

Use Jupyter or the Colab entry in the notebook with pandas, OR-Tools, and an Excel-reading engine:

```bash
python -m pip install jupyter pandas ortools openpyxl
jupyter notebook university_scheduling.ipynb
```

Place the input workbooks in the notebook's working directory and execute cells in order. The solution workflow writes `final_schedule_output.xlsx` and prints room usage and preference-penalty information. [Scheduling_Code_Overview.pdf](Scheduling_Code_Overview.pdf) accompanies the implementation.

## Technical contribution

The project connects institutional scheduling preferences to explicit decision variables, conditional constraints, and weighted penalties, illustrating how constraint programming can make academic timetabling policies computationally actionable.
