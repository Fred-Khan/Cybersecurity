# Password Salt and Pepper
---
### What is a password salt?
A **salt** in password hashing is a random value added to the password before it is hashed. This process enhances security by ensuring that even if two users have the same password, their hashed values will be different due to the unique salts. Here’s why salts are important:

1. **Prevents Rainbow Table Attacks**:
   - Rainbow tables are precomputed tables for reversing cryptographic hash functions, primarily used for cracking password hashes. By adding a unique salt to each password, the effectiveness of these tables is nullified because the same password will have different hashes.

2. **Enhances Uniqueness**:
   - Even if two users have the same password, the addition of different salts will result in different hash values, making it harder for attackers to guess the password.

3. **Mitigates Brute Force Attacks**:
   - Salts increase the complexity and time required for brute force attacks, as attackers must compute the hash for each possible salt and password combination.

### Here’s a simple example to illustrate:

- **Password**: `password123`
- **Salt**: `randomSalt`

The combined string `password123randomSalt` is then hashed, producing a unique hash value. Even if another user has the same password but a different salt, the resulting hash will be different.

The random salt is typically stored alongside the hashed password in the database. This allows the system to retrieve and use the salt when verifying a user's password during future logins. Here’s how it works:

1. **Password Creation**:
   - When a user creates or updates their password, the system generates a random salt.
   - The salt is combined with the user's password, and the combined string is hashed.
   - Both the salt and the resulting hash are stored in the database.

2. **Storage Format**:
   - The salt and the hash can be stored in various formats, but a common approach is to concatenate them into a single string or store them in separate fields within the same database record. Ideally we would like to store the salt in another table or better still in another table in a different database entirely.
   - For example, a database record might look like this:
| user_id | username | salt | hashed_password |
|----------|----------|----------|----------|
| 1 | user1 | randomSaltValue | hashedPasswordValue

3. **Password Verification**:
   - When a user attempts to log in, the system retrieves the stored salt and hash for that user.
   - The system then combines the provided password with the stored salt and hashes the result.
   - If the newly computed hash matches the stored hash, the password is correct.

As you can see, this method ensures that each user's password is uniquely hashed, even if they have the same password, because of a different salt for each user.



### What is a password pepper?
A **pepper** in password hashing is an additional security measure used to enhance the protection of hashed passwords.

1. **Definition**:
   - A pepper is a secret value, typically a random string of characters, added to a password before it is hashed. Unlike a salt, which is stored alongside the hashed password, a pepper is kept secret and stored separately, often in a secure location like a Hardware Security Module (HSM) or within the application's source code.

2. **Purpose**:
   - The primary purpose of a pepper is to add an extra layer of security. By keeping the pepper secret, it makes it significantly harder for attackers to crack the hashed passwords, even if they manage to obtain the hashed values and the salts.

3. **How It Works**:
   - When a user creates or updates their password, the system combines the password with the pepper before hashing. For example, if the password is `password123` and the pepper is `secretPepper`, the system might hash the combined string `password123secretPepper`.
   - The resulting hash is stored in the database, but the pepper is not. This means that even if an attacker gains access to the database, they would still need to know the pepper to successfully crack the passwords.

4. **Comparison with Salt**:
   - **Salt**: A unique value added to each password before hashing, stored alongside the hashed password. It ensures that identical passwords have different hashes.
   - **Pepper**: A secret value added to the password before hashing, not stored with the hashed password. It adds an additional layer of security by being kept secret.

5. **Example**:
   - Suppose a user’s password is `myPassword`. The system adds a salt (e.g., `randomSalt`) and a pepper (e.g., `secretPepper`) to the password before hashing:
     ```plaintext
     Combined string: myPasswordrandomSaltsecretPepper
     ```
   - The combined string is then hashed, and the resulting hash is stored in the database along with the salt. The pepper remains secret.

Using both salt and pepper together significantly enhances password security by protecting against various types of attacks, including rainbow table and brute force attacks. Incidentally, the password length increases which also adds to the running time to crack the password.



Using a fixed pepper in password hashing can introduce several risks:

1. **Single Point of Failure**:
   - If an attacker discovers the fixed pepper, it compromises the security of all hashed passwords that use it. This is because the pepper is the same for every password, making it a single point of failure.

2. **Source Code Exposure**:
   - Fixed peppers are often hard-coded into the application’s source code. If the source code is breached, the attacker can easily find the pepper and use it to crack the hashed passwords.

3. **Difficulty in Changing**:
   - Changing a fixed pepper requires modifying the source code and redeploying the application. This process can be cumbersome and may lead to downtime or other operational issues.

4. **Limited Effectiveness**:
   - While a pepper adds an extra layer of security, its effectiveness is limited if it is not kept secret. Unlike salts, which are unique for each password and stored with the hash, a fixed pepper does not provide the same level of individualized protection.

To mitigate these risks, it’s recommended to use a unique pepper for each password stored separately or to combine both salts and peppers in a way that enhances overall security. 

This approach ensures that even if one element is compromised, the other can still provide a layer of protection.
