# 🔐 ShadowCheck: Real-Time Password Strength Analyzer

**ShadowCheck** a simple Python tool that checks the **strength of a password** directly from your terminal, built for Kali Linux and other UNIX systems to assess password complexity with real-time feedback. As a Red Teamer, a password complexity checker helps you fingerprint an organization's password policy, craft more effective brute-force and phishing attacks, validate wordlists, and enhance post-engagement reports by demonstrating password weaknesses and educating users.

---

## 📦 Features

- 📏 Enforces minimum length (**8+ characters**)
- 🔠 Requires **uppercase and lowercase** letters
- 🔢 Checks for **at least one digit**
- 🔣 Validates presence of **special characters**
- 🧠 Provides **clear feedback and improvement tips**
- 🟢 Rates password as **Weak**, **Medium**, or **Strong**

---

# ⚙️ Setup Instructions

**1. Create the Project directory and enter directory**
```bash
mkdir PasswordChecker
cd PasswordChecker
```
**3. Create and Edit the Python file housing the python script that checks how strong a password is by looking for length, uppercase, lowercase, numbers, and special characters, then tells you if the password is Strong, Medium, or Weak and gives tips to improve it.**

```bash
vim pchecker.py
```

Paste the code below 👇

```python
import re

def check_password_strength(password):
    length_error = len(password) < 8
    lowercase_error = not re.search(r"[a-z]", password)
    uppercase_error = not re.search(r"[A-Z]", password)
    digit_error = not re.search(r"\d", password)
    special_char_error = not re.search(r"[!@#$%^&*(),.?\":{}|<>]", password)

    errors = {
        "length": length_error,
        "lowercase": lowercase_error,
        "uppercase": uppercase_error,
        "digit": digit_error,
        "special": special_char_error
    }

    score = 5 - sum(errors.values())

    if score == 5:
        return "🟢 Strong", errors
    elif 3 <= score < 5:
        return "🟡 Medium", errors
    else:
        return "🔴 Weak", errors

def main():
    print("=== PassShield: Password Strength Checker ===")
    password = input("Enter a password to check: ")
    strength, errors = check_password_strength(password)

    print(f"\nPassword strength: {strength}")
    if errors["length"]:
        print("- ❌ Too short (minimum 8 characters)")
    if errors["lowercase"]:
        print("- ❌ Add at least one lowercase letter")
    if errors["uppercase"]:
        print("- ❌ Add at least one uppercase letter")
    if errors["digit"]:
        print("- ❌ Include at least one number")
    if errors["special"]:
        print("- ❌ Use a special character like !@#$%^&*")

if __name__ == "__main__":
    main()
```

---

**3. I then Ran the Program to execute the script**

```bash
python3 pchecker.py
```

Then this pops up, you follow the steps to check the strength of

```bash
python3 pchecker.py
=== PassShield: Password Strength Checker ===
Enter a password to check: kali
Password strength: 🔴 Weak
- ❌ Too short (minimum 8 characters)
- ❌ Add at least one uppercase letter
- ❌ Include at least one number
- ❌ Use a special character like !@#$%^&*
```

**I ran the command again to insert a stronger password**

```bash
python3 pchecker.py
=== PassShield: Password Strength Checker ===
Enter a password to check: Amazingday@123

Password strength: 🟢 Strong
```

## 🧠 How Strength is Scored

| Criteria                | Requirement          |
|-------------------------|----------------------|
| Length ≥ 8 characters   | ✅ Required           |
| Contains lowercase      | ✅ Required           |
| Contains uppercase      | ✅ Required           |
| Contains digit          | ✅ Required           |
| Contains special char   | ✅ Required           |

> 💡 **Strength Levels**  
> - 🟢 **Strong**: All 5 criteria met  
> - 🟡 **Medium**: 3–4 criteria met  
> - 🔴 **Weak**: 2 or fewer criteria met  


