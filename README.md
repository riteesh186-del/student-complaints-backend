# Student Complaints Portal: Backend

Spring Boot 3 (Java 17) REST API with Spring Data JPA and MySQL.

## Links
- Frontend repository: https://github.com/riteesh186-del/student-complaints-frontend
- Live website: https://student-complaints-frontend.onrender.com
- Live API: https://student-complaints-portal.onrender.com/api/complaints (the free host sleeps when idle, so the first request can take up to a minute)

## Endpoints
| Method | Path | Access |
|---|---|---|
| POST | `/api/complaints` | Public (rate limited) |
| GET | `/api/complaints/track?ids=1,2` | Public |
| GET | `/api/complaints/lookup?id=&email=` | Public (rate limited) |
| GET | `/api/complaints` | Admin |
| PATCH | `/api/complaints/{id}/status` | Admin |
| PATCH | `/api/complaints/{id}/response` | Admin |
| DELETE | `/api/complaints/{id}` | Admin |

Admin requests send the password in an `X-Admin-Password` header.

## Configuration (environment variables)
| Variable | Purpose | Default |
|---|---|---|
| `MYSQLHOST`, `MYSQLPORT`, `MYSQLUSER`, `MYSQLPASSWORD`, `MYSQLDATABASE` | Database connection | `localhost`, `3306`, `root`, `root`, `student_complaints` |
| `MYSQL_SSL_MODE` | MySQL SSL mode | `PREFERRED` |
| `ADMIN_PASSWORD` | Admin password (admin endpoints are disabled while empty) | empty |
| `CORS_ALLOWED_ORIGINS` | Frontend origin(s), comma separated | `http://localhost:5173` |
| `PORT` | Server port | `8080` |

## Run locally
Requires JDK 17+, Maven 3.9+ and MySQL 8+.

```powershell
$env:ADMIN_PASSWORD = "choose-a-password"
mvn spring-boot:run
```

Tables are created automatically (`spring.jpa.hibernate.ddl-auto=update`).

## Docker
```bash
docker build -t complaints-backend .
docker run -p 8080:8080 -e ADMIN_PASSWORD=choose-a-password complaints-backend
```

## Deployment
Deployed on Render as a Docker web service, with MySQL on Aiven.
