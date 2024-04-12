## Postmortem: Login Service Outage on 2024-04-11

**Issue Summary:**

This document details a login service outage that occurred on Friday, April 11th, 2024, between 10:15 AM and 12:45 PM. The outage impacted all user login functionality across our website and mobile app. Users attempting to log in during this window experienced error messages and were unable to access their accounts.  The outage lasted for approximately 2 hours and 15 minutes.

**Timeline:**

* **10:15 AM:** User login attempts started failing across the platform. Monitoring systems alerted engineers to a significant increase in login error rates.
* **10:30 AM:** On-call engineers investigated the issue and identified an error within the login service code. Initial assumptions pointed towards a bug triggered by a recent code deployment.
* **11:00 AM:** The engineering team rolled back the recent code deployment, suspecting it caused the login service malfunction. 
* **11:30 AM:** Rolling back the deployment did not resolve the issue. Further investigation revealed the root cause was a database connection issue impacting the login service.
* **11:45 AM:** The incident was escalated to the database operations team to investigate the connection problem.
* **12:15 PM:** The database operations team identified a failing disk drive on the database server hosting user login credentials. 
* **12:30 PM:** The failing disk was replaced, and the login service was restarted with a healthy database connection.
* **12:45 PM:** Login functionality resumed normal operation. User login attempts were successful, and access to accounts was restored.

**Root Cause and Resolution:**

The root cause of the outage was a failing disk drive on the database server responsible for storing user login credentials. This hardware failure disrupted the connection between the login service and the database, preventing successful login attempts. The database operations team replaced the failing disk and restarted the login service, restoring normal functionality.

**Corrective and Preventative Measures:**

*  **Database Redundancy:** Implement a redundant database server configuration to ensure login functionality remains operational even if one server experiences hardware failure.
* **Disk Drive Monitoring:** Enhance monitoring of database server disk health to detect and proactively address potential drive failures before they cause outages.
* **Disaster Recovery Plan:** Review and update the disaster recovery plan for the login service to ensure a faster response and resolution time in case of future outages.
* **Login Service Testing:** Integrate automated login functionality testing into the development and deployment process to identify potential issues before they impact production.


This postmortem outlines the cause of the login service outage and the steps being taken to prevent similar incidents from occurring in the future. The engineering team and database operations team will collaborate to implement the corrective and preventative measures outlined above. 
