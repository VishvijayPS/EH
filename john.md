# Ethical Hacking Lab: ZIP Password Recovery Using John the Ripper

A practical lab demonstrating how to create a password-protected ZIP archive, extract its hash using `zip2john`, and recover a known test password using John the Ripper.

This project illustrates password auditing and recovery in a controlled, authorized lab environment. It focuses on the ethical use of security tools for learning and testing.

## Overview

John the Ripper is a widely used password auditing and recovery tool. It can test candidate passwords against a variety of hash formats and encrypted files.

In this lab:

- a sample text file is created
- the file is saved into a password-protected ZIP archive
- the archive is converted into a hash using `zip2john`
- John the Ripper performs a dictionary attack using a wordlist
- the recovered password is used to extract the archive with `unzip`

This exercise also highlights the importance of password strength and why common passwords remain vulnerable to dictionary-style attacks.

## Objectives

- Understand ZIP encryption and password-protected archives.
- Create a password-protected ZIP file.
- Extract the ZIP hash using `zip2john`.
- Recover a known test password using John the Ripper.
- Display the recovered password result.
- Extract and verify the original file contents.
- Understand the limitations of dictionary attacks.

## Tools and Technologies

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used for the lab |
| John the Ripper | Password recovery and auditing |
| `zip` | Creates password-protected ZIP archives |
| `zip2john` | Extracts ZIP hash information for cracking |
| `unzip` | Lists and extracts ZIP archives |
| `nano` | Creates and edits text files |
| Terminal | Executes commands |

## Requirements

- Kali Linux installed and working
- Internet access for package installation
- Basic Linux terminal familiarity
- A sample text file
- Permission to test the archive under study

## Installation

Update the package list:

```bash
sudo apt update
```

Install the required tools:

```bash
sudo apt install john zip unzip -y
```

Verify the installation:

```bash
john --version
zip -v
unzip -v
command -v zip2john
```

If `zip2john` is missing, check the package files:

```bash
dpkg -L john | grep zip2john
```

## Experiment Procedure

### 1. Create a working directory

```bash
mkdir -p ~/john-zip-lab
cd ~/john-zip-lab
```

Confirm the directory:

```bash
pwd
```

### 2. Create a sample text file

```bash
nano secret.txt
```

Add content such as:

```text
This is my ZIP password recovery lab.
The file is protected with a test password.
```

Save and close the file.

Verify the content:

```bash
cat secret.txt
```

### 3. Create a password-protected ZIP file

```bash
zip -e protected.zip secret.txt
```

When prompted, enter a test password such as:

```text
Cyber123
```

The password will not be shown while typing.

Confirm the archive exists:

```bash
ls -lh
```

### 4. Verify the archive

List archive contents:

```bash
unzip -l protected.zip
```

Test integrity:

```bash
unzip -t protected.zip
```

If necessary, try extracting the file with the password to confirm it is protected.

### 5. Extract the ZIP hash

Convert the archive to a crackable hash:

```bash
zip2john protected.zip > zip.hash
```

Check the generated file:

```bash
ls -lh zip.hash
head -c 120 zip.hash
```

The output contains a hash representation of the ZIP file’s encrypted data, not the original password.

### 6. Create a wordlist

```bash
nano wordlist.txt
```

Add candidate passwords:

```text
password
123456
admin123
Cyber123
kali123
hello123
```

Save and verify:

```bash
cat wordlist.txt
```

### 7. Run John the Ripper

```bash
john --wordlist=wordlist.txt zip.hash
```

John will test each candidate password against the ZIP hash.

For this lab, the expected recovered password is:

```text
Cyber123
```

### 8. Display recovered passwords

```bash
john --show zip.hash
```

This shows the password result that John recovered from the supplied hash.

### 9. Extract the ZIP file

Create a destination folder:

```bash
mkdir -p extracted
```

Extract the archive:

```bash
unzip protected.zip -d extracted
```

When prompted, enter the recovered password.

Verify the extracted content:

```bash
cat extracted/secret.txt
```

The output should match the original file contents.

## Understanding the Commands

| Command | Description |
|---|---|
| `sudo apt update` | Refresh package metadata |
| `sudo apt install john zip unzip -y` | Install required tools |
| `mkdir -p` | Create a directory |
| `cd` | Change directory |
| `nano` | Open a text editor |
| `zip -e` | Create an encrypted ZIP archive |
| `unzip -l` | List archive contents |
| `unzip -t` | Test archive integrity |
| `zip2john` | Extract ZIP hash information |
| `john --wordlist=wordlist.txt zip.hash` | Run a dictionary attack |
| `john --show zip.hash` | Display recovered results |
| `unzip protected.zip -d extracted` | Extract the ZIP file |
| `cat` | Show file contents |

## Expected Results

The experiment should demonstrate:

1. a sample file is created
2. the file is stored in a password-protected ZIP archive
3. `zip2john` successfully extracts password-testing information
4. John the Ripper identifies the correct password from the wordlist
5. the archive is extracted using the recovered password
6. the extracted file matches the original content

Expected test password:

```text
Cyber123
```

## Troubleshooting

### `zip2john: command not found`

Check the package installation:

```bash
sudo apt install john -y
command -v zip2john
dpkg -L john | grep zip2john
```

### `No password hashes loaded`

Verify the hash file has data:

```bash
ls -lh zip.hash
head -c 200 zip.hash
```

If the file is empty, confirm the ZIP archive exists and rerun the hash extraction command.

### Password not recovered

Confirm the correct password is in the wordlist:

```bash
grep -n 'Cyber123' wordlist.txt
```

Then rerun:

```bash
john --wordlist=wordlist.txt zip.hash
```

### Incorrect password during extraction

Check the file and archive:

```bash
file protected.zip
unzip -t protected.zip
```

Make sure the proper archive is being used and that it has not been replaced or corrupted.

## Conclusion

This lab demonstrates how to create a password-protected ZIP archive and recover a password in a controlled Kali Linux environment. The process uses `zip2john` to extract the hash and John the Ripper to test candidate passwords from a wordlist.

The exercise also shows why strong passwords matter. Passwords that appear in common wordlists are especially vulnerable to dictionary-based attacks.

## Safety and Legal Disclaimer

This lab is intended for educational purposes, authorized password auditing, and recovery of files you own or are explicitly permitted to test.

Only use these tools against systems or archives for which you have authorization. Do not access or recover passwords from other people's files without permission.

For secure file storage, prefer strong encryption and unique, long passwords.

## References

- John the Ripper: https://www.openwall.com/john/
- John the Ripper Documentation: https://www.openwall.com/john/doc/
- Kali Linux John package: https://www.kali.org/tools/john/
- Info-ZIP: https://infozip.sourceforge.net/

## Project Summary

- Project: ZIP Password Recovery Using John the Ripper
- Platform: Kali Linux
- Category: Ethical Hacking and Password Security Auditing
