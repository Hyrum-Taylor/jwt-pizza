# **Penetration Testing - Hyrum Taylor**

## **Self-Attack**


### BUG - Price of a pizza is decided by the user loaded webpage
- POSSIBLE HACKS - Users who use HTTP directly (as opposed to through the GUI) were able to choose what price they wanted to pay for their pizza, including a negative price
- FIX - Added a step to the order processing where the price of the pizza is retrieved from the database, and overwrites the user-sent price. The new price is reported back to the user to avoid confusion


### BUG - Email formatting is checked on the user loaded webpage
- POSSIBLE HACKS - By bypassing the GUI, users were able to create accounts with an email that doesn’t match an email regex pattern. This would make making fake accounts very easy
- FIX - Added a check making sure it matches email regex when registering or updating an account. If not, it throws error, and stops the process

### BUG - Email uniqueness was never checked
- POSSIBLE HACKS - When registering or updating an account, a user could overwrite someone else’s account by using that person’s email with no checks.
- FIX - Added a check to make sure that the email is not already in the database when registering.

### BUG - SQL injection vulnerability in the database function updateUser
- POSSIBLE HACKS - Full unrestricted access to the database for anyone who has an account.
- FIX - Updated code to use built-in data sanitation functions
