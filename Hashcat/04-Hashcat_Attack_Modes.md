# Hashcat Attack Modes
---
Hashcat offers several attack modes, each designed for different scenarios and types of password cracking. Here are the main attack modes:

1. **Dictionary Attack (Mode 0)**:
   - Uses a list of possible passwords (a dictionary) to try and match the hash.
   - Example command:
     ```bash
     hashcat -a 0 -m 0 hashes.txt wordlist.txt
     ```

2. **Brute-Force Attack (Mode 3)**:
   - Tries all possible combinations of characters within a specified keyspace.
   - Example command:
     ```bash
     hashcat -a 3 -m 0 hashes.txt ?a?a?a?a?a?a?a?a
     ```
   - Here, `?a` represents all possible characters (lowercase, uppercase, digits, and special characters).

3. **Mask Attack (Mode 3)**:
   - A type of brute-force attack that uses a pattern to reduce the number of guesses by focusing on likely formats.
   - Example command:
     ```bash
     hashcat -a 3 -m 0 hashes.txt ?u?l?l?l?d?d?d
     ```
   - This mask targets passwords with one uppercase letter, three lowercase letters, and three digits.

4. **Combination Attack (Mode 1)**:
   - Combines words from two dictionaries to create possible passwords.
   - Example command:
     ```bash
     hashcat -a 1 -m 0 hashes.txt wordlist1.txt wordlist2.txt
     ```

5. **Hybrid Attack (Modes 6 and 7)**:
   - Combines dictionary and mask attacks.
   - Mode 6: Dictionary + Mask
     ```bash
     hashcat -a 6 -m 0 hashes.txt wordlist.txt ?d?d?d
     ```
   - Mode 7: Mask + Dictionary
     ```bash
     hashcat -a 7 -m 0 hashes.txt ?d?d?d wordlist.txt
     ```

6. **Rule-Based Attack (Mode 0 with Rules)**:
   - Applies rules to modify words from a dictionary to create new password candidates.
   - Example command:
     ```bash
     hashcat -a 0 -m 0 -r rules/best64.rule hashes.txt wordlist.txt
     ```

Each attack mode has its strengths and is suitable for different types of password cracking scenarios. Understanding these modes can help you choose the most efficient method for your specific needs.
