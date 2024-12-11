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

### BUG - Admin username/password are automatically generated, not automatically updated
- POSSIBLE HACKS - Full unrestricted access to everything for anyone who finds them from the code
- FIX - Changed admin credentials to not be the defaults


## **Peer Attack - Hyrum attacking pizza.cs329.click**


### Attack - SQL injection when updating user
- GOOD - Can’t do this attack without an admin user, which stopped the attack
- BAD - From a user point of view this is frustrating, as there are legitimate reasons to update an account

###  Attack - Ordered large number of pizzas (100 pizzas, sent order ~100 times)
- BAD - "Failed to fulfill order at factory", and I didn’t get the pizzas. Also, the user tab stops showing orders after 10, including a normal-sized order done after the large ones (although the HTTP response includes all orders)

### Attack - Ordering a pizza for negative BC
- GOOD - Said out of range, invalid order
- BAD - The error returned a stack trace, which is inadvisable

### Attack - Ordering a pizza for 0 bitcoin
- BAD - Successfully bought pizza for 0 BC

### Attack - Registering user with invalid email address
- BAD - Successfully registered user without using email address using Burp suite

### Attack - Tried creating new account with same email as existing user
- BAD - Was able to create a new account with the same users.
- GOOD - Was not able to see original user’s orders. Was not able to log in again with the new account. Did not overwrite original account.
- BAD - By checking if able to log in again, exposes if a given email has been used on the website before.


## **Peer Attack - Stephen (TA) attacking my website**


### Attack - SQL injection
- GOOD - secure

### Attack - Default credentials
- GOOD - default password was changed for Admin
- BAD - default password was not changed for Franchisee

### Attack - Pizza prices can be chosen from the user side
- GOOD - Prices changed to be found from database, not from user. Secure as far as we could tell
