# TryHackMe — Intermediate Nmap

**Author:** Maloy Roy Orko
**Platform:** TryHackMe
**Room:** Intermediate Nmap
**Category:** Nmap | Network Enumeration

---

## 📌 Challenge Description

You've learned some great Nmap skills! Now can you combine that with other skills with Netcat and protocols, to log in to this machine and find the flag?

The VM is listening on a **high port**, and connecting to it may provide information that can be used to connect to a lower port commonly used for remote access.

---

## 🔎 Step 1 — Nmap Scan

The challenge description gives us an important clue: the target is listening on a **high-numbered port**.

Let's start with a basic Nmap scan:

```bash
nmap 10.49.181.27
```

![Nmap Scan](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiKnOKSnNrsvEt5f1s0Uuk1SjZfgIyin4lwJauGJTF6JY0W3-oPbayQO8XcGGHpyRAZ7NAjd2itgG8vnlNruFZoobTB6HsTQCLqeb21JKTqhbSEgqHS1RN0MDB-8DemaYoQkyHuMobsU6WvBqcbQn1u6NaFVWp_HA1rN9YwmcjvrbxVdhc3L1JO5GAi5JU/w613-h277/Screenshot%202026-08-11%20111057.png)

The scan reveals a service running on a high-numbered port.

---

## 🔌 Step 2 — Connect to the High Port

The description suggests connecting to the high port to obtain information that can help us access the machine.

Using Netcat:

```bash
nc <TARGET_IP> <HIGH_PORT>
```

![Netcat Connection](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhBAqzonj1dJzQ7AUuj0vqBjzcb6lNZHBF83Krb4eqG4SF_I45YENmRcbsRikffcpjWwvXtrMe7JtTrCzR4uUL6MrIufeB8wASoXJsygETQNSFUm_2p7HzQ1N6M459V1vlHssD8wzuJqZZyS7B-dsIFTR35Fojzw9kRE8CJlxoUL3px5r71hFCa2R7RvcA/w575-h254/Screenshot%202026-08-11%20111314.png)

The service provides credentials:

```text
Username: ubu***
Password: **********************
```

These credentials can be used to access the remote-access service on the lower port.

---

## 💻 Step 3 — Find the Flag

After logging into the machine, I started enumerating the filesystem.

Check the current directory:

```bash
pwd
```

List files:

```bash
ls -la
```

Move to `/home`:

```bash
cd /home
ls
```

Then enter the `users` directory:

```bash
cd users
ls
```

Finally, read the flag:

```bash
cat flag.txt
```

---

## 🚩 Flag

The flag was successfully retrieved from:

```text
/home/users/flag.txt
```

![Flag](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEUXioZZHpr0gXJ6IyTI-cpTTCM2ifeV3SJx1duzhPBmfLCL2aQsA42T8tnT656si9FrGDOL9ZvHMHLEbD1Fq8RFN41KMtRTSaImJwxi_rz78AP5kBQ4psb1Pq3dKE-yXggu9HkhXbFbmty4xjQjL5wqvJv3etuEp3Nyup5D6X9Wv0RUhYejp5jeWmaPA/w646-h246/Screenshot%202026-08-28%20223133.png)

```text
flag{************************************}
```

---

## 🧠 Key Takeaways

* Use the challenge description for enumeration clues.
* Nmap helps identify open ports and running services.
* High-numbered ports can expose useful information.
* Netcat can be useful for interacting directly with network services.
* Once authenticated, basic Linux commands are enough to locate the flag.

---

## ✅ Conclusion

The challenge followed a simple enumeration-to-access workflow:

```text
Nmap Scan
    ↓
High-Port Service
    ↓
Netcat
    ↓
Credentials
    ↓
Remote Access
    ↓
Linux Enumeration
    ↓
Flag
```

**Challenge completed! 🚩**

**— Maloy Roy Orko**
