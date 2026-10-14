<div align="center">

# ResumeIQ

### AI-Assisted Resume Screening & Candidate Ranking System

[![Python](https://img.shields.io/badge/Python-3.12%2B-3776AB?style=for-the-badge\&logo=python\&logoColor=white)](https://www.python.org/)

[![FastAPI](https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge\&logo=fastapi\&logoColor=white)](https://fastapi.tiangolo.com/)

[![Pytest](https://img.shields.io/badge/Pytest-Tested-0A9EDC?style=for-the-badge\&logo=pytest\&logoColor=white)](https://docs.pytest.org/)

[![Status](https://img.shields.io/badge/Status-Active%20Development-2E7D32?style=for-the-badge)](#)

**Explainable candidate ranking with direct and semantic skill matching, resume uploads, and recruiter-ready screening insights.**

[Quick Start](#quick-start) •

[Features](#features) •

[Demo](#demo) •

[API](#api-documentation) •

[Project Structure](#project-structure)

</div>

## Why This Project

Manual resume screening can be time-consuming and difficult to evaluate consistently, especially when recruiters need to compare multiple technical candidates against the same job requirements.

**ResumeIQ** provides a structured screening workflow that:

* Accepts job requirements and candidate resumes.
* Extracts candidate profile information automatically.
* Detects and normalizes technical skills from resume content.
* Matches candidate skills directly against job requirements.
* Identifies related skills using a semantic skill relationship graph.
* Calculates transparent scores using required skills, must-have skills, nice-to-have skills, and experience.
* Highlights strengths, missing skills, concerns, and semantic evidence.
* Allows recruiters to compare candidates side-by-side.

## Features

| Capability              | Description                                                                                                         |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Explainable Ranking     | Returns matched skills, missing skills, strengths, concerns, hard-constraint status, and semantic evidence.         |
| Role-Aware Scoring      | Supports `backend`, `frontend`, `data_ai`, `devops`, and `fullstack` job categories.                                |
| Resume Parsing          | Processes `PDF`, `DOCX`, and `TXT` resume files.                                                                    |
| Auto Profile Extraction | Extracts candidate name, years of experience, and detected technical skills from resume content.                    |
| Skill Normalization     | Handles skill aliases such as `React.js` → `React`, `HTML5` → `HTML`, `CSS3` → `CSS`, and `Express` → `Express.js`. |
| Semantic Skill Matching | Uses predefined relationships between related technical skills to identify relevant semantic evidence.              |
| Hybrid Scoring          | Combines direct skill evidence with weighted semantic evidence.                                                     |
| Hard-Constraint Check   | Identifies whether direct must-have skill coverage meets the configured threshold.                                  |
| Drag-and-Drop Upload    | Recruiters can upload resumes directly through the dashboard.                                                       |
| Comparison View         | Compare two candidates using score components and supporting evidence.                                              |
| Recruiter Dashboard     | Provides a centralized interface for job context, candidate screening, ranking, and comparison.                     |

## Supported Job Roles

ResumeIQ currently supports five job-role categories:

1. Backend
2. Frontend
3. Data/AI
4. DevOps
5. Full Stack

The role family can be selected manually or inferred from the job title and job description.

## Screening Workflow

```text
Job Requirements + Candidate Resumes
                ↓
          Resume Processing
                ↓
      Candidate Information Extraction
                ↓
       Skill Extraction & Normalization
                ↓
          Direct Skill Matching
                ↓
         Semantic Skill Matching
                ↓
           Weighted Scoring
                ↓
        Hard-Constraint Check
                ↓
         Candidate Ranking
                ↓
      Explainable Recruiter Insights
```

## Scoring Approach

ResumeIQ evaluates candidates using four major scoring components:

* **Required Skills**
* **Must-Have Skills**
* **Nice-to-Have Skills**
* **Experience**

The scoring weights vary by job-role category.

The system distinguishes between:

### Direct Skill Match

A skill is directly matched when the candidate's resume explicitly contains the required skill after normalization.

### Semantic Skill Match

A semantic match is identified when the candidate has a related skill connected through the project's predefined semantic skill relationship graph.

For example:

```text
Git
 ↓
GitHub
```

If a job requires GitHub and the candidate explicitly lists Git, the system can provide semantic evidence rather than treating the relationship as an exact match.

## Explainability

ResumeIQ does not return only a numerical score. For every candidate, the system provides supporting information such as:

* Direct Skill Matches
* Semantic Evidence
* Missing Skills
* Strengths
* Concerns
* Hard-Constraint Status
* Required Skill Score
* Must-Have Match Rate
* Nice-to-Have Match Rate
* Experience Score
* Overall Score

This allows recruiters to understand the evidence behind the candidate ranking.

## Demo

### Dashboard

The ResumeIQ dashboard provides:

* Job Context configuration
* Job-role selection
* Must-have and nice-to-have skill inputs
* Resume text input
* PDF/DOCX/TXT upload
* Candidate profile preview
* Candidate ranking
* Explainable screening results
* Candidate comparison

### Screenshot

Replace this placeholder with your final ResumeIQ dashboard screenshot:

`docs/media/resumeiq-dashboard.png`

## Architecture

```text
┌─────────────────────────────────────────────┐
│                ResumeIQ Dashboard           │
│        HTML + CSS + JavaScript              │
└──────────────────────┬──────────────────────┘
                       ↓
┌─────────────────────────────────────────────┐
│                 FastAPI API                 │
│       Job Context + Candidate Requests      │
└──────────────────────┬──────────────────────┘
                       ↓
┌─────────────────────────────────────────────┐
│            Resume Processing                │
│          PDF / DOCX / TXT Parsing           │
└──────────────────────┬──────────────────────┘
                       ↓
┌─────────────────────────────────────────────┐
│       Candidate Profile Extraction          │
│     Name + Experience + Technical Skills    │
└──────────────────────┬──────────────────────┘
                       ↓
┌─────────────────────────────────────────────┐
│       Skill Extraction & Normalization       │
│        Canonical Skills + Skill Aliases      │
└──────────────────────┬──────────────────────┘
                       ↓
┌─────────────────────────────────────────────┐
│          Semantic Skill Matching             │
│        Related Skill Relationship Graph      │
└──────────────────────┬──────────────────────┘
                       ↓
┌─────────────────────────────────────────────┐
│              Scoring Engine                  │
│ Required + Must-Have + Nice-to-Have + Exp.  │
└──────────────────────┬──────────────────────┘
                       ↓
┌─────────────────────────────────────────────┐
│          Candidate Ranking & Insights        │
│  Score + Evidence + Strengths + Concerns    │
└─────────────────────────────────────────────┘
```

## Quick Start

### Windows PowerShell

From the project directory:

```powershell
Set-Location "C:\Users\91845\Desktop\TalentRank-Studio-AI-Resume-Screening-main"

.\.venv\Scripts\Activate.ps1

$env:PYTHONPATH = "src"

uvicorn app.main:app --host 127.0.0.1 --port 8001 --reload
```

Open:

* Dashboard: `http://127.0.0.1:8001/`
* API Docs: `http://127.0.0.1:8001/docs`

### Linux/macOS

```bash
python -m venv .venv

source .venv/bin/activate

python -m pip install --upgrade pip

python -m pip install -r requirements.txt

PYTHONPATH=src uvicorn app.main:app --host 127.0.0.1 --port 8001 --reload
```

## API Documentation

Base URL:

`http://127.0.0.1:8001`

### Health Check

* `GET /v1/health`

### Analyze Text Candidates

* `POST /v1/analyze`
* Input: JSON payload containing job context and candidate resume text.

### Analyze Uploaded Resumes

* `POST /v1/analyze-files`
* Input: multipart form containing resume files.

### Preview Uploaded Resume Profiles

* `POST /v1/preview-files`
* Input: multipart form containing resume files.
* Output: parse status, candidate name, years of experience, and detected skills.

## Example Request Payload

```json
{
  "job_title": "Backend Python Engineer",
  "job_description": "Looking for Python, FastAPI, Docker, PostgreSQL, and AWS experience.",
  "role_family": "backend",
  "must_have_skills": ["python", "fastapi"],
  "nice_to_have_skills": ["aws"],
  "candidates": [
    {
      "name": "Alex",
      "resume_text": "Built Python APIs with FastAPI and Docker, deployed on AWS with PostgreSQL.",
      "years_experience": 4
    }
  ]
}
```

## Demo Data

The project can be tested using:

* Backend job descriptions
* Candidate resume samples
* PDF resume files
* Candidate comparison scenarios
* Resume upload testing

Supported resume formats:

```text
PDF
DOCX
TXT
```

## Project Structure

```text
src/app/

    api/routes.py              # FastAPI endpoints

    services/scoring.py        # Ranking and weighted scoring logic

    services/skill_taxonomy.py # Skill extraction, normalization,
                               # aliases, and semantic relationships

    services/resume_parser.py  # Resume parsing and profile extraction

    web/static/                 # ResumeIQ dashboard frontend

    schemas.py                  # Request/response models

    main.py                     # Application entrypoint

demo_assets/

    job_descriptions/

    resumes/

    resumes_pdf/

portfolio_assets/              # Demo and portfolio materials

scripts/                       # Setup and demo utility scripts

tests/                         # Unit and endpoint tests
```

## Testing

Activate the virtual environment and run:

```powershell
Set-Location "C:\Users\91845\Desktop\TalentRank-Studio-AI-Resume-Screening-main"

.\.venv\Scripts\Activate.ps1

$env:PYTHONPATH = "src"

pytest -q
```

The project has also been manually tested for:

* Backend role screening
* Frontend role screening
* Data/AI role screening
* DevOps role screening
* Full Stack role screening
* Direct skill matching
* Semantic skill matching
* Missing-skill identification
* Candidate comparison
* PDF resume uploads
* DOCX resume uploads
* TXT resume uploads
* Automatic candidate name extraction
* Automatic experience extraction

## Troubleshooting

### Error: Failed to fetch

* Ensure the FastAPI backend is running.
* Open the dashboard from:

`http://127.0.0.1:8001/`

* Refresh the browser using `Ctrl + Shift + R`.
* If the server is not running, start it with:

```powershell
$env:PYTHONPATH = "src"

uvicorn app.main:app --host 127.0.0.1 --port 8001 --reload
```

## Future Enhancements

* Export shortlist reports in CSV/PDF format
* Authentication and recruiter workspaces
* Project-level screening history
* Audit trail for screening decisions
* Configurable scoring templates
* Additional job-role categories
* Advanced NLP-based resume analysis
* Education and certification matching
* ATS integration
* Bias and fairness monitoring
* Integration with trained machine-learning/NLP models

## Project Objective

The objective of ResumeIQ is to demonstrate an explainable and structured approach to technical resume screening.

The system combines:

```text
Skill Extraction
      +
Skill Normalization
      +
Semantic Skill Relationships
      +
Weighted Scoring
      +
Candidate Ranking
      +
Explainable Insights
```

ResumeIQ is designed as a **decision-support system**. It provides recruiters with structured evidence for candidate evaluation rather than making an autonomous hiring decision.

## Implementation Note

The current ResumeIQ implementation uses deterministic skill extraction, skill normalization, predefined semantic skill relationships, and weighted scoring.

It should therefore be described as an **AI-assisted, explainable resume screening system**, rather than as a separately trained machine-learning model.

## Roadmap

* Export shortlist reports
* Recruiter authentication
* Candidate screening history
* Configurable scoring templates
* Additional job-role categories
* Advanced NLP integration
* ATS integration
* Recruiter analytics

---

**ResumeIQ – AI-Assisted Resume Screening & Candidate Ranking System**
