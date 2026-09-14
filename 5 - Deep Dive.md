# Deep Dives
### 1. Matching Service

Problem at Scale:
Matching can become very expensive if the system tries to compare every candidate with every job whenever a user opens the app.
- Trade-offs:
	- Async Processing: Matching is done in the background instead of during the user request.
	- Event-Based Updates: When a profile or job changes, an event is sent to the matching service.
	- Background Workers: Workers process these events and calculate the new matches.
	- Result Storage: The ranked matches are saved in Redis or PostgreSQL so they can be returned quickly.
	- Eventual Consistency: A new match may take a short time to appear, but this gives us much better performance and scalability.
---
### 2. Application Service

- Problem at Scale: 
	- Many requests may arrive at the same time, so the system must prevent a candidate from applying to the same job more than once and must keep the application status valid.
- Trade-offs:
	- Database: PostgreSQL is used because applications require strong data consistency.
	- Duplicate Prevention: A unique `(candidate_id, job_id)` rule prevents duplicate applications.
	- Status Validation: The service only allows valid status changes such as `Applied → Screened → Interview → Offer`.
	- Transaction: Application creation and important status updates are handled safely in the database.
	- Events: When the application status changes, an event is sent to the notification service and other services that need the update.
---
### 3. Search Service
- Problem at Scale:  
	- Searching through millions of jobs or candidates using normal database queries can become slow, especially when users search by keywords, skills, salary, and experience together.
- Trade-offs:
	- Search Engine: Elasticsearch is used for fast searching and filtering.
	- Separate Search Data: Jobs and candidates are stored in a search-friendly format, so search requests do not need many database joins.
	- Event-Based Updates: When a job or profile changes, an event updates the search index.
	- Fast Reads: Search requests are handled by Elasticsearch instead of the main PostgreSQL database.
	- Eventual Consistency: There may be a small delay before a new or updated job appears in search, which is acceptable for better performance.

