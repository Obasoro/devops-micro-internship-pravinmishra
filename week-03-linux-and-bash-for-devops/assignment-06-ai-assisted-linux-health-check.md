# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

![screenshot]
(week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 165428.png)
![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 165438.png)
![screenshot]
(week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 174522.png)

---

#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

![screenshot]
(week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 174721.png)

---

### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

When `sudo nginx -t` and the response is successful configuration. You confirm by using `sudo systemctl status nginx` if shows active running and finally, `sudo in-active nginx`

---

**2. What proves that the server is listening for HTTP traffic?**

When the response from `sudo systemctl status nginx` and the port running is seen working

---

**3. Why must you capture a healthy baseline before simulating an incident?**

Necessary for you to capture to know how the server behaving before reunning the incident

---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

![screenshot]
(week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 175555.png)

---

### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

These serves a guardrail for the project to infor it what to do and how to go about executing the detail without revealing credential

---

**2. Why is the human required to execute the recovery command?**

Human are here to serve as the final arbiter of the checks by the agent

---

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The safety rule is put in place to serve as checks

---

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 194111.png)

---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The part where it inspects the environment and produces a read-only plan before creating any Bash code.

---

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Yes, it did not create any files.

---

**3. Why is planning before coding useful in DevOps automation?**

It helps to ensure that the script is well-structured and follows the best practices.

---

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 194737.png)

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 194829.png)



---

#### Screenshot 6 — Middle section showing check functions and conditionals

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 194959.png)

---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 195031.png)

---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 195120.png)

---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The value stored in the array is the names of the check functions.

---

**2. How does the `for` loop use that array?**

The purpose of the `for` loop is to iterate over the array of check function names and execute each function.

---

**3. Why are the health checks separated into functions?**

Code reusability and modularity.

---

**4. What is the purpose of `$(...)` in this script?**

The purpose of `$(...)` is to capture the output of the command and use it as a value.

---

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

The script uses different exit codes to indicate the status of the health check. This allows the script to be used in other scripts or automated systems to determine the status of the health check.

---

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 195715.png)

---

#### Screenshot 10 — Output showing the captured exit code and final summary

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 195424.png)

---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

Add your answer here.

---

**2. Which exact Linux evidence proves the application is serving traffic?**

`ss -tlnp | grep :<port>` this would prove it there is listening port

---

**3. Did your script return exit code 0 or 1? Explain why.**

The code exit 0 proves that the script was succesful without fail.

---

**4. What is the difference between a warning and a failure in this script?**

A warning is guidance for the user to take action, while a failure is a critical issue that needs to be addressed.

---

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 200654.png)

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 195932.png)

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 195947.png)

---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

Giving it write permission is braking safety rule. Do not give agent ability to write directly into your system

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

This is useful because it prevents the skill from making any API calls or model invocations, which is important for security and cost control.

The disable-model-invocation: true flag in YAML frontmatter is useful because it blocks AI agents from autonomously triggering a skill, ensuring it behaves exclusively as a manual slash command
---

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash handle the triage.sh, interpreting it using the interpreter, while claude intelligently use the skill.md to perform operation

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

Providing Claude with a structured skill or evidence is better because it stops the AI from guessing or making up a generic, fictional status report

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 200952.png)

---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 201035.png)

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 201453.png)

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

Nginx
Port
Local connection

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

From response of running `sudo systemctl status nginx` and `curl -I http://localhost` within the script

---

**3. Did Claude execute the recovery command? Why is that important?**

No, claude did not execute the recovery command. This is important you did not give claude the permission to write but only read.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

Context phase

---

**5. Which phase is represented by Claude's explanation?**

Analysis phase

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 203418.png)

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 195947.png)

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

![screenshot](week-03-linux-for-devops\screenshots\assignment-6-week-3\Screenshot 2026-07-18 204057.png)

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

![screenshot]()

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

The scripting process I executed manually

---

**2. What evidence proves that the service recovered?**

After running the systemctl restart

---

**3. Why is the second triage run necessary?**

Yes, to confirm the the system is working and service is fully working

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

It is would make the system effective and less downtime for application

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**


While a chatbot simply chats and guesses based on what you tell it, an agentic workflow connects the AI directly to your terminal so it can look at real-time server evidence and safely run commands for you
---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Obasoro Olakunle Adeyemi

**Date:** 18/07/2026

---

**1. Reported Symptom**

Nginx became unreachable. A triage run at 2026-07-18T19:09:17Z reported the web server as down: the service was inactive, port 80 was closed, and an HTTP request to `http://localhost` failed to connect (status `000`). The site was effectively offline.

---

**2. Evidence Collected**

From `reports/linux-health-report.txt` (run 2026-07-18T19:09:17Z, Overall Status: FAIL, exit code 2):

- `[FAIL] Nginx service is not active`
- `[FAIL] Port 80 is not listening`
- `[FAIL] Local HTTP check returned status 000`
- `[PASS] Root disk usage is 69%`
- `[PASS] Available memory is 124 MB`



---

**3. Most Likely Cause*

Nginx was stopped and never restarted. The logs show a clean, intentional shutdown at **19:08:13** ("Stopping" → "Deactivated successfully" → "Stopped") with no crash, OOM, or failed-state entries. Because the service was inactive, nothing was bound to port 80, which is why the port check failed and the local HTTP probe returned status `000` (connection refused).

The three failures share a single root cause, not three separate problems: service inactive → port 80 closed → HTTP unreachable. Disk (69%) and memory (124 MB) both passed, ruling out resource exhaustion. The "Deactivated successfully" message (rather than a crash) points to a manual or intentional stop.

---

**4. Human-Approved Recovery Action**

The AI recommended the recovery command but did not execute it. A human reviewed and ran it manually:

```
sudo systemctl start nginx
```

---

**5. Verification**

A follow-up triage run at 2026-07-18T19:31:40Z confirmed recovery (Overall Status: HEALTHY, exit code 0):

- `[PASS] Nginx service is active`
- `[PASS] Port 80 is listening`
- `[PASS] Local HTTP check returned status 200`

The service logs showed a successful start proving recovery:

```
Jul 18 19:17:44 ip-172-31-22-67 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
Jul 18 19:17:45 ip-172-31-22-67 systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
```

Subsequent runs at 19:52:21Z and 19:57:45Z remained HEALTHY (PASS: 5, FAIL: 0), confirming the service stayed stable after recovery.

---

**6. Safety Decision**
The AI skill was permitted to **gather** evidence (run the read-only triage script) and **analyze** it (interpret the failed checks and logs), because those actions are read-only and cannot change system state. It was **not** permitted to restart the service, per the project safety rules ("Never stop, start, or restart a service automatically"). Restarting nginx is a state-changing, hard-to-reverse action that requires human judgment: a human must confirm the stop was not intentional (e.g., planned maintenance) before bringing the service back. Keeping the "act" step with a human preserves accountability and prevents the AI from masking or overriding a deliberate operational decision.



---

**7. Agentic Loop Mapping**

This incident followed the loop exactly:

- **Gather** — `bash scripts/linux-triage.sh` collected read-only evidence into `reports/linux-health-report.txt` (the FAIL run at 19:09:17Z).
- **Analyze** — The AI read the report, identified the three FAIL checks, and traced them to a single root cause (nginx stopped at 19:08:13) using only the report evidence.
- **Human Act** — The AI recommended `sudo systemctl start nginx` but did not run it; a human reviewed and executed it manually (service started 19:17:45).
- **Verify** — A fresh triage run (19:31:40Z) returned HEALTHY with all 5 checks passing and a successful start in the logs, confirming nginx and the application recovered.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

<<<<<<< HEAD:week-03-linux-for-devops/assignment-06-ai-assisted-linux-health-check.md
``
=======
`Add your URL here`
>>>>>>> ca849c4fc9d86f701bb2344802dc8e24d2adc20e:week-03-linux-and-bash-for-devops/assignment-06-ai-assisted-linux-health-check.md

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

`Add your URL here`

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [ ] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [ ] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [ ] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [ ] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [ ] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [ ] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [ ] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [ ] Incident summary contains all seven required sections
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots and the Bash report
- [ ] Skill does not have Write permission
- [ ] Skill did not execute any recovery commands
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*