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


### 🔑 Why Knowing the Keyspace Matters

1. **Estimating Runtime**
- The size of the keyspace, combined with your device’s cracking speed (e.g. in MH/s or GH/s), gives you a ballpark estimate for how long an attack will take.
- Example:  
  If your keyspace is 208,827,064,576 and your system runs at 1,348 MH/s (i.e. 1.348 billion guesses/second), then:
  \[
  \text{Estimated Time} = \frac{208,827,064,576}{1,348,000,000} \approx 155 \text{ seconds} \approx 2.6 \text{ minutes}
  \]

2. **Choosing the Right Attack**
- A massive keyspace might steer you away from a full brute-force attack toward wordlists or rule-based attacks, which are more efficient.
- You might also optimize the mask (e.g. narrowing to `?l?l?l?l`) or use incremental lengths to cut down processing time.

3. **GPU/CPU Resource Planning**
- Knowing the expected duration helps manage heat, power usage, and load balancing if multiple sessions or devices are involved.
- You can schedule heavy workloads during off-hours or distribute keyspace across multiple GPUs or nodes in a cluster.

4. **RAM, Disk & Storage**
- While Hashcat doesn't preload the keyspace, certain optimizations (like large wordlists, rules, or potfile lookups) can require substantial memory. Knowing the keyspace helps estimate the demand curve.

5. **Feasibility of Exhaustive Cracks**
- If the keyspace exceeds trillions or quadrillions of combinations, even at high speeds, it might not be practical to exhaust it. Knowing that number helps set realistic expectations—or prove the importance of strong passwords in demonstrations.

