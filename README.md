# Suspicious-login-bruteforce-lab
SOC Investigation analyzing brute force login attempts using Linux authentication logs.
Suspicious Login & Brute‑Force Detection Lab
SOC Investigation Project — Authentication Log Analysis
 Overview
This project simulates a real‑world brute‑force attack against a Linux system and walks through the full SOC investigation process. Using authentication logs from /var/log/auth.log , the goal is to detect suspicious login attempts, identify brute‑force patterns, extract attacker IPs, and document findings in a SOC‑style report.
This lab demonstrates core SOC analyst skills including log analysis, pattern recognition, and incident reporting.

 Objectives
• 	Analyze Linux authentication logs
• 	Identify brute‑force attack patterns
• 	Extract attacker IP addresses
• 	Determine targeted usernames
• 	Understand attacker behavior
• 	Produce a SOC‑style investigation report

 Tools & Technologies
• 	Ubuntu Linux VM
• 	Terminal / Bash
• 	/var/log/auth.log
• 	grep, awk, sort, uniq
• 	SOC‑style documentation

 Key Findings
• 	20 failed SSH login attempts within ~1 minute
• 	Attempts occurred every 3 seconds (automated)
• 	Multiple usernames probed: admin, test, guest 
• 	Heavy targeting of the root account
• 	Single attacker IP: 185.199.110.23
• 	No successful logins observed

 Sample Evidence (Simulated Log Excerpts)
Failed password for invalid user admin from 185.199.110.23
Failed password for invalid user test from 185.199.110.23
Failed password for invalid user guest from 185.199.110.23
Failed password for root from 185.199.110.23
(repeated 17 times)

  Analysis Commands Used
Count failed attempts by IP:
grep "Failed Password" simulate_auth.log | awk {print $(NF-3)}' | sort | uniq -c | sort -nr

Count failed attempts by username:
grep "Failed Password" simulated_auth.log |awk '{print $9}' | sort | uniq -c | sort -nr

View all suspicious entries:
grep "Failed password" simulated_auth.log

 Attacker Behavior Summary
• 	The attacker probed multiple common usernames
• 	Quickly shifted focus to the root account
• 	Attempted 20 passwords in rapid succession
• 	Behavior consistent with automated brute‑force tools
• 	Attack intensity: medium
• 	Risk level: high, due to root targeting

 Recommendations
• 	Disable root SSH login
• 	Enable fail2ban or SSH rate limiting
• 	Use SSH keys instead of passwords
• 	Monitor for repeated failed attempts
• 	Block attacker IP if appropriate
• 	Consider changing default SSH port

 Full SOC Report
The complete SOC‑style investigation report is included in this repository as a PDF/DOCX.

 Skills Demonstrated
• 	Linux log analysis
• 	Brute‑force detection
• 	Attack pattern recognition
• 	Evidence extraction
• 	SOC‑style reporting
• 	Command‑line investigation
• 	Cybersecurity documentation

 Author
Lanisha Thomas
Cybersecurity Student — Western Kentucky University
