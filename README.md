# Rutgers Course Advisor Agent

An AI-powered Jupyter notebook that recommends Rutgers University courses based on your major and preferred class time, and pulls live professor ratings from RateMyProfessors.

---

## What It Does

1. Asks for your **major** and **time preference** (morning, afternoon, or evening)
2. Fetches matching courses from the **Rutgers Schedule of Classes API**
3. Looks up each professor's **difficulty score and rating** from RateMyProfessors
4. Saves a formatted report to `course_recommendations.md`

---

## Setup

### 1. Install dependencies
```bash
pip install -r requirements.txt
```

### 2. Configure environment variables

Copy `.env.example` to `.env` and fill in your values:
```bash
cp .env.example .env
```

| Variable | Description |
|---|---|
| `GITHUB_TOKEN` | Your GitHub Personal Access Token (used to access GitHub Models) |
| `GITHUB_MODEL_ID` | Model to use, e.g. `gpt-4.1-mini` |
| `GITHUB_ENDPOINT` | `https://models.inference.ai.azure.com` |

> To get a GitHub token: GitHub → Settings → Developer settings → Personal access tokens → Generate new token

### 3. Run the notebook

Open `classesagent.ipynb` in Jupyter or VS Code and run all cells. The last cell will prompt you:

```
What is your major? Computer Science
What time of day do you prefer? morning
```

---

## Supported Majors

Accounting, Biology, Chemistry, Civil Engineering, Computer Science, Data Science, Economics, Electrical Engineering, English, Finance, History, Linguistics, Management, Math, Mechanical Engineering, Philosophy, Physics, Political Science, Psychology, Sociology, Statistics

---

## Time Preferences

| Option | Hours |
|---|---|
| `morning` | Before 12:00 PM |
| `afternoon` | 12:00 PM – 5:00 PM |
| `evening` | 5:00 PM and later |
| `any` | No filter |

---

## Output

Results are saved to `course_recommendations.md` and include:

- A table of matching courses (title, course ID, instructor, time, day)
- Each professor's difficulty bar and star rating (out of 5)

---

## How It Works

The notebook uses two AI agents built with the `agent-framework-openai` library:

- **ScheduleCoordinator** — fetches courses from the Rutgers SOC API filtered by major and time
- **DifficultyExpert** — looks up professor ratings on RateMyProfessors and summarizes workload

---

## Notes

- Course data is pulled live from Rutgers for **Fall 2026, New Brunswick campus**
- Professor data is scraped from RateMyProfessors and may not be available for all instructors
