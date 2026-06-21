# API Security Risk Analysis

## Overview
This project documents an API security risk analysis performed on public demo APIs using Postman. The assessment identifies common API security weaknesses, maps them to the OWASP API Security Top 10 (2023), and provides practical remediation recommendations.

All testing was passive and non-intrusive. No production systems were targeted and no exploitation was performed.

## Project Objective
- Identify security risks in API endpoints
- Review authentication, response headers, token handling, and rate limiting
- Map findings to the OWASP API Security Top 10 (2023)
- Assess the overall security risk
- Recommend mitigations for developers and organizations

## Scope

### APIs Tested
- JSONPlaceholder
- ReqRes.in

### Endpoints Tested
- `DELETE /posts/1`
- `POST /api/login`
- `GET /api/users?page=2`

## Tools Used
- Postman v7.39
- Postman Collection Runner
- Browser DevTools

## Key Findings

| ID | Finding | Risk | OWASP API Security Top 10 (2023) |
|---|---|---|---|
| F-01 | No authentication on DELETE endpoint | High | Broken Object Level Authorization |
| F-02 | Authentication token exposed in response body | Medium | Broken Authentication |
| F-03 | Missing critical security headers | Medium | Security Misconfiguration |
| F-04 | No rate limiting on API endpoints | Medium | Unrestricted Resource Consumption |

## Security Indicators Observed
- An unauthenticated `DELETE /posts/1` request returned `200 OK`
- Login endpoint returned a token in the JSON response body without expiry information
- Security headers such as HSTS, CSP, `X-Frame-Options`, and `X-Content-Type-Options` were absent
- 100 consecutive requests completed without throttling or rate-limit responses
- The `x-powered-by: Express` header disclosed backend technology information

## Risk Classification
**High â Broken Access Control**

The overall API security posture was classified as high risk. The unauthenticated DELETE endpoint presents a serious access-control issue, and the additional findings increase exposure to unauthorized actions, session risks, brute-force attempts, and security misconfiguration.

## Recommendations

### For API Developers
- Enforce JWT or OAuth 2.0 authentication on write endpoints.
- Return `401 Unauthorized` for unauthenticated requests.
- Implement rate limiting and return `429 Too Many Requests` when limits are exceeded.
- Configure security headers using Helmet.js or an equivalent solution.
- Use short-lived tokens and transmit them only over HTTPS.
- Remove technology-disclosure headers such as `x-powered-by`.

### For Organizations
- Perform regular API security reviews and automated testing in CI/CD.
- Maintain an API inventory with authentication requirements.
- Use an API gateway for centralized authentication, rate limiting, and logging.
- Map endpoints to the OWASP API Security Top 10 during design and review.
- Conduct secure API development awareness training.

## Conclusion
The analysis identified four API security risks related to authentication, token handling, response security headers, and rate limiting. These findings align with common OWASP API Security Top 10 risks. Implementing the recommended controls can reduce the attack surface and strengthen API security.

## Author
**Urvi Nandasana**  
Cyber Security Intern @Future Interns

## Project Report
The complete assessment report is available in this repository:

`Task-3_API_Security_Risk_Analysis_Urvi_Nandasana.pdf`