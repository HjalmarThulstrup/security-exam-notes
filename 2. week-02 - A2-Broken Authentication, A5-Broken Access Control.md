# Week-02 [A2 - Broken Authentication](https://www.owasp.org/index.php/Top_10-2017_A2-Broken_Authentication)[A5 - Broken Access Control](https://www.owasp.org/index.php/Top_10-2017_A5-Broken_Access_Control)
## Explain about __OWASP A2__, and explain a number of the problems that would leave your application vulnerable to A2-problems
OWASP qualified __Broken Authentication__ as the number 2 security risk in 2017. They explain it thusly: 
>Application functions related to __authentication__ and __session management__ are often implemented incorrectly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users' identities temporarily or permanently.

An authentication attack can happen in a number of ways, the most common being cracked __weak passwords__ and automated __bruce force attacks__ like __credential stuffing__.
There are other, less common ways, of exploiting some form of __broken authentication__ weakness. To list a few
* weak or ineffective password recovery like "knowledge-based answers", which cannot be made safe
* storing plaintext, encrypted or weakly hashed passwords
* missing or ineffective MFA/2FA
* exposing session IDs in the URL
* improper session ID validation.

## For each of the problems explained above, explain how this problem could have been prevented

#### Weak passwords
Implementing weak-password checks, like testing new or changed passwords against a list of common and/or bad passwords.
Ensuring password complexity through length and symbol requirements *could* also help, though less so than enforcing proper pass-phrases.

#### Allowing automated- and brute force attacks
__Automated__ and __brute force__ attacks, like __credential stuffing__ can be circumvented through a properly implemented MFA/2FA solution.

#### Weak or ineffective password recovery
Requiring a stronger proof-of-identity than the common knowledge-based checks (what is your first teachers name?, where did you live 10 years ago? etc.).
This could be some form of transaction ID, in the case of a webshop, or maybe even a MFA/2FA solution.

#### Storing plaintext, encrypted or weakly hashed passwords
The solution here is self-explanatory.
Hash with a strong (unbroken) hashing algorythm like bcrypt, SHA256/SHA512 or something of similar complexity.
Common advice is to also base64 encode passwords before hashing them, but this actually *lowers* the security of your passwords by normalizing the characters used in encryption.
The more diverse, the better!

#### Missing or ineffectial MFA/2FA
Well, implement a good one instead :^)
Follow the principles of strong MFA closely, using 2 or more of the following:
* something the user, and only the user, is
* something the user, and only the user, knows
* something the user, and only the user, has

This is why the most common form of MFA is password (something user knows) + mobile phone (something user has)

#### Exposing session IDs in the URL & Improper session ID validation
OWASP says it best here.
>Use a server-side, secure, built-in session manager that generates a new random session ID with high entropy after login. Session IDs should not be in the URL, be securely stored and invalidated after logout, idle, and absolute timeouts.

## Explain the idea behind the term "Credential Stuffing"
Credential stuffing is a form of automated brute-force attacks using previously breached username/password pairs from this, or other sites.
Many people re-use usernames and passwords across sites, which is why this attack works.
For example, lets say John Doe with password 1235 has a google account, and google's user database is somehow breached. His password is now snatched by a hacker. He, ofcourse, changes his password on google, but not on FaceBook, where the hacker now executes their attack. His account is breached.

## Demonstrate how you, in practice, have, or could, remove some of the vulnerabilities listed above
The [security-presentation project](https://github.com/JonasGroenbek/security-presentation) contains examples for proper hasing and improper session ID management.

## Explain about OWASP A5, and explain a number of the problems that would leave your application vulnerable to A5-problems
OWASP put __Broken Access Control__ at 5 in 2017. Access Control is the security practice of limiting user permissions and assuring that a user cannot act outside of their intended permissions.
Failure to do this typically leads to sensitive information being disclosed, modified or deleted.

One thing that could leave a program open to this, is __broken authentication__, or some of the problems that lead to broken authentication. Weak passwords, improper session management, lack of MFA etc.
On top of these, there is bypassing access control checks by modifying the URL, Allowing primary keys to be changed to another user (SQL injection?), metadata manipulation like tampering with, or reusing a JSON web token.

## For each of the problems explained above, explain how this problem could have been prevented

#### Bypassing access control checks
Denying access to any non-public resources by default largely solves this.

#### Allowing primary keys to be changed to another user
First of all, securing against SQL injection, allowing only admin users to perform changes to a user's internal data (non-visible data), and disabling root access to the database are all standards that should be followed.
Model access controls should enforce record ownership (user can only make changes to their own data) rather than accepting changes to any user data.

#### metadata manipulation
JWT tokens should be invalidated on the server after logout.

## Demonstrate how you, in practice, have removed some of the vulnerabilities listed above
The [YDB stock tacker](https://github.com/MartinMoller/YDB-StockTrackerFrontend) contains proper JWT token invalidation.
The [JS locationblog project](https://github.com/David-M-Nielsen/miniproject-client) uses a NoSQL database, which circumvents SQL injection and primary key changes.

## Demonstrate at least one practical example of a A5 Vulnerability, and show how you have solved the problem (removed the vulnerability)
See above
