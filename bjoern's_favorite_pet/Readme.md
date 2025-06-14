# Bjoern's Favorite Pet

## **Link to Video (german):**

[Watch the video to this challenge](https://go.screenpal.com/watch/cT1eoEn6NfC)

## Table of Contents

1. [Challenge Overview](#challenge-overview)
2. [What do you need to solve the challenge?](#what-do-you-need-to-solve-the-challenge)
3. [Solution](#solution)
   * [Find a Foto or Video that shows a pet](#step-1-find-a-foto-or-video-that-shows-a-pet)
   * [Try to reset Bjoern's password](#step-2-try-to-reset-bjoerns-password)
   * [Shouldn't the task have been solved with the Burp Intruder?](#step-3-shouldnt-the-task-have-been-solved-with-the-burp-intruder)
4. [Summary](#summary)
5. [Risks and Security Recommendations](#risks-and-security-recommendations)
6. [Recommendations for Developers](#recommendations-for-developers)
7. [Pro Tip for Users](#pro-tip-for-users)

## Challenge Overview
  
#### Difficulty

* 3-Star-Challenge

#### Category

* Broken Authentication

#### Description

* Reset the password of Bjoern's OWASP account via the Forgot Password mechanism with the original answer to his security question.

#### Hints from OWASP Juice Shop itself
- He might have trumpeted it on at least one occasion where a camera was running. Maybe elsewhere as well.

#### Hints from the Developer Akademie

* Reset the password for the user `bjoern@owasp.org`.
  * As security question when registering he used the option: `Name of your favorite pet?`.
* Tip:
  * Use the **Burp Intruder**.

## What do you need to solve the challenge?

* If it's not included in the task:
  * Bjoern's email address
    * In the task `Admin Registration` a user was registered with admin status. The administration page, that can be used with this user or the admin account, shows the registered users.
            ```bash
            http://127.0.0.1:3000/#/administration
            ```
    * There you can find Björn's email address regarding to his owasp account:
      * `bjoern@owasp.org` 
    * Do not use *bjoern@juice-sh.op*. This address machtes with another security question.
  * Bjoern's security question
    * Once you find out the email address and enter it into the *Forgotten-Password-Form*, the security question appears automatically
      * `Name of your favorite pet?`
* **OWASP Juice Shop**
  * All Products page: `http://127.0.0.1:3000/#/`
  * Photo Wall: `http://127.0.0.1:3000/#/photo-wall`
* **Google** image search  

OR

* If you have a proper wordlist:
  * **Burpsuite** - [Click here for more information](https://portswigger.net/burp)
    * Proxy Server
    * Burp Intruder

## Solution

### Step 1: Find a Foto or Video that shows a pet

* Would like to know more about Björn. Maybe he left a review. Search for `bjoern` on the product page using the developer tool's Inspect Mode.
  * <ins>Result</ins>: His full name is `Björn Kimminich`.
* Now the clue says Björn's pet can be seen on a photo or in a video.
  * The one-star task called `Missing Encoding` involves making a cat photo visible in the photo gallery.
    * So, have a look at the photo wall:

        ```bash
        http://127.0.0.1:3000/#/photo-wall
        ```

        ![Zatschi](zatschi.png)

    * The three legged cat that is shown there is called **Zatschi**.
      * This path does not lead to results. It's the right cat but Zatschi is her pet name, not the pet's name.
  * Use the **Google** image search:
    * Search query: `björn kimminich owasp`
    * <ins>Result</ins>: An Instagram post from **@bkimminich** that shows Zatschi alias `Zaya`.  

        ![Zaya](zaya.png)

### Step 2: Try to reset Bjoern's password

* Open the login page and select `Forgot your password?` or go directly to the password reset page:

  ```bash
  http://127.0.0.1:3000/#/forgot-password
  ```

* Fill out the form:
  * Email: `bjoern@owasp.org`
  * Security Question: `Zaya`
  * New Password: `abc123`
  * Repeat Password: `abc123`

    ![Forgotten Passwort Form](forgotten_password.png)

* You will be rewarded with confetti and a message:
  * *You successfully solved a challenge: Bjoern's Favorite Pet (Reset the password of Bjoern's OWASP account via the Forgot Password mechanism with the original answer to his security question.)*

### Step 3: Shouldn't the task have been solved with the **Burp Intruder**?

* What ist the **Burp Intruder**?
  * The Burp Intruder is a powerful tool within the **Burp Suite** used to carry out automated attacks on web applications. For example it is used for Brute-Force-Attacks.
  * You can bruteforce the answer to the security question, but you need a suitable word list. I haven't found any that contains the name *Zaya*. Neither a first name list nor a list with pet names.

## Summary

In this challenge there is given a scenario of **Broken Authentication** because of an easily guessable answer of the security question. The security question was provided with the task, but is also displayed in the *Forgot-Password-Form* as soon as you have entered the email address. The answer to the question was easily found because the user loves to share pictures of his pet. In short, information that the victim shares voluntarily and publicly were used to guess sensitive data such as passwords. This procedure is called **Social Engineering or OSINT (Open Source Intelligence)**.  
After finding out the answer the attacker can reset the password using the password reset mechanism (**Reset Password Manipulation**).  
Reasons for this include unauthorized access to user accounts (access to stored credit card information), misuse of the account (using the account to attack additional people (e.g. through phishing emails)), damage to reputation through publication of sensitive data, sale of the compromised account to the owner (blackmail), etc.  
If a website does not provide safe alternatives to security questions like OTP or MFA, the responsibility falls on the user to design the answers so that they cannot be guessed or researched.

## Risks and Security Recommendations

### Key Risks:

1. **Unauthorized Access to Accounts**  
   - Exposure of personal info, orders, stored payment methods

2. **Account Takeover / Abuse**  
   - Spam, phishing attacks launched from the hijacked account

3. **Identity Theft and Reputation Damage**

4. **Blackmail / Ransom Attempts**  
   - Selling account access or extorting the owner

---

### Recommendations for Developers:

- **Avoid weak security questions** entirely if possible
- Implement safer alternatives like:
  - OTP (One-Time Password)
  - 2FA / MFA (Multi-Factor Authentication)
- Never reveal security questions before verifying user identity
- Hash and store answers securely
- Conduct regular security audits and penetration tests

---

### Pro Tip for Users

> [!WARNING] 
> If you must use security questions, choose answers that can’t be guessed or researched — use fictional or unrelated terms.
