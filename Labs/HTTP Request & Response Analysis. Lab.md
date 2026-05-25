## Practical Findings

Target:

uniten.edu.my

Request Method:

GET

Path:

/

Response Status:

200 OK

Server:

Microsoft-IIS/10.0

Technology:

ASP.NET

Content Type:

text/html

The server successfully responded with an HTML page and disclosed the web server and backend technology in HTTP headers.

<img width="1892" height="1007" alt="Screenshot 2026-05-26 043042" src="https://github.com/user-attachments/assets/6c5f2e4c-ead1-405a-a165-d32e80308992" />

POST request=
## Findings

Captured an HTTP POST request used for authentication.

Request Path:

/login

Parameters Identified:

- username
- password

Content Type:

application/x-www-form-urlencoded

The submitted credentials were transmitted within the HTTP request body.

<img width="1904" height="1016" alt="image" src="https://github.com/user-attachments/assets/41d410ce-a79a-4e3d-adde-36378ac95f1d" />
## Lessons Learned

- POST requests are used to submit user data to web applications.
- Form fields are commonly transmitted in the request body.
- HTTP requests contain headers, cookies, and body parameters.
- Burp Suite can intercept and inspect submitted form data.
- Authentication workflows typically rely on POST requests.

