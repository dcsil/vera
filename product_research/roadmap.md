# Roadmap
We will manage our roadmap using **GitHub Projects**, with **Milestones** to define broader deadlines and **Issues** to keep track of individual tasks. Each item below will be represented as GitHub Issues grouped into Milestones.

Here, we discuss our timeline with respect to our **tech stack**, including our **infrastructure**, **developer environments**, **test environments**, and **user research**.

## Short-Term — MVP Foundations
**Key Milestone**: Core Infrastructure Setup & MVP Skeleton   
**Date Goal**: Approx. Weeks 1-6; Q4 2025 

### Infrastructure & Developer Environment
- Set up the GitHub repo and establish a branching and commit strategy.
- Define `.gitignore` and any linting rules
- Initialize frontend with [what are we using?]
- Initialize backend service with [ … ]
- Set up a lightweight database (SQLite/Postgres) for our MVP
- Create environment files for secrets management.
  
### Testing
- Unit test framework setup (which framework for frontend? Pytest or Mocha/Chai for backend)
  
### Main Product Features
- M1: Implement the auth page, with login/signup (email, Google OAuth)
- M1: Onboarding questionnaire; create a taste profile object saved with Firestore and processed by a unique LangGraph agent
- M2: Basic recommendation list rendering (with mock restaurant data to begin) as a LangGraph agent query, including basic restaurant metadata (ratings, photos, menus)
  
### User Research
- Validate onboarding questions and recommendation rationale clarity
- Clearly define the filtering and recommendation UX with Flutterflow and Figma
- Draft and conduct 5-8 user interviews with target personas
- Main Deliverables
- Mostly-working MVP skeleton: user can sign up, complete onboarding, and see mock recommendations


## Medium-Term — MVP Completion & Pilot Testing
**Key Milestone**: MVP Feature Completion & User Testing   
**Date Goal**: Approx. 2–6 Months; Q1 2026

### Infrastructure
- Migrate from SQLite to Postgres (Heroku or AWS)
- Add Docker containerization for easier dev/test deployment
- Deploy a staging server (Heroku/AWS and EC2/Netlify)

### Testing
- Expand unit tests to cover onboarding, recommendation engine, and filters
- Add integration tests for recommendation ranking
- Begin tracking performance benchmarks (e.g., rec loading time under 2s)

### Main and Secondary Product Features
- M2: Connect recommendations to live datasets (e.g., Google Places API / Yelp API)
- M2: Add template-based rationale text generation for each recommendation
- M3: Implement client-side distance and filter controls (stored in a local database)
- S1: Implement group creation, invite link, and group rec aggregation
- S3: Implement restaurant search by name/keyword
- S2: Prototype calendar integration

### User Research
- Pilot testing with 10-15 users; collect feedback on our rationale clarity and group usability; potentially A/B testing on UX design
- Refine feature priorities based on feedback

### Main Deliverables
- Functional MVP covering all 3 main CUJs and at least 2 secondary CUJs


## Long-Term — Expansion & Launch Prep
**Key Milestone**: Launch-Ready Product & Scale   
**Date Goal**: Approx. 6+ Months; Q3 2026

### Infrastructure
- Deploy production-grade backend (AWS Lambda)
- Implement monitoring/logging (Datadog)
- Add analytics pipeline (event logs for rec usage, filter adjustments, group creation)

### Testing
- Load testing for 100 or more concurrent users
- Automated regression tests for rec engine updates

### Product Features
- Enhance recommendation engine (collaborative filtering, contextual recs)
- Improve group functionality (real-time votes and conflict resolution)
- Full calendar integration (Google Calendar API, Outlook Calendar API, etc.)

### User Research & Marketing
- Conduct beta launch with 50-100 users from our campus/community
- Collect retention + engagement metrics
- Refine features for a v2.0 based on feedback
- Low-Fidelity Launch Plan
- Soft Launch: campus-wide pilot within 9-12 months
- Public Launch: app store/web rollout within 3-4 months after soft launch

### Main Deliverables
- Production-ready app with stable infrastructure, full CUJ support, and a real user base

