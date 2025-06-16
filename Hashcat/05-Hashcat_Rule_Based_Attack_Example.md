# Hashcat Rule-Based Attack Example
---
Creating custom rules in Hashcat allows you to define specific modifications to apply to your wordlist, generating new password candidates. Here are some examples to help you get started:

1. **Understand Rule Syntax**:
   - Rules are written in a specific syntax where each line represents a different rule.
   - Common rule commands include:
     - `:` - Do nothing.
     - `l` - Lowercase all letters.
     - `u` - Uppercase all letters.
     - `c` - Capitalize the first letter and lowercase the rest.
     - `$X` - Append character `X` to the end.
     - `^X` - Prepend character `X` to the front.
     - `sXY` - Replace all instances of `X` with `Y`.

2. **Create a Rule File**:
   - Open a text editor and write your rules, one per line.
   - Save the file with a `.rule` extension, for example, `custom.rule`.

   Example rule file (`custom.rule`):
   ```plaintext
   l
   u
   c
   $1
   ^1
   s@3
   ```

3. **Apply the Rule File in Hashcat**:
   - Use the `-r` option to specify your rule file when running Hashcat.
   - Example command:
     ```bash
     hashcat -a 0 -m 0 -r custom.rule hashes.txt wordlist.txt
     ```

4. **Test and Debug Your Rules**:
   - It’s a good practice to test your rules on a small subset of your wordlist to ensure they work as expected.
   - You can use the `--stdout` option to see the output of your rules without actually running the attack:
     ```bash
     hashcat --stdout -r custom.rule wordlist.txt
     ```

5. **Use Existing Rule Sets**:
   - Hashcat comes with several pre-defined rule sets that you can use as a reference or starting point. These are located in the `rules` directory of your Hashcat installation.

For more detailed tutorials, you might find these videos helpful:
- [Hashcat Creating Custom Rules: Ten Minute Tutorials](https://www.youtube.com/watch?v=PyIkY6hBDRI) - A video tutorial explaining how to create custom rules.
- [Performing Rule Based Attack Using Hashcat](https://www.armourinfosec.com/performing-rule-based-attack-using-hashcat/) - A detailed guide on rule-based attacks.
