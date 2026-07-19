# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 064713.png)

---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 064812.png)

---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash also known as Bourne Again Shell is a Unix shell and command language that reads commands from input and executes them. Its core function are command interpretation, scripting and programming interface.

---

**2. What is the difference between shell and Bash?**

The difference between shell and bash is that shell is a general term for a command-line interpreter, while bash is a specific type of shell. There are several shell type, and they include zsh, fish, Tcsh, Ksh.

---

**3. Why is it important to confirm the Bash version before writing scripts?**

It is important to confirm the Bash version before writing scripts because different versions of Bash may have different features and syntax, and some features may not be available in older versions of Bash.

---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 065327.png)

---

#### Screenshot 2 — Output of `./first-script.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 065424.png)

---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 065459.png)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

This is called the shebang, the path to where the interpreter is located

---

**2. Why do we use `chmod +x` before running a script?**

This gives the script execute permission, allowing it to be run directly. It grant and make the script executable

---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

The difference is that `./script.sh` runs the script in the current shell environment, while `bash script.sh` runs the script in a new shell environment. The `./` prefix tells the system to execute the script directly, while `bash` explicitly invokes the Bash interpreter.

---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 065942.png)

---

#### Screenshot 2 — Output of `./user-info.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 070028.png)

---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable is a store of value. it enables script to store, process and output data dynamically

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Bash interprete spaces as value

---

**3. How do you access the value stored inside a Bash variable?**

Use the $ prefix to access the value stored inside a Bash variable, like $variable_name or ${variable_name}

---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 070521.png)

---

#### Screenshot 2 — Output of `./tools-checklist.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 070609.png)

---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array in script writing provide a structured way to handle multiple related value in script, making the code more organized and efficient

---

**2. Why are arrays useful in scripts?**

Arrays are useful in scripts because they allow you to store and manage multiple values in a single variable, making it easier to work with collections of data. They provide a structured way to handle related values, making the code more organized and efficient.

---

**3. What does `"${tools[@]}"` mean?**

The [@] syntax with quotes is the standard way to iterate over all array elements safely in Bash scripts.

---

**4. What is the purpose of the `for` loop in this script?**

For serves looping process to iterate through each element in the array

---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 071015.png)

---

#### Screenshot 2 — Output of `./counter.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 071059.png)

---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop is a programming construct that repeatedly executes a block of code as long as a specified condition is true.

Core concept:

Repetition - Runs the same code multiple times
Iteration - Each cycle through the loop is one iteration
Condition - Determines when the loop starts and stops
Automation - Eliminates repetitive manual coding

---

**2. Why do we use loops in Bash scripting?**

Loops are used in Bash scripting to automate repetitive tasks, process multiple items efficiently, and reduce code duplication. They allow scripts to iterate over lists, files, or ranges, making them more flexible and maintainable.

---

**3. How many times did the loop run in your script?**

5 times

---

**4. What would you change if you wanted the loop to run 10 times?**

Change the range in the for loop from 5 to 10.

---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 071738.png)

---

#### Screenshot 2 — Content of `file-check.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 071826.png)

---

#### Screenshot 3 — Output of `./file-check.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 071911.png)

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

This `-d` tells the script to check if the path is a directory.

---

**2. What does `-f` check in Bash?**

This `-f` tells the script to check if the path is a regular file.

---

**3. Why should file and directory paths be stored in variables?**

Why file and directory paths should be stored in variables:

Benefits of using variables for paths:

1. Maintainability:

Single source of truth - Change path in one place, updates everywhere
Easy updates - Modify the variable instead of finding/replacing throughout script
Centralized configuration - All paths defined at the top of the script
2. Reusability:

Flexible deployment - Same script works on different systems with different paths
Environment adaptation - Variables can be set based on environment (dev/staging/prod)
Parameter passing - Paths can be passed as arguments to functions
3. Readability:

Self-documenting - Variable names explain what the path represents
Clear intent - $LOG_DIR is more meaningful than /var/log/myapp
Easier debugging - Clear variable names make troubleshooting simpler
4. Error reduction:

Typos prevention - Define once, use many times
Consistency - Same path used consistently throughout script
Validation - Can validate paths once at the start

---

**4. What happens if the file does not exist?**

What happens if the file does not exist:

File test operators:

-f returns false - The condition fails, script proceeds to else branch
-d returns false - Directory check fails
No error message - Silent failure, just returns false
Command execution:

Commands fail - Any command trying to read/access the file fails
Error messages - Commands like cat, less, cp show "No such file or directory"
Non-zero exit code - Commands return exit code 1 or higher
Script continues - Unless you use set -e or check exit codes

---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 072327.png)

---

#### Screenshot 2 — Output showing `Result: Pass`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 072415.png)

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 072521.png)

---

#### Screenshot 4 — Output showing `Result: Retry`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 072608.png)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

The purpose of if-else in for loop is to execute different blocks of code based on certain conditions.

---

**2. What does `-ge` mean?**

`-ge` means greater than or equal to.

---

**3. Why should conditions be tested with different values?**

The purpose testing with different value is validate the block of code

---

**4. How can conditionals help in automation scripts?**

How conditionals help in automation scripts:

Decision making:

Branching logic - Execute different code paths based on conditions
Error handling - Check if operations succeeded before proceeding
Validation - Verify prerequisites before running tasks

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 081017.png)

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 081033.png)

---

#### Screenshot 2 — Output of `./final-automation.sh`

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 081958.png)

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 082056.png)

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function in Bash is a reusable block of code that performs a specific task and can be called multiple times throughout a script.

Key characteristics:

Code reuse - Write once, use multiple times
Modularity - Break complex scripts into smaller, manageable pieces
Named blocks - Functions have names for easy reference
Parameters - Can accept arguments like commands
Return values - Can return status codes or output

---

**2. Why are functions useful in scripts?**

Functions are useful in scripts because they help to organize code, make it more readable, and allow for code reuse. They also make it easier to debug and maintain scripts.

---

**3. Which functions did you create in this script?**

Created a print_user_details function that prints user details.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The final script combines all these elements by using variables to store user information, arrays to store multiple users, loops to iterate through the users, conditionals to check if the user exists, files to read the user information, and functions to organize the code.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/olakunleobasoro_devops-linux-bashscripting-ugcPost-7484217984589283328-D41X/?highlightedUpdateUrn=urn%3Ali%3Aactivity%3A7484217985625227264&highlightedUpdateType=SOCIAL_SHARE&origin=SOCIAL_SHARE&utm_source=share&utm_medium=member_desktop&rcm=ACoAABJp-z8BWxSilwa0aYicOVVzFmjwFjP4oPM`

---

#### Screenshot — Published LinkedIn post

![Screenshot](week-03-linux-for-devops/screenshots/assignment-5-week-3/Screenshot 2026-07-18 131121.png)

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
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