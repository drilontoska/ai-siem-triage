# 🔐 AI-Assisted Incident Triage in a Splunk SIEM Environment

## Overview
Modern security operations centers (SOCs) rely heavily on SIEM platforms to collect and analyze large volumes of security data from across an organization. While these systems are effective at centralizing logs and generating alerts, they often produce a high number of security notifications that require manual review. This can lead to alert fatigue, inconsistent triage decisions, and increased time to respond, especially when security analysts must quickly interpret complex log data under time pressure. As a result, the challenge is not always detecting suspicious activity, but efficiently understanding and prioritizing alerts once they occur. 

Recent advances in artificial intelligence, particularly in large language models, present an opportunity to improve this stage of the security workflow. Rather than attempting to replace traditional detection logic, AI can be used to assist analysts by summarizing alert context, highlighting relevant evidence, and suggesting investigative next steps. When integrated carefully, AI can act as a decision-support tool that improves clarity and consistency without removing human oversight. 

The goal of this project is to explore how AI can be integrated into a SIEM environment to support incident triage. Using Splunk as the SIEM platform, I will design a virtualized lab environment that reflects a small enterprise network, including a Windows Server configured with Active Directory and domain-joined Windows endpoints. This setup allows for the generation of realistic authentication, authorization, and administrative activity commonly seen in organizational environments. Within this lab, I will implement rule-based detections using SPL and develop an AI-assisted triage component that analyzes alert evidence and produces structured summaries and recommendations. The project focuses on improving analyst understanding and response efficiency rather than creating new detection mechanisms. 

---

## Project Objectives
- Build a realistic enterprise-style SOC lab using Active Directory and domain-joined endpoints
- Generate authentic authentication and attack telemetry
- Detect suspicious behavior using rule-based SPL searches in Splunk
- Automate alert handling using workflow orchestration
- Integrate AI to assist with alert summarization and triage recommendations
- Demonstrate a modern SIEM + automation + AI workflow

---

## System Architecture
The environment simulates a small enterprise network with centralized authentication, monitoring, and response capabilities.

**Architecture Flow:**

      Kali Linux (Attacker)

                ↓

    Windows Domain (AD + Endpoints)

                ↓

    Splunk SIEM (Detection & Alerts)

                ↓

      n8n Automation Workflow

                ↓

        AI-Assisted Analysis

                ↓

        Slack Alert Output


Each component serves a distinct SOC function, mirroring how modern security teams operate in production environments.

---

## Lab Environment
- **Windows Server 2022**
  - Active Directory Domain Controller
  - DNS services
  - Splunk Enterprise SIEM
- **Windows 10 Pro (2x)**
  - Domain-joined endpoints
  - User authentication and system activity generation
- **Ubuntu Server**
  - Hosts the n8n workflow automation platform
  - Acts as the automation and integration layer between Splunk and AI analysis
  - Processes alert data and forwards structured summaries to downstream notification services
- **Kali Linux**
  - Adversarial simulation and attack execution
- **Networking**
  - Internal network for inter-VM communication
  - NAT adapter for controlled internet access

This setup enables the generation of realistic enterprise authentication, authorization, and attack telemetry.

---

## Detection Engineering (Splunk SPL)
Splunk Processing Language (SPL) is used to detect suspicious behaviors within collected logs, including:
- Repeated failed authentication attempts
- Brute-force login patterns
- Time-based correlation of authentication failures

Alerts are configured to trigger automatically when defined thresholds are met, forming the foundation for downstream automation and AI-assisted analysis.

---

## Attack Simulation
To generate realistic security events, controlled adversarial activity is performed from the Kali Linux system:
- SSH services are intentionally exposed
- Brute-force authentication attempts are executed using common attack tools
- High-volume failed login events are generated and ingested into Splunk

These attacks create meaningful detection data without impacting real systems.

---

## AI-Assisted Incident Triage
The core contribution of this project is the **AI-assisted triage workflow**.

Instead of replacing detection logic, AI is used to:
- Analyze alert metadata and correlated log evidence
- Summarize what occurred in plain language
- Highlight key indicators (host, user, source IP, frequency)
- Assess potential severity
- Recommend logical investigative next steps for analysts

This approach reduces cognitive load, improves consistency across alerts, and accelerates analyst understanding during triage.

---

## Automation Workflow
Automation is implemented using **n8n**, acting as the orchestration layer between Splunk and AI analysis:
1. Splunk alert triggers on suspicious activity
2. Alert metadata is forwarded to n8n
3. AI analyzes the alert context
4. A structured summary and recommendations are generated
5. The final alert is delivered to Slack

This demonstrates how SIEM, automation, and AI can work together in a modern SOC.

---

## Results & Observations
- Alert context is significantly clearer when summarized by AI
- Analysts receive actionable insights rather than raw logs
- The workflow demonstrates reduced triage time and improved consistency
- Human oversight remains essential for validation and response decisions

---

## Limitations & Future Work
- The lab environment is small-scale and not production-sized
- AI does not directly access raw logs—only alert evidence
- No claims are made regarding real-world accuracy or detection rates

Future improvements could include:
- SOAR-style response actions
- Expanded detection coverage
- Integration with additional alerting platforms

---

## Conclusion
This project demonstrates how **AI-assisted incident triage** can enhance SOC workflows by improving alert clarity and analyst decision-making without replacing existing SIEM detection mechanisms. The integration of Splunk, automation, and AI reflects modern defensive security practices and highlights the potential for AI as a practical decision-support tool in cybersecurity operations.
