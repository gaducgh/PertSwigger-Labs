
# PortSwigger Labs - SQL Injection Journey 

This repository contains my solutions and technical write-ups for the PortSwigger Web Security Academy labs.

---

## 1. SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

### Objective
The goal of this lab is to exploit a SQL injection vulnerability in the category filter to display all products, including unreleased ones.

### Vulnerability Analysis
- *Entry Point:* The category parameter in the URL.
- *Initial Test:* Adding a single quote ' to the URL resulted in a 500 Internal Server Error, confirming the parameter is vulnerable.
 
### Exploitation (The Payload)
I used the following payload to bypass the logic:
' OR 1=1--%20

*Final URL:*
`https://<lab-id>.web-security-academy.net/filter?category=Gifts' OR 1=1--%20`

### 💡 Why it worked?
1. The ' closed the original string.
2. OR 1=1 made the condition always TRUE, forcing the database to return all rows.
3. -- ` (followed by a space) commented out the rest of the original query, removing the filter for `released = 1.