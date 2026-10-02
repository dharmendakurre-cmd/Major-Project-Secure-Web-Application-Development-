# Major-Project-Secure-Web-Application-Development-
(Authentication, Session Management &amp; Defense Architecture) 
Project Overview & Objectives
The primary objective of this project is to construct a secure web application featuring a user registration and login interface engineered to resist common web application security risks. The project enforces: 
•	Input Validation & Sanitization: Enforcing strict regex validation to neutralize unauthorized payloads at the boundary. 
o	
o	Cryptographic Storage: Mitigating credential exposure by hashing passwords using industry-standard key derivation (scrypt/pbkdf2 via Werkzeug) rather than plain-text storage.

o	SQL Injection (SQLi) Defense: Implementing parameterized database queries with SQLite3 to separate SQL code from user inputs. 

o	Cross-Site Scripting (XSS) Prevention: Output escaping powered by Jinja2 templating. 

•	Session Management: Secure server-side session allocation and clean session invalidation upon logout. 

Implementation & Verification Proofs
Task 1: Environment & Dependency Provisioning
•	Commands Executed: sudo apt install python3-flask python3-werkzeug sqlite3 -y
•	Purpose: Sets up the essential Python web framework, security libraries, and relational database engine.

 






Task 2: Application Structure & Template Hierarchy
•	Files Created: app.py, templates/register.html, templates/login.html, templates/dashboard.html
•	Purpose: Separates backend routing logic from the frontend presentation layer

 
Task 3: Local Server Deployment
•	Command Executed: python3 app.py
•	Purpose: Verifies that the Flask microservice is bound locally to port 5000 and listening for HTTP connections.


 

Task 4: Boundary Input Validation Defense
•	Mechanism: Regex enforcement (^[a-zA-Z0-9_]{3,20}$) applied to the username field.
•	Observation: When non-alphanumeric or unauthorized characters are entered, the system rejects the request immediately, displaying a validation alert without modifying the database state.
 



Task 5: Password Cryptographic Hashing Verification
•	Command Executed: sqlite3 database.db "SELECT id, username, email, password FROM users;"
•	Observation: User password is stored strictly as a complex salted hash (scrypt:32768:8:1$...). The database at rest never exposes plaintext credentials.


 



Task 6: Secure Authentication & Session Handling
•	Mechanism: Matching stored credentials via check_password_hash() and creating a transient user session.
•	Observation: The dashboard confirms active authenticated state and provides an explicit logout hook to clear session cookies.



 

Task 7: SQL Injection (SQLi) Attack Mitigation
•	Attack Payload Injected: ' OR '1'='1 in the login username field.
•	Defense Mechanism: SQLite parameterized statement (SELECT ... WHERE username = ?).
•	Observation: The database engine treats the injected payload as an immutable literal value rather than executable SQL syntax. Authentication fails safely, confirming zero authorization bypass.




 

4. Conclusion
5. All operational requirements set forth in the project brief—including secure sign-up, authenticated login, input boundary checks, session clearance, and protection against SQL injection and XSS—were successfully built, tested, and validated within Kali Linux.
