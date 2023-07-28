# Job Openings Scraper & API

This project is a web scraper built with Spring Boot that collects job openings related to interns, internships, university graduates, and new grads from various career sites. It provides two APIs—one to run the scraper and store job data in a local PostgreSQL database and another to retrieve job data based on filters.

## Prerequisites

- Java 11 or higher installed.
- PostgreSQL database set up.

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/job-openings-scraper.git
   cd job-openings-scraper
   ```

2. Configure the database:

   - Create a PostgreSQL database and note down the connection details (URL, username, and password).

   - Update the database configuration in `src/main/resources/application.properties`:

     ```
     spring.datasource.url=jdbc:postgresql://your-database-url
     spring.datasource.username=your-database-username
     spring.datasource.password=your-database-password
     ```

3. Build and run the application:

   ```bash
   ./mvnw spring-boot:run
   ```

   The application will start on `http://localhost:8080`.

## Endpoints

### 1. Start the Scraper

- **Endpoint**: POST /api/scrape
- **Description**: Trigger the web scraper to collect job data from various career sites. You can specify a site name as a filter (e.g., lever, tesla) or leave it empty to scrape all sites.
- **Request Body** (JSON):
  ```json
  {
    "siteName": "lever"
  }
  ```
- **Response**: 200 OK

### 2. Retrieve Job Data

- **Endpoint**: GET /api/jobs
- **Description**: Retrieve job data from the local database based on company name and job type filters. The response will contain a JSON array with a maximum of 10 results.
- **Parameters** (Query String):
  - `companyName` (optional): Filter jobs by company name.
  - `jobType` (optional): Filter jobs by job type (e.g., intern, full-time).
- **Response** (JSON):
  ```json
  [
    {
      "id": 1,
      "title": "Software Engineer Intern",
      "location": "San Francisco, CA",
      "link": "https://example.com/job/12345",
      "type": "Intern",
      "company": "Example Inc."
    },
    {
      "id": 2,
      "title": "Junior Data Analyst",
      "location": "New York, NY",
      "link": "https://example.com/job/67890",
      "type": "Full-time",
      "company": "Another Company"
    },
    ...
  ]
  ```

## Data Model

The job data is stored in the `jobs` table with the following columns:

- `id`: Unique identifier for each job entry.
- `title`: Job title.
- `location`: Job location.
- `link`: URL to the job description page.
- `type`: Job type (e.g., intern, full-time).
- `company`: Company name.

## Notes

- The scraper is designed to avoid storing duplicate job entries in the database based on the job title and company name.
- Please ensure that you use the APIs responsibly and respect the terms of service of the career sites you are scraping.
- For security reasons, consider using authentication and authorization mechanisms if deploying the application in a production environment.

## Contributors

- [Deepak Choudhary](https://github.com/Deepak-Choudhary0/)

## License

This project is licensed under the [MIT License](LICENSE).

Feel free to add any additional information or sections to the README to suit your project's specific needs. This README provides a basic outline to get you started.
