# GitHub API Troubleshooting Guide

This guide outlines an action plan for the most common errors when interacting with the GitHub API, aiming to ensure robust and continuous data extraction.

---

## Common Error 1: 401 Unauthorized

This is the most frequent authentication-related error. It indicates the API couldn’t validate your identity.

### Problem Description

The request is rejected because the provided credentials are invalid, incorrect, or lack the necessary permissions.

### Primary Causes and Solutions

#### Invalid or Expired Token

**Action Plan:**
- **Validate the Token:** Ensure the Personal Access Token (PAT) is active and hasn’t been revoked.
- **Verify Scopes:** Confirm the token includes necessary scopes (e.g. `repo`).
- **Regenerate if Needed:** If the token is invalid, generate a new one via GitHub’s developer settings.

#### Token Without Required Scopes

**Solution:**
- Make sure your PAT includes the appropriate scopes for the action you’re performing.  
- For this project, the `repo` scope is sufficient for accessing both public and private repository information.

#### Authorization Header Error

**Solution:**
- Check your code to confirm that the `Authorization` header is sent correctly.  
- The format must be: `token YOUR_TOKEN_HERE`.  
- A common mistake is forgetting the word `"token"` before the PAT.

---

## Common Error 2: 403 Forbidden – Rate Limit Exceeded

This error is usually linked to the API’s usage limits (*Rate Limiting*).

### Problem Description

The API rejects the request because you’ve exceeded the number of allowed calls within a set time period.

### Primary Causes and Solutions

#### Unauthenticated Requests

**Cause:**  
Making API calls without a PAT.  
The limit for anonymous requests is very low (about 60 per hour).

**Solution:**  
- Always authenticate with a PAT.  
- This raises the limit to **5,000 requests per hour**, which is suitable for most data extraction tasks.

#### Aggressive Scripts

**Cause:**  
A script performs a massive number of requests in a short time (e.g. looping through thousands of result pages without breaks).

**Solution (Proactive Approach):**
- **Check Response Headers:**  
  GitHub’s API responses include headers such as:
  - `X-RateLimit-Limit` (total limit)
  - `X-RateLimit-Remaining` (how many requests remain)
  - `X-RateLimit-Reset` (when the counter resets)  
  An advanced script can read these headers and pause when request limits are nearly reached.

- **Add Delays:**  
  Implement brief pauses (`time.sleep()`) in long loops to space out requests over time and avoid hitting the limit quickly.