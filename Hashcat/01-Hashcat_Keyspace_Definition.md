# Hashcat Keyspace Definition
---
In Hashcat, the term **keyspace** refers to the total number of possible password candidates that will be tested during a cracking session. It essentially defines the scope of the attack by specifying the length and character set of the passwords being tested.

Here's a more detailed breakdown:

1. **Character Set**: The set of characters that can be used in the passwords. This can include lowercase letters, uppercase letters, numbers, and special characters.

2. **Password Length**: The length of the passwords being tested. For example, if you're testing passwords that are exactly 8 characters long, the keyspace will be calculated based on this length.

3. **Combination Calculation**: The keyspace is calculated by raising the number of characters in the character set to the power of the password length. For example, if you're using a character set of 26 lowercase letters and testing passwords of length 8, the keyspace would be \(26^8 = 208,827,064,576\).

4. **Mask Attack**: When using a mask attack, the keyspace is defined by the mask you provide. For example, a mask of `?l?l?l?l?l?l?l?l` (where `?l` represents a lowercase letter) would have a keyspace of \(26^8 = 208,827,064,576\).

5. **Keyspace Command**: Hashcat provides a `--keyspace` option to display the keyspace for a given attack configuration. This helps you understand the size of the task before starting the attack.

Understanding keyspace is crucial for estimating the time and resources needed for a password cracking attempt. It helps in planning and optimising the attack strategy
