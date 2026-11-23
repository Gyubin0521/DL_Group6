# Final Project – Task 1: Data Exploration & Service Idea

**Course:** Data Literacy Foundations (2026 Fall)
**Team:** [Team name] – [Name 1 (Student ID)], [Name 2 (Student ID)], [Name 3 (Student ID)]

Service direction: **a scholarship finder for university students.** A student enters school type, semester, major field and region of residence; the service filters the national student-aid catalog and returns the programs they can apply for (open now or usually opening soon), with amounts, deadlines and official links.

## Datasets

| | A. Selected | B. Compared candidate |
|---|---|---|
| Name | 한국장학재단_학자금지원정보(대학생) – KOSAF student financial-aid programs | 한국환경공단_전기차 충전소 위치 및 운영정보 – EV charging stations |
| Provider | Korea Student Aid Foundation (한국장학재단) | Korea Environment Corporation (한국환경공단) |
| Page | https://www.data.go.kr/data/15028252/fileData.do | data.go.kr, search "한국환경공단_전기차 충전소 위치 및 운영정보" (current API version: https://www.data.go.kr/data/15156662/openapi.do) |
| File version used | `_20261110` | `_20221027` |
| Size | 1,944 rows × 22 columns | 190,498 rows × 14 columns |
| Encoding | CP949 (EUC-KR) | UTF-8 with BOM |
| License | 이용허락범위 제한 없음 (no restriction on use) | public data from data.go.kr |

## Files

```
Task1_Report.pdf              # 3-page report
Task1_Report.docx             # same report, editable in Word
data_exploration.ipynb        # loads the data and reproduces every statistic, table and figure in the report
requirements.txt
data/
  scholarship_20261110.csv    # dataset A (renamed copy of the data.go.kr file, ~2 MB)
  sigungu_to_sido.csv         # district -> province lookup derived from dataset B (used to tag regions)
  ev_charger_20221027.csv     # dataset B – NOT committed (40 MB); see below
outputs/                      # written by the notebook
  fig1_timing_and_region.png
  table1_aid_type_summary.csv
  table2_feasibility.csv
  table_criteria_status.csv
```

Dataset A is small and has no usage restriction, so it is committed in `data/`. Dataset B is too large for a browser upload to GitHub (25 MB limit), so it is not committed. To re-run the dataset-B profile, download it from data.go.kr and save it as `data/ev_charger_20221027.csv`. Without it, the notebook skips that profile and uses the saved `data/sigungu_to_sido.csv`.

To use a newer monthly version of dataset A, download it from the data.go.kr page above and save it as `data/scholarship_20261110.csv`, or change `SCHOLARSHIP_CSV` and `REF_DATE` in the first code cell. Numbers will change.

## How to run

Requires Python 3.10+.

```bash
git clone <this repository URL>
cd <repository folder>
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook data_exploration.ipynb   # then: Kernel → Restart & Run All
```

To run it without opening the browser:

```bash
jupyter nbconvert --to notebook --execute --inplace data_exploration.ipynb
```

## Notebook contents

1. Candidate B profile: EV chargers (size, missing values, coverage); builds the district → province lookup
2. Dataset A profile: shape, column types, English column names, sample records, meaning of a record
3. Missing values and duplicates
4. Data-quality issues: glued multi-value fields, hidden missing values ("check with the organization"), GPA scales, region spellings, amounts, links, stale application rounds
5. Descriptive statistics
6. Preliminary EDA: region tagging, summary table by aid type, Figure 1, observations
7. Feasibility check of the core interaction (three example students)
8. Analytical questions for Task 2

## Report

`Task1_Report.pdf` (also submitted separately). Team repository: [GitHub URL]
