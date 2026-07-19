# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

week-03-linux-for-devops\screenshots\assignment-2-week-3\Screenshot-12.png

---

#### Screenshot 2 — Output of `ip a`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 162644.png

---

#### Screenshot 3 — Output of `sudo ss -tulpen`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 163805.png

---

#### Screenshot 4 — Output of `sudo ufw status`

Using AWS Linux machine, ufw was not installed and saying this handled by AWS security group under the hood

---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

Nginx is listening through the port 80 by using this commands `sudo ss -tulpen | grep :80` and `sudo netstat -tulnp | grep :80`. You can verify by using `sudo systemctl status nginx`

---

**2. What proves SSH is active on port 22?**

The same above command used to verify port :80. `sudo ss -tunp | grep :22` and `sudo systemctl status ssh`

---

**3. Did you find any unexpected open ports? Explain briefly.**

No expected port opened except the port opened through security group. 

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 163635.png

---

#### Screenshot 2 — Output of `sudo nginx -t`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 163732.png

---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 163805.png

---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

Nginx fail to deploy the application and 500 error is displayed on the client side. This would not allow port 80/443 accept new connection from the server

---

**2. What's your basic rollback plan?**

Run s `systemctl status nginx` to see if nginx is running anf if it is running, would check the error log. Check also run `sudo nginx -t` to confirm the configuration file is fine.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 164656.png

---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 164757.png

---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 164757.png

---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

No error log, this maybe due to the application working and no. The configuration is health and working

---

**2. If there were no errors, what does that indicate about the system?**

The error logs leads to the issue causing for the failure of nginx. It could be server problem or sys

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

My access log was not accessible, but access give information about who is logging into a system and what port is open. This gives the idea when a network problem is encountered

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 164842.png

---

#### Screenshot 2 — Output of `free -h`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 164901.png

---

#### Screenshot 3 — Output of `df -h`



---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 165011.png

---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

The CPU usage is at 100% which is critical because it means the server is under heavy load and may not be able to handle additional requests.



---

**2. What happens if disk becomes 100% full in a production server?**

The call on the server would be slow and lead to application crashing. Database failure might also occure leading to stoping of serving agent like nginx

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 175752.png

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

System wide, I did not get result for my search

---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 175921.png

---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

Check from the browser been loaded, if you see the old application, then need to check the deployment process again

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 181655.png

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 181953.png

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 182148.png

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

the missing `;` in nginx configuration file, lead to the failure

---

**2. How did you fix the issue?**

I refixed the missing `;` and ran the `sudo nginx -t` for success

---

**3. How can you avoid this kind of issue in real production systems?**

By running every system failure and check before deployment. The `sudo nginx -t` would show that the ngninx file was having issue and so the engineer would have gone inside and corrected it

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 182335.png

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

week-03-linux-for-devops\screenshots\assignment-3-week3\Screenshot 2026-07-17 182148.png

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

Wrongly deleting the application code for me. The moving of code base and not properly backing it up and deleting it.

---

**2. How did you fix the issue and restore the application?**

Ran a new build and copied the file again and recursely give permission to serve the application

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

Have an autoscaling group and if you delete or temper with the code base in any way, it would be restored automatically. Also never work directly on production

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

SSH key-based authentication is more secure because it uses cryptographic encryption that is much harder to crack than passwords, provides better access control, and eliminates human memory issues like password reuse.

---

**2. Why should only required ports be open on a production server?**

Only required ports should be open to minimize the attack surface and reduce security risks. Unnecessary open ports provide potential entry points for attackers.

---

**3. Why is it important for Nginx to be enabled on boot?**

It is important for Nginx to be enabled on boot so that the web service automatically starts after server reboots, ensuring continuous availability without manual intervention.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Sharing secrets publicly can lead to unauthorized access, data breaches, financial loss, and reputational damage. Attackers can use exposed credentials to compromise systems and steal sensitive data.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Cloud resources should be stopped or terminated when no longer needed to avoid unnecessary costs, reduce security risks, and maintain good resource management practices.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/olakunleobasoro_devops-linux-bashscripting-ugcPost-7484217984589283328-D41X/?highlightedUpdateUrn=urn%3Ali%3Aactivity%3A7484217985625227264&highlightedUpdateType=SOCIAL_SHARE&origin=SOCIAL_SHARE&utm_source=share&utm_medium=member_desktop&rcm=ACoAABJp-z8BWxSilwa0aYicOVVzFmjwFjP4oPM`

---

#### Screenshot — Published LinkedIn post

week-03-linux-for-devops\screenshots\assignment-2-week-3\Screenshot-12.png

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
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