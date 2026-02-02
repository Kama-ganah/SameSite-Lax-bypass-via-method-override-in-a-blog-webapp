# Overview
During an assessment of the application’s account management functionality, I identified a moderate-severity Cross-Site Request Forgery (CSRF) vulnerability affecting the email change feature. The application allowed HTTP method overrides via the _method parameter, which, combined with the default SameSite=Lax cookie policy, enabled an attacker to change a victim’s email address through a crafted GET request.

# Methodology

Step 1: Logged in with test credentials and analyzed requests for the email update functionality using Burp Suite.

Step 2: Inspected session cookies to understand the SameSite behavior applied by the browser.

Step 3: Tested CSRF exploitability by crafting a GET request with _method=POST to bypass the Lax cookie restrictions.

Step 4: Delivered a proof-of-concept HTML payload that changed the authenticated user’s email to an attacker-controlled address.

Step 5: Verified the email change was successful without the user’s consent.

# Conclusion

This assessment confirmed that the email change feature is vulnerable to CSRF via method override, bypassing SameSite=Lax protections. Mitigation requires enforcing anti-CSRF tokens, avoiding method override where unnecessary, and setting strict SameSite and Secure attributes on session cookies to protect sensitive account operations.
