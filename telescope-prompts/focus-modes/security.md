# Focus Mode: Security

## Description
Comprehensive security analysis focusing on vulnerability identification, authentication and authorization mechanisms, data protection, secure coding practices, and compliance with security standards.

## Active Agents
- Security Agent (primary)
- Code Quality Agent
- Database Agent
- Architecture Agent

## Core Focus Areas

### 1. Authentication & Identity Management
**Priority: CRITICAL**

Analyze authentication mechanisms and identity verification:
- Authentication methods (passwords, tokens, OAuth, etc.)
- Session management
- Multi-factor authentication
- Password storage and hashing
- Identity verification processes

**Key Patterns to Identify:**
- Weak password policies
- Insecure session handling
- Missing MFA implementation
- Plaintext password storage
- Session fixation vulnerabilities

**Questions to Answer:**
- How are users authenticated?
- Are passwords properly hashed (bcrypt, Argon2)?
- Are sessions securely managed?
- Is MFA available for sensitive operations?
- Are authentication tokens properly validated?

### 2. Authorization & Access Control
**Priority: CRITICAL**

Evaluate authorization mechanisms and permission systems:
- Role-based access control (RBAC)
- Permission checking mechanisms
- Resource ownership validation
- Principle of least privilege
- Access control enforcement points

**Key Patterns to Identify:**
- Missing authorization checks
- Insecure direct object references (IDOR)
- Privilege escalation vulnerabilities
- Horizontal/vertical access control bypasses
- Authorization logic flaws

**Questions to Answer:**
- Are all protected resources checked for authorization?
- Is the principle of least privilege followed?
- Can users access resources they shouldn't?
- Are permissions checked at every access point?
- Is authorization centralized and consistent?

### 3. Input Validation & Sanitization
**Priority: CRITICAL**

Examine input handling and validation:
- User input validation
- Data sanitization practices
- Type checking and constraints
- Allowlist vs blocklist approaches
- Input normalization

**Key Patterns to Identify:**
- Missing input validation
- SQL injection vulnerabilities
- Command injection risks
- Path traversal vulnerabilities
- Insufficient data validation

**Questions to Answer:**
- Is all user input validated?
- Are validation rules comprehensive?
- Is validation performed server-side?
- Are allowlists used instead of blocklists?
- Is input sanitized before use?

### 4. Injection Prevention
**Priority: CRITICAL**

Identify and prevent injection vulnerabilities:
- SQL injection
- Command injection
- LDAP injection
- XML/JSON injection
- Template injection

**Key Patterns to Identify:**
- Dynamic SQL query construction
- Unsanitized user input in commands
- String concatenation for queries
- Eval() usage with user input
- Unsafe deserialization

**Questions to Answer:**
- Are parameterized queries used consistently?
- Is user input ever executed as code?
- Are ORM frameworks used safely?
- Is input validated before SQL/command execution?
- Are there safe alternatives to dynamic queries?

### 5. Cross-Site Scripting (XSS) Protection
**Priority: HIGH**

Analyze XSS vulnerability prevention:
- Output encoding and escaping
- Content Security Policy (CSP)
- DOM-based XSS risks
- Stored XSS vulnerabilities
- Reflected XSS vulnerabilities

**Key Patterns to Identify:**
- Unescaped user-generated content
- innerHTML usage with user data
- Missing CSP headers
- Unsafe JavaScript generation
- DOM manipulation with untrusted data

**Questions to Answer:**
- Is output properly encoded for context?
- Is CSP implemented and configured?
- Are framework XSS protections used?
- Is user content sanitized before display?
- Are DOM operations safe?

### 6. Cross-Site Request Forgery (CSRF) Protection
**Priority: HIGH**

Evaluate CSRF protection mechanisms:
- CSRF token implementation
- SameSite cookie attributes
- Origin header validation
- State-changing operation protection
- Token validation logic

**Key Patterns to Identify:**
- Missing CSRF tokens
- Incorrect SameSite cookie settings
- GET requests for state changes
- Missing origin validation
- Token validation bypasses

**Questions to Answer:**
- Are CSRF tokens used for state-changing requests?
- Are SameSite cookie attributes set?
- Are GET requests idempotent?
- Is the origin header validated?
- Are CSRF protections framework-provided?

### 7. Data Protection & Encryption
**Priority: CRITICAL**

Examine data protection mechanisms:
- Encryption at rest
- Encryption in transit
- Key management practices
- Sensitive data handling
- Data masking and redaction

**Key Patterns to Identify:**
- Plaintext sensitive data storage
- Weak encryption algorithms
- Hard-coded encryption keys
- Missing TLS/HTTPS
- Insecure key storage

**Questions to Answer:**
- Is sensitive data encrypted at rest?
- Is TLS/HTTPS enforced?
- Are strong encryption algorithms used (AES-256)?
- How are encryption keys managed?
- Is PII properly protected?

### 8. Secrets Management
**Priority: CRITICAL**

Analyze how secrets and credentials are managed:
- API key storage
- Database credential handling
- Secret rotation practices
- Environment variable usage
- Secrets in version control

**Key Patterns to Identify:**
- Hard-coded secrets
- Secrets in source code
- Secrets in configuration files
- Unencrypted secrets storage
- Secrets in logs or error messages

**Questions to Answer:**
- Are secrets stored in secure vaults?
- Are secrets in version control?
- Is secret rotation implemented?
- Are environment variables used properly?
- Are secrets excluded from logs?

### 9. API Security
**Priority: HIGH**

Evaluate API security measures:
- API authentication mechanisms
- Rate limiting implementation
- API key management
- Request/response validation
- API versioning security

**Key Patterns to Identify:**
- Missing API authentication
- No rate limiting
- Overly permissive CORS
- API key exposure
- Excessive data exposure

**Questions to Answer:**
- Are APIs properly authenticated?
- Is rate limiting implemented?
- Is CORS configured securely?
- Are API responses filtered appropriately?
- Are API errors sanitized?

### 10. Security Headers & Configuration
**Priority: MEDIUM**

Examine security-related HTTP headers and configurations:
- Security headers (HSTS, CSP, X-Frame-Options, etc.)
- Cookie security attributes
- TLS configuration
- Server information disclosure
- Error handling and messages

**Key Patterns to Identify:**
- Missing security headers
- Insecure cookie attributes
- Outdated TLS versions
- Information leakage in errors
- Debug mode in production

**Questions to Answer:**
- Are security headers properly configured?
- Are cookies marked as Secure and HttpOnly?
- Is TLS 1.2+ enforced?
- Do errors leak sensitive information?
- Is debug mode disabled in production?

## Analysis Emphasis

### Security Quality Indicators

**GOOD Implementation:**
- Defense in depth strategy
- Principle of least privilege enforced
- All inputs validated and sanitized
- Parameterized queries throughout
- Strong authentication with MFA support
- Comprehensive authorization checks
- Encrypted sensitive data at rest and in transit
- Secrets in secure vault (not code)
- Security headers properly configured
- Regular security audits and updates
- Secure by default configurations
- Detailed security logging and monitoring

**BAD Implementation:**
- Single layer of security
- Overly permissive access controls
- Missing input validation
- String concatenation for SQL queries
- Weak password requirements
- No authorization checks
- Plaintext sensitive data
- Hard-coded secrets and API keys
- Missing security headers
- No security testing
- Debug mode in production
- Sensitive data in logs or error messages

### Specific Concerns

**Authentication:**
- Never store passwords in plaintext
- Use strong hashing (bcrypt, Argon2, scrypt)
- Implement account lockout after failed attempts
- Support MFA for sensitive accounts
- Use secure session management

**Authorization:**
- Check permissions on every protected operation
- Validate resource ownership
- Use centralized authorization logic
- Log authorization failures
- Implement time-based access controls

**Input Validation:**
- Validate all inputs server-side
- Use allowlists, not blocklists
- Validate data type, length, format, range
- Sanitize before use and storage
- Reject invalid input, don't try to fix it

**Injection Prevention:**
- Always use parameterized queries
- Never concatenate user input into queries
- Use ORM frameworks properly
- Validate input before any execution
- Apply principle of least privilege to database users

**Data Protection:**
- Encrypt sensitive data at rest (AES-256)
- Enforce TLS 1.2+ for data in transit
- Use secure key management (KMS, vault)
- Implement proper key rotation
- Redact sensitive data from logs

## Code Review Checklist

When reviewing for security, verify:

1. **Authentication:**
   - [ ] Passwords are properly hashed (bcrypt, Argon2)
   - [ ] MFA is available for sensitive operations
   - [ ] Session tokens are securely generated
   - [ ] Sessions have appropriate timeouts
   - [ ] Password reset flows are secure

2. **Authorization:**
   - [ ] All protected endpoints check permissions
   - [ ] Resource ownership is validated
   - [ ] Least privilege principle is followed
   - [ ] Authorization is centralized
   - [ ] No IDOR vulnerabilities

3. **Input Validation:**
   - [ ] All user inputs are validated
   - [ ] Validation is server-side
   - [ ] Allowlists are used over blocklists
   - [ ] Type checking is enforced
   - [ ] Input length limits are set

4. **Injection Prevention:**
   - [ ] Parameterized queries are used
   - [ ] No string concatenation for SQL
   - [ ] Command execution is avoided or sanitized
   - [ ] ORM is used safely
   - [ ] No eval() with user input

5. **XSS Prevention:**
   - [ ] Output is properly encoded
   - [ ] CSP headers are configured
   - [ ] Framework XSS protections are used
   - [ ] No innerHTML with user data
   - [ ] Template engines auto-escape

6. **CSRF Prevention:**
   - [ ] CSRF tokens are used
   - [ ] SameSite cookies are configured
   - [ ] State changes require POST/PUT/DELETE
   - [ ] Origin headers are validated
   - [ ] Framework CSRF protection is enabled

7. **Data Protection:**
   - [ ] Sensitive data is encrypted at rest
   - [ ] TLS/HTTPS is enforced
   - [ ] Strong encryption algorithms are used
   - [ ] Keys are stored securely
   - [ ] PII is properly handled

8. **Secrets Management:**
   - [ ] No secrets in source code
   - [ ] Secrets are in secure vault
   - [ ] Environment variables are used properly
   - [ ] Secret rotation is implemented
   - [ ] Secrets are excluded from logs

9. **API Security:**
   - [ ] APIs require authentication
   - [ ] Rate limiting is implemented
   - [ ] CORS is configured securely
   - [ ] API responses are filtered
   - [ ] API errors don't leak information

10. **Security Headers:**
    - [ ] HSTS header is set
    - [ ] CSP header is configured
    - [ ] X-Frame-Options is set
    - [ ] X-Content-Type-Options is set
    - [ ] Cookies are Secure and HttpOnly

## Common Vulnerabilities (OWASP Top 10)

1. **Broken Access Control**
   - IDOR vulnerabilities
   - Missing authorization checks
   - Privilege escalation

2. **Cryptographic Failures**
   - Weak encryption
   - Plaintext sensitive data
   - Poor key management

3. **Injection**
   - SQL injection
   - Command injection
   - LDAP injection

4. **Insecure Design**
   - Lack of security controls
   - Weak architecture
   - Missing threat modeling

5. **Security Misconfiguration**
   - Default credentials
   - Unnecessary features enabled
   - Missing security headers

6. **Vulnerable and Outdated Components**
   - Unpatched dependencies
   - EOL software versions
   - Known vulnerabilities

7. **Identification and Authentication Failures**
   - Weak password policies
   - Session management issues
   - Missing MFA

8. **Software and Data Integrity Failures**
   - Unsigned code
   - Insecure deserialization
   - Unverified updates

9. **Security Logging and Monitoring Failures**
   - Insufficient logging
   - No alerting
   - Missing audit trails

10. **Server-Side Request Forgery (SSRF)**
    - Unvalidated URLs
    - Internal service access
    - Cloud metadata exposure

## Security Testing

**Testing Approaches:**
- Static Application Security Testing (SAST)
- Dynamic Application Security Testing (DAST)
- Dependency vulnerability scanning
- Penetration testing
- Security code review

**Tools to Consider:**
- OWASP ZAP for web security testing
- SonarQube for code analysis
- Snyk or Dependabot for dependency scanning
- Burp Suite for penetration testing
- GitGuardian for secrets detection

## Compliance Considerations

**Standards & Frameworks:**
- OWASP Top 10
- CWE Top 25
- PCI DSS (payment data)
- HIPAA (healthcare data)
- GDPR (EU privacy)
- SOC 2 (service organization controls)

## Documentation Requirements

Security documentation should include:
- Threat model documentation
- Authentication and authorization flows
- Data classification and protection measures
- Incident response procedures
- Security testing results
- Dependency vulnerability reports
- Security header configurations
- Encryption key management procedures
- Access control matrix
- Security audit logs and reviews
