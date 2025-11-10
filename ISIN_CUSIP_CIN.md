# 🏦 Identification Guide: ISIN, CUSIP, and CIN

This document explains how to identify and classify **ISIN**, **CUSIP**, and **CIN** codes by visually inspecting or programmatically matching their formats. It also includes their official structure, usage, and validation patterns.

---

## 📘 1. ISIN — International Securities Identification Number

**Full Form:** International Securities Identification Number  
**Standard:** ISO 6166  
**Purpose:** Globally unique identifier for securities (stocks, bonds, ETFs, etc.)  

### 🧩 Structure

```

CCNNNNNNNNNC

````

| Segment | Meaning |
|----------|----------|
| `CC` | Country code (2 letters, ISO 3166) |
| `NNNNNNNNN` | 9-character alphanumeric security identifier |
| `C` | Check digit (numeric, based on Luhn algorithm) |

**Total Length:** 12 characters  
**Example:** `US0378331005` → Apple Inc. (United States)

### 🔍 Identification Pattern

| Property | Description |
|-----------|-------------|
| **Starts With** | 2 letters (country code) |
| **Ends With** | 1 digit (check digit) |
| **Contains** | 9 alphanumeric characters in between |
| **Length** | 12 |

**Regex Pattern:**
```regex
^[A-Z]{2}[A-Z0-9]{9}[0-9]$
````

---

## 📗 2. CUSIP — Committee on Uniform Security Identification Procedures

**Full Form:** Committee on Uniform Security Identification Procedures
**Standard:** ANSI X9.6
**Purpose:** Identifies securities traded in the **U.S. and Canada**.
CUSIP is also embedded within U.S. ISINs (characters 3–11).

### 🧩 Structure

```
IIIIIIJJC
```

| Segment  | Meaning                |
| -------- | ---------------------- |
| `IIIIII` | Issuer code            |
| `JJ`     | Issue number           |
| `C`      | Check digit (0–9 or X) |

**Total Length:** 9 characters
**Example:** `037833100` → Apple Inc.

### 🔍 Identification Pattern

| Property        | Description                     |
| --------------- | ------------------------------- |
| **Starts With** | Alphanumeric (no fixed letters) |
| **Length**      | 9                               |
| **Contains**    | Only A–Z or 0–9                 |

**Regex Pattern:**

```regex
^[A-Z0-9]{9}$
```

---

## 📙 3. CIN — Corporate Identification Number (India)

**Full Form:** Corporate Identification Number
**Authority:** Ministry of Corporate Affairs (MCA), India
**Purpose:** Unique identifier for companies registered under the **Companies Act, 2013** (India).

### 🧩 Structure

```
L/U99999XXYYYYABCNNNNNN
```

| Segment   | Meaning                                             |
| --------- | --------------------------------------------------- |
| `L` / `U` | Listing status (`L` = Listed, `U` = Unlisted)       |
| `99999`   | Industry code (5 digits)                            |
| `XX`      | State code (e.g., `DL` = Delhi, `MH` = Maharashtra) |
| `YYYY`    | Year of incorporation                               |
| `ABC`     | Company type (`PLC`, `PTC`, etc.)                   |
| `NNNNNN`  | ROC registration number (6 digits)                  |

**Total Length:** 21 characters
**Example:** `U74999DL2010PTC123456`

### 🔍 Identification Pattern

| Property        | Description                    |
| --------------- | ------------------------------ |
| **Starts With** | `L` or `U`                     |
| **Includes**    | State and company type letters |
| **Length**      | 21                             |
| **Ends With**   | 6 digits                       |

**Regex Pattern:**

```regex
^[LU][0-9]{5}[A-Z]{2}[0-9]{4}[A-Z]{3}[0-9]{6}$
```

---

## 🧾 Summary Table

| Identifier | Purpose                   | Length | Starts With         | Regex Pattern                                    |
| ---------- | ------------------------- | ------ | ------------------- | ------------------------------------------------ |
| **ISIN**   | Global securities ID      | 12     | 2 letters (country) | `^[A-Z]{2}[A-Z0-9]{9}[0-9]$`                     |
| **CUSIP**  | U.S./Canada securities ID | 9      | Alphanumeric        | `^[A-Z0-9]{9}$`                                  |
| **CIN**    | Indian corporate ID       | 21     | `L` or `U`          | `^[LU][0-9]{5}[A-Z]{2}[0-9]{4}[A-Z]{3}[0-9]{6}$` |

---

## 🧠 Quick Visual Identification Guide

| Identifier | Example                 | Quick Clue                                         |
| ---------- | ----------------------- | -------------------------------------------------- |
| **ISIN**   | `US0378331005`          | 12 chars, starts with country letters              |
| **CUSIP**  | `037833100`             | 9 chars, all alphanumeric                          |
| **CIN**    | `U74999DL2010PTC123456` | 21 chars, starts with L/U, has year and state code |

---

**References:**

* ISO 6166 (ISIN Standard)
* ANSI X9.6 (CUSIP Standard)
* Ministry of Corporate Affairs, India (CIN Format)

```
