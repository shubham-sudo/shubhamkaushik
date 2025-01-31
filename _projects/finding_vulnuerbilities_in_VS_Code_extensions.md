---
layout: page
title: Finding Vulnerabilities
description: Finding Vulnerabilities in VS Code Extensions
img: assets/img/cyber.png
importance: 2
category: Academics
giscus_comments: true
---

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/cyber.png" title="cyber" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/path-traversal.png" title="path traversal" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

VS Code is a widely used text editor with numerous extensions that enhance its functionality. However, these extensions can introduce security risks if not properly vetted. This project aims to analyze VS Code extensions for security vulnerabilities, specifically **Remote Code Execution (RCE)** and **Command Injection**, and develop an automated tool to identify these threats.  

## **Motivation**  
With millions of developers relying on VS Code, extensions become an attractive target for cyberattacks. A single compromised extension could allow attackers to execute arbitrary code or inject malicious commands, leading to system breaches or data theft. Since VS Code extensions often run with the same privileges as the user, even a seemingly harmless plugin can pose a critical security risk.  

## **Overview**  
This research focused on extensions that execute shell commands or interact with the system’s terminal, making them potential candidates for **RCE** and **Command Injection** vulnerabilities. The selected extensions were analyzed for unsafe command execution practices.  

I built an **automated tool** using **Python, pyautogui, and subprocess**, which:  
1. **Searches & Downloads Extensions** – Uses VS Code’s CLI to fetch and install extensions.  
2. **Analyzes Command Execution** – Extracts `package.json` to identify exposed commands and scripts.  
3. **Executes & Monitors** – Runs extension commands while monitoring system behavior.  
4. **Flags Vulnerable Extensions** – Logs extensions that execute arbitrary commands unsafely.  

## **Challenges & Solutions**  
- **Identifying Risky Extensions** – Filtering through 1K extensions required refining search queries.  
- **Automation Hurdles** – Extensions behave differently based on configurations, so we incorporated **sandboxing** to safely execute and observe their behavior.  
- **Rate Limits** – Bypassed API restrictions using **asynchronous requests** for efficiency.  

## **Results**  
We tested **150 extensions** for security vulnerabilities:  
- **RCE Vulnerabilities Found in 5 Extensions**  
- **Command Injection Found in 3 Extensions**  

## **Conclusion**  
Our tool successfully identified security risks in popular VS Code extensions. This highlights the **urgent need for better security vetting in the VS Code ecosystem**. Future improvements could focus on deeper static analysis and behavior monitoring.  

---

#### For more details, check out:
- 📄 [Read Report](https://shubhamkaushik.com/assets/pdf/vulnerabilities_in_vs_code.pdf)
- 🐙 [GitHub Repository](https://github.com/prateekdceit06/EC521)
