# API Contracts

This directory contains API specifications and contracts for all services.

## Purpose

API contracts define the interface between services or between frontend and backend. In AI-driven development with parallel workflows, **frozen contracts** are essential to prevent integration conflicts.

## Contract Types

### 1. Internal Service Contracts
Contracts between microservices or internal modules.

**File naming:** `[service-a]-to-[service-b]-contract.md` or `[service-name]-api-contract.md`

### 2. External API Contracts
Contracts for integrations with external systems.

**File naming:** `external-[system-name]-contract.md`

### 3. Sprint Contracts
Contracts frozen for a specific sprint to enable parallel development.

**File naming:** `sprint-[N]-contracts.md`

## Contract Format

Every contract must include:

1. **Metadata** - Version, status, owners
2. **Endpoints** - All API endpoints with methods
3. **Request Schema** - JSON schema or example
4. **Response Schema** - Success and error responses
5. **Status Codes** - All possible HTTP status codes
6. **Authentication** - Auth requirements
7. **Rate Limits** - If applicable
8. **Examples** - Real request/response examples
9. **Constraints for AI** - Rules for AI agents

## Contract Template

```markdown
# API Contract: [Service/Feature Name]

**Version:** 1.0  
**Status:** [Draft / Frozen / Active / Deprecated]  
**Last Updated:** YYYY-MM-DD  
**Owners:** [Backend Team], [Frontend Team]  

---

## Overview

[Brief description of what this API provides]

---

## Base URL

- **Development:** https://dev-api.example.com/v1
- **Staging:** https://staging-api.example.com/v1
- **Production:** https://api.example.com/v1

---

## Authentication

**Type:** [Bearer Token / API Key / OAuth2 / etc.]

**Header:**
```
Authorization: Bearer {token}
```

**Token Lifetime:** [duration]

---

## Endpoints

### 1. [Endpoint Name]

**Method:** GET | POST | PUT | PATCH | DELETE  
**Path:** `/api/v1/resource/{id}`  
**Description:** [What this endpoint does]

#### Request

**Path Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id | UUID | Yes | Resource identifier |

**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| page | integer | No | 1 | Page number |
| limit | integer | No | 50 | Items per page |

**Headers:**
| Header | Required | Description |
|--------|----------|-------------|
| Authorization | Yes | Bearer token |
| Content-Type | Yes | application/json |

**Body Schema:**
```json
{
  "field1": "string",
  "field2": 123,
  "nested": {
    "subfield": "value"
  }
}
```

**Validation Rules:**
- field1: Required, 2-100 characters
- field2: Required, positive integer
- nested.subfield: Optional, enum [value1, value2, value3]

#### Response

**Success Response (200 OK):**
```json
{
  "id": "uuid",
  "field1": "string",
  "field2": 123,
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

**Error Responses:**

**400 Bad Request - Validation Error:**
```json
{
  "code": "VALIDATION_ERROR",
  "message": "Request validation failed",
  "errors": [
    {
      "field": "field1",
      "code": "REQUIRED",
      "message": "field1 is required"
    }
  ]
}
```

**401 Unauthorized:**
```json
{
  "code": "UNAUTHORIZED",
  "message": "Authentication required"
}
```

**403 Forbidden:**
```json
{
  "code": "FORBIDDEN",
  "message": "Insufficient permissions"
}
```

**404 Not Found:**
```json
{
  "code": "NOT_FOUND",
  "message": "Resource not found"
}
```

**409 Conflict:**
```json
{
  "code": "CONFLICT",
  "message": "Resource already exists",
  "field": "email"
}
```

**500 Internal Server Error:**
```json
{
  "code": "INTERNAL_ERROR",
  "message": "An unexpected error occurred",
  "requestId": "uuid"
}
```

#### Status Codes

| Code | Meaning | When Used |
|------|---------|-----------|
| 200 | Success | Request succeeded with response body |
| 201 | Created | Resource successfully created |
| 204 | No Content | Success with no response body (DELETE) |
| 400 | Bad Request | Validation error or malformed request |
| 401 | Unauthorized | Missing or invalid authentication |
| 403 | Forbidden | Authenticated but not authorized |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Duplicate or conflicting resource |
| 500 | Server Error | Unexpected server-side error |

---

## Rate Limits

- **Authenticated:** 1000 requests per hour per user
- **Unauthenticated:** 100 requests per hour per IP
- **Header Response:** `X-RateLimit-Remaining`, `X-RateLimit-Reset`

---

## Pagination

For list endpoints:

**Request:**
```
GET /api/v1/resources?page=2&limit=25
```

**Response:**
```json
{
  "data": [...],
  "pagination": {
    "page": 2,
    "limit": 25,
    "total": 150,
    "totalPages": 6,
    "hasNext": true,
    "hasPrev": true
  }
}
```

---

## Constraints for AI

[Critical section for AI agents implementing this API]

### Backend Implementation Rules
- ALWAYS validate all input fields before processing
- NEVER expose internal error messages to API responses
- WHEN handling validation errors THEN return 400 with field-level error details
- ALL endpoints MUST check authentication (except explicitly public ones)
- ALWAYS use [validation library name] for input validation
- ALL database queries MUST use parameterized queries
- WHEN resource not found THEN return 404 with code "NOT_FOUND"
- ALL timestamps MUST be in ISO 8601 format with UTC timezone

### Frontend Implementation Rules
- ALWAYS include Authorization header for protected endpoints
- WHEN receiving 401 THEN redirect to login page
- WHEN receiving 403 THEN show "Insufficient permissions" message
- ALL API calls MUST have error handling for network failures
- ALWAYS display field-level validation errors to users
- WHEN pagination available THEN implement infinite scroll or pagination UI

---

## Examples

### Example 1: Create Resource

**Request:**
```bash
curl -X POST https://api.example.com/v1/resources \
  -H "Authorization: Bearer eyJhbGc..." \
  -H "Content-Type: application/json" \
  -d '{
    "field1": "example value",
    "field2": 42
  }'
```

**Response:**
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "field1": "example value",
  "field2": 42,
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

---

## Change Log

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | YYYY-MM-DD | [Name] | Initial contract |

---

## Contract Status

- **Draft:** Contract is being designed, subject to change
- **Frozen:** Contract is locked for current sprint, no changes allowed
- **Active:** Contract is implemented and in use
- **Deprecated:** Contract is being phased out, see migration guide

---

## Related Documents

- ADR: [Link to relevant ADR]
- User Story: [Link to story that requires this API]
- Sprint Context: [Link to sprint-context.md]
```

## Contract Freeze Protocol

### When to Freeze a Contract

Freeze contracts when:
1. ✅ Parallel development starts (backend + frontend)
2. ✅ Multiple teams depend on the same API
3. ✅ Sprint planning locks in the interface

### Contract Freeze Rules

When a contract is marked **Status: Frozen**:
- ❌ **NO changes** to endpoint paths
- ❌ **NO changes** to request/response schema
- ❌ **NO changes** to status codes
- ✅ **MAY add** optional fields (backward compatible)
- ✅ **MAY add** documentation clarifications

### Unfreezing a Contract

To change a frozen contract:
1. **Escalate to Tech Lead** immediately
2. **Impact assessment** on all dependent work
3. **Team synchronization** meeting
4. **Version bump** if breaking change
5. **All teams re-sync** before proceeding

## Usage in AI-Driven Development

### For Architects
- Define contract structure standards
- Review and approve all API contracts
- Ensure security and compliance requirements are met

### For Tech Leads
- Create API contracts BEFORE sprint starts
- Freeze contracts before parallel development begins
- Enforce freeze protocol strictly
- Use contracts in user story "Technical Context" section

### For Developers (Backend)
- Implement exactly as specified in contract
- Do NOT add fields not in contract without Tech Lead approval
- Use contract's "Constraints for AI" section for implementation rules
- Run contract validation tests before PR submission

### For Developers (Frontend)
- Code against the contract, not the implementation
- Use mocks based on contract for local development
- Handle ALL status codes specified in contract
- Do NOT assume fields exist that aren't in the contract

## Testing Contracts

### Contract Testing Tools
- **Pact:** Consumer-driven contract testing
- **Postman:** API testing and documentation
- **Swagger/OpenAPI Validator:** Schema validation
- **JSON Schema Validator:** Request/response validation

### Test Checklist
- [ ] All endpoints return documented status codes
- [ ] Response schemas match specification exactly
- [ ] Validation rules enforce documented constraints
- [ ] Error responses follow documented format
- [ ] Authentication requirements are enforced
- [ ] Rate limiting works as specified

## OpenAPI/Swagger Generation

To generate OpenAPI spec from this contract:

```bash
# Tool or script to convert markdown contract to OpenAPI YAML
./scripts/generate-openapi.sh [contract-file.md]
```

Output: `[service-name]-openapi.yaml`

## Related Documents

- `.github/copilot-instructions.md` - API design standards
- `.github/project-architecture.md` - Integration architecture
- `docs/sprint-context.md` - Current sprint contracts
- `docs/user-stories/` - Stories that reference these contracts
