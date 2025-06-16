# 🔐 Hashcat Tutorial

## 1. Create a Hashed Password Using ***md5sum***

You can create a hash in two different ways:

### a. Interactive Method

Run:
```bash
md5sum
```

This starts a shell where you can type the password directly (not saved to shell history). Copy the hash (omit the trailing space or dash), paste it into a file, and save.

---

### b. Scripted Method

Use this one-liner to generate an MD5 hash and extract just the hash and save it to a file:

```bash
printf '%s' 'password' | md5sum | cut -d ' ' -f 1 > hashed-password.txt
```

#### Breakdown of the command used:

- `printf '%s' 'password'`: Prints `password` without newline.
- `|`: Pipes output to the next command.
- `md5sum`: Generates MD5 hash.
- `cut -d ' ' -f 1`: Extracts only the hash portion.
- `> hashed-password.txt`: Saves it to a file.

Check the result with:

```bash
cat hashed-password.txt
```

---

## 2. Crack the Hash Using Hashcat

When you don’t know the password length, use a mask increment attack:

```bash
hashcat -m 0 -a 3 hashed-password.txt ?a?a?a?a?a?a?a?a --increment --increment-min=1 --increment-max=8
```

### Explanation:

- `-m 0`: MD5 hash type.
- `-a 3`: Brute-force attack.
- `?a`: Any possible character (letters, digits, symbols).
- `--increment`: Start with small lengths and increase.
- `--increment-max=8`: Cap length at 8 characters.

---

### Dictionary vs Mask-Based Attack

> dictionary attack using known password list

When dictionary attack fails, you can try a simple mask-based brute-force (e.g., for the hash of `"abc"`):

```bash
cd ~
mkdir hashcat_lesson
cd hashcat_lesson
printf '%s' 'abc' | md5sum | cut -d ' ' -f 1 > hashed-password.txt
cat hashed-password.txt
hashcat -m 0 -a 3 hashed-password.txt ?l?l?l
```

---

## 3. Use Custom Character Sets in Mask Attacks

To define your own charset (e.g., alphanumeric):

```bash
hashcat -a 3 -m <hash_type> <hash_file> -1 ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1
```

- `-1`: Defines a custom charset.
- `?1`: Placeholder for the defined charset.

---

## 4. Viewing Cracked Hashes

Hashcat stores cracked results in its ***.potfile***:

```bash
~/.local/share/hashcat/hashcat.potfile
```

To view the cleartext result for a previously cracked hash:

```bash
hashcat -m 0 --show hashed-password.txt
```

---

## 🔗 Useful Links

- [Hashcat Tutorial – TheLinuxCode](https://thelinuxcode.com/hashcat-tutorial/)
- [Using Mask Attack – InfoSecScout](https://infosecscout.com/use-mask-attack-with-hashcat/)
