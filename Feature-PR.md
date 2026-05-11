## feat(auth): implement JWT-based authentication with secure login flow

This PR introduces a complete authentication system for the DAICA backend using JWT. It enables secure user login, token generation, and protected route access across the API.

---

## What was added and why

### Authentication Core
- `POST /auth/login` endpoint — validates user credentials and issues JWT tokens
- JWT token generation — signs secure tokens for authenticated sessions
- Token verification middleware — protects private routes by validating incoming JWTs

### Security Enhancements
- Password hashing using `bcrypt` — ensures passwords are never stored or compared in plain text
- Authorization header parsing — extracts and validates Bearer tokens from requests
- Invalid token handling — returns standardized `401 Unauthorized` responses for expired or malformed tokens

### Middleware Layer
- `authMiddleware` — guards protected routes and injects authenticated user context into requests
- Future-ready structure for role-based access control (RBAC)

---

## Notes for Reviewers

- No refresh token system implemented yet — currently using short-lived JWTs only
- User roles are not enforced yet, but the architecture supports RBAC expansion
- Consider adding rate limiting on `/auth/login` to prevent brute-force attacks

---

## Checklist

- [x] Login endpoint implemented (`POST /auth/login`)
- [x] JWT token generation working
- [x] Authentication middleware added
- [x] Passwords securely hashed with bcrypt
- [x] Protected route access verified
- [x] No secrets or sensitive data exposed

---

## Branch Information

- **Branch:** `feat/auth-jwt-login` → `dev`
- **Type:** `feat`
- **Breaking changes:** None