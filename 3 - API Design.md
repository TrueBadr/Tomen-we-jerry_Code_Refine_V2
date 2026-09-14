# API Design
1. Register
POST Carieeer/register
Request
{
  "name": "Badr",
  "email": "badr@gmail.com",
  "password": "12345678",
  "role": "candidate"
}
Response
{
  "id": "123",
  "name": "Badr",
  "email": "badr@gmail.com",
  "role": "candidate"
}

2. Login
POST Carieeer/login
Request
{
  "email": "badr@gmail.com",
  "password": "12345678"
}
Response
{
  "id": "123",
  "name": "Badr",
  "email": "badr@gmail.com",
  "role": "candidate"
}

3. Get Candidate Profile
GET Carieeer/candidates/:id
Response
{
  "id": "123",
  "user_id": "123",
  "bio": "Backend Developer",
  "experience_years": 2,
  "location": "Cairo",
  "career_goal": "Backend Engineer"
}

4. Update Candidate Profile
PUT Carieeer/candidates/:id
Request
{
  "bio": "Backend Developer",
  "experience_years": 2,
  "location": "Cairo",
  "career_goal": "Backend Engineer"
}
Response
{
  "id": "123",
  "user_id": "123",
  "bio": "Backend Developer",
  "experience_years": 2,
  "location": "Cairo",
  "career_goal": "Backend Engineer"
}

5. Add Experience
POST Carieeer/candidates/:id/experiences
Request
{
  "company": "ABC",
  "job_title": "Backend Developer",
  "start_date": "2024-01-01",
  "end_date": "2025-01-01",
  "description": "Built backend APIs"
}
Response
{
  "id": "exp1",
  "candidate_id": "123",
  "company": "ABC",
  "job_title": "Backend Developer",
  "start_date": "2024-01-01",
  "end_date": "2025-01-01",
  "description": "Built backend APIs"
}

6. Add Education
POST Carieeer/candidates/:id/education
Request
{
  "institution": "Zagazig University",
  "degree": "Computer Science",
  "field_of_study": "CS",
  "start_date": "2023-09-01",
  "end_date": "2027-06-01"
}
Response
{
  "id": "edu1",
  "candidate_id": "123",
  "institution": "Zagazig University",
  "degree": "Computer Science",
  "field_of_study": "CS",
  "start_date": "2023-09-01",
  "end_date": "2027-06-01"
}

7. Add Portfolio Item
POST Carieeer/candidates/:id/portfolio
Request
{
  "title": "E-Commerce API",
  "description": "Backend API using Node.js",
  "url": "https://github.com/badr/project"
}
Response
{
  "id": "p1",
  "candidate_id": "123",
  "title": "E-Commerce API",
  "description": "Backend API using Node.js",
  "url": "https://github.com/badr/project"
}

8. Add Skill
POST Carieeer/candidates/:id/skills
Request
{
  "skill_id": "s1"
}
Response
{
  "id": "s1",
  "name": "Node.js"
}

9. Get Employer Profile
GET Carieeer/employers/:id
Response
{
  "id": "ep1",
  "user_id": "u1",
  "company_id": "c1",
  "position": "HR Manager",
  "bio": "HR Manager",
  "experience_years": 5,
  "location": "Cairo",
  "career_goal": "Talent Acquisition"
}

10. Create Company
POST Carieeer/companies
Request
{
  "name": "Tech Corp",
  "description": "Software Company",
  "website": "https://techcorp.com",
  "linkedin": "https://linkedin.com/company/techcorp",
  "industry": "Software",
  "location": "Cairo"
}
Response
{
  "id": "c1",
  "name": "Tech Corp",
  "description": "Software Company",
  "website": "https://techcorp.com",
  "linkedin": "https://linkedin.com/company/techcorp",
  "industry": "Software",
  "location": "Cairo"
}

11. Create Job
POST Carieeer/jobs
Request
{
  "company_id": "c1",
  "title": "Backend Developer",
  "description": "Build backend services",
  "min_salary": 15000,
  "max_salary": 25000,
  "location": "Cairo",
  "employment_type": "Full-time",
  "experience_level": "Mid"
}
Response
{
  "id": "j1",
  "company_id": "c1",
  "title": "Backend Developer",
  "description": "Build backend services",
  "min_salary": 15000,
  "max_salary": 25000,
  "location": "Cairo",
  "employment_type": "Full-time",
  "experience_level": "Mid",
  "status": "open"
}

12. Search Jobs
GET Carieeer/jobs?keyword=backend&location=Cairo&min_salary=10000&max_salary=30000
Response
[
  {
    "id": "j1",
    "company_id": "c1",
    "title": "Backend Developer",
    "min_salary": 15000,
    "max_salary": 25000,
    "location": "Cairo",
    "employment_type": "Full-time",
    "experience_level": "Mid",
    "status": "open"
  }
]

13. Search Candidates
GET Carieeer/candidates?experience_years=2&location=Cairo
Response
[
  {
    "id": "123",
    "name": "Badr",
    "experience_years": 2,
    "location": "Cairo"
  }
]

14. Get Recommended Jobs
GET Carieeer/candidates/:id/recommended-jobs
Response
[
  {
    "job_id": "j1",
    "match_score": 92
  },
  {
    "job_id": "j2",
    "match_score": 85
  }
]

15. Get Recommended Candidates
GET Carieeer/jobs/:id/recommended-candidates
Response
[
  {
    "candidate_id": "123",
    "match_score": 92
  },
  {
    "candidate_id": "124",
    "match_score": 87
  }
]

16. Apply to Job
POST Carieeer/jobs/:id/applications
Request
{
  "candidate_id": "123",
  "cv": "cv_url"
}
Response
{
  "id": "app1",
  "job_id": "j1",
  "candidate_id": "123",
  "status": "applied",
  "cv": "cv_url"
}

17. Get Applications for Candidate
GET Carieeer/candidates/:id/applications
Response
[
  {
    "id": "app1",
    "job_id": "j1",
    "candidate_id": "123",
    "status": "interview",
    "cv": "cv_url",
    "applied_at": "2026-09-14"
  }
]

18. Get Applications for Job
GET Carieeer/jobs/:id/applications
Response
[
  {
    "id": "app1",
    "job_id": "j1",
    "candidate_id": "123",
    "status": "screened",
    "cv": "cv_url"
  }
]

19. Update Application Status
PUT Carieeer/applications/:id/status
Request
{
  "status": "interview"
}
Response
{
  "id": "app1",
  "job_id": "j1",
  "candidate_id": "123",
  "status": "interview"
}

20. Skill Gap Analysis
GET Carieeer/jobs/:id/skill-gap/:candidate_id
Response
{
  "matched_skills": [
    "Node.js",
    "PostgreSQL"
  ],
  "missing_skills": [
    "Docker",
    "Redis"
  ]
}
