# ZIP Password Recovery Using John the Ripper

## Ethical Hacking Lab Experiment

**Aim:** To create a password-protected ZIP archive, extract its password hash using `zip2john`, recover a known test password using John the Ripper, and extract the protected file using `unzip`.

## Table of Contents

- [Introduction](#introduction)
- [Objectives](#objectives)
- [Tools and Technologies](#tools-and-technologies)
- [Requirements](#requirements)
- [Installation](#installation)
- [Experiment Procedure](#experiment-procedure)
- [Understanding the Commands](#understanding-the-commands)
- [Expected Results](#expected-results)
- [Troubleshooting](#troubleshooting)
- [Conclusion](#conclusion)
- [Safety and Legal Disclaimer](#safety-and-legal-disclaimer)

## Introduction

John the Ripper is an open-source password security auditing and password recovery tool. It can test candidate passwords against supported password hashes and encrypted file formats.

In this experiment, a sample text file is created and protected using ZIP encryption. The `zip2john` utility extracts the information required for password testing. John the Ripper then checks a small wordlist containing candidate passwords.

After recovering the test password, the archive is extracted using the `unzip` utility.

## Objectives

- Understand ZIP file encryption.
- Create a password-protected ZIP archive.
- Extract ZIP password hash information using `zip2john`.
- Perform a dictionary-based password recovery test.
- Display recovered password results.
- Extract and verify the original file.
- Understand the limitations of dictionary attacks.

## Tools and Technologies

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system for the experiment |
| John the Ripper | Password recovery and auditing |
| zip | Create password-protected ZIP archives |
| zip2john | Extract ZIP password-testing information |
| unzip | List and extract ZIP archives |
| Nano | Create and edit text files |
| Terminal | Execute Linux commands |

## Requirements

- A working Kali Linux installation or virtual machine.
- Internet connectivity for installing packages.
- Basic knowledge of Linux terminal commands.
- A sample text file.
- Permission to test the archive being examined.

## Installation

Update the package list:

```bash
sudo apt update
```

Install the required utilities:

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

If `zip2john` is not found, check the installed package files:

```bash
dpkg -L john | grep zip2john
```

## Experiment Procedure

### Step 1: Create a Working Directory

Create a directory for the experiment:

```bash
mkdir -p ~/john-zip-lab
cd ~/john-zip-lab
```

Verify the current directory:

```bash
pwd
```

### Step 2: Create a Sample Text File

Create a file named `secret.txt`:

```bash
nano secret.txt
```

Enter the following sample content:

```text
This is my ZIP password recovery lab.
The file is protected with a test password.
```

Save the file using `Ctrl + O`, press `Enter`, and exit with `Ctrl + X`.

Verify the contents:

```bash
cat secret.txt
```

### Step 3: Create a Password-Protected ZIP File

Run:

```bash
zip -e protected.zip secret.txt
```

When prompted, enter the following test password twice:

```text
Cyber123
```

The password will not appear on the terminal while typing.

Verify that the archive was created:

```bash
ls -lh
```

The directory should contain:

- `secret.txt`
- `protected.zip`

### Step 4: Verify the ZIP Archive

List the contents of the archive:

```bash
unzip -l protected.zip
```

Test the archive's integrity:

```bash
unzip -t protected.zip
```

To verify password protection, attempt extraction and enter the test password when prompted. If a file with the same name already exists, avoid overwriting it.

### Step 5: Extract the ZIP Password Hash

Use `zip2john` to extract the password-testing information:

```bash
zip2john protected.zip > zip.hash
```

Inspect the generated file:

```bash
ls -lh zip.hash
head -c 120 zip.hash
echo
```

The output contains a long record representing the archive's encryption data. This record is not the original password.

### Step 6: Create a Wordlist

Create a file named `wordlist.txt`:

```bash
nano wordlist.txt
```

Add the following candidate passwords:

```text
password
123456
admin123
Cyber123
kali123
hello123
```

Save the file and verify its contents:

```bash
cat wordlist.txt
```

The list contains several incorrect candidates and the known test password.

### Step 7: Run John the Ripper

Execute the dictionary attack against the extracted hash:

```bash
john --wordlist=wordlist.txt zip.hash
```

John tests the candidate passwords against the ZIP hash.

If the password is successfully recovered, the result should identify the password associated with the archive. For this experiment, the expected password is `Cyber123`.

### Step 8: Display Recovered Results

Run:

```bash
john --show zip.hash
```

This displays recovered results available in John's password pot file for the supplied hash.

The output format may vary according to the installed version and archive format.

### Step 9: Extract the ZIP File

Create a separate directory for extraction:

```bash
mkdir -p extracted
```

Extract the archive:

```bash
unzip protected.zip -d extracted
```

When prompted, enter the recovered test password.

Verify the extracted file:

```bash
cat extracted/secret.txt
```

The output should be:

```text
This is my ZIP password recovery lab.
The file is protected with a test password.
```

## Understanding the Commands

| Command | Description |
|---|---|
| `sudo apt update` | Refreshes package information |
| `sudo apt install john zip unzip -y` | Installs the required utilities |
| `mkdir -p` | Creates a directory |
| `cd` | Changes the current directory |
| `nano` | Opens a terminal text editor |
| `zip -e` | Creates a password-encrypted ZIP archive |
| `unzip -l` | Lists archive contents |
| `unzip -t` | Tests archive integrity |
| `zip2john` | Extracts ZIP password-testing information |
| `john --wordlist=wordlist.txt zip.hash` | Tests candidates from a wordlist |
| `john --show zip.hash` | Displays recovered results |
| `unzip protected.zip -d extracted` | Extracts the archive into a directory |
| `cat` | Displays file contents |

## Expected Results

The experiment should demonstrate the following:

1. A sample text file is created.
2. The file is stored inside a password-protected ZIP archive.
3. The ZIP archive's password-testing information is extracted into `zip.hash`.
4. John the Ripper successfully identifies the known password from the supplied wordlist.
5. The protected archive is extracted using the recovered password.
6. The extracted file's contents match the original sample file.

**Expected test password:** `Cyber123`

Password recovery depends on the archive format, the quality of the hash extraction, and whether the correct password is among the candidates tested.

## Troubleshooting

### Error: `zip2john: command not found`

Check the package installation:

```bash
sudo apt install john -y
command -v zip2john
dpkg -L john | grep zip2john
```

### Error: `No password hashes loaded`

Check whether the hash file contains data:

```bash
ls -lh zip.hash
head -c 200 zip.hash
echo
```

If the file is empty, verify that `protected.zip` exists and rerun the extraction command.

### Password Not Recovered

Check that the wordlist contains the correct test password:

```bash
grep -n 'Cyber123' wordlist.txt
```

Then rerun:

```bash
john --wordlist=wordlist.txt zip.hash
```

A dictionary attack cannot guarantee recovery if the correct password is not included in the tested candidates.

### Incorrect Password During Extraction

Confirm that you are using the correct archive and password:

```bash
file protected.zip
unzip -t protected.zip
```

Ensure that the ZIP file has not been replaced or corrupted.

## Conclusion

This experiment demonstrates how to create a password-protected ZIP archive and perform password recovery in a controlled Kali Linux environment.

The `zip2john` utility extracts the encryption information required by John the Ripper. John tests candidate passwords from a wordlist, and the recovered password can then be used with `unzip` to extract the protected file.

The experiment illustrates why password strength matters and why simple passwords that appear in common wordlists are vulnerable to dictionary attacks.

## Safety and Legal Disclaimer

This experiment is intended for educational purposes, authorized password auditing, and recovery of files you own or are permitted to examine.

Only test archives for which you have authorization. Do not use password-recovery tools to access other people's private files without permission.

For confidential information, prefer a modern archive encryption method such as AES-based ZIP encryption and use a strong, unique password.

## References

- [John the Ripper — Official Website](https://www.openwall.com/john/)
- [John the Ripper — Documentation](https://www.openwall.com/john/doc/)
- [Kali Linux — John the Ripper Package](https://www.kali.org/tools/john/)
- [Info-ZIP — ZIP and UNZIP Utilities](https://infozip.sourceforge.net/)

---

**Experiment:** ZIP Password Recovery Using John the Ripper  
**Platform:** Kali Linux  
**Category:** Ethical Hacking and Password Security Auditing
