# AI-Assisted Incident Triage in a Splunk SIEM Environment

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
- Brute-force authentication attempts are executed using common attack tools such as Hydra
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

This project shows how AI-assisted incident triage can improve the way Security Operations Centers handle alerts by making them easier to understand and act on, without trying to replace traditional SIEM detection logic. While SIEM platforms like Splunk are very effective at collecting logs and triggering alerts, the triage process itself is often where analysts struggle the most. Reviewing large volumes of alerts, interpreting raw log data, and deciding what matters under time pressure can quickly become overwhelming. This project focuses on that exact problem and explores how AI can be used as a practical support tool during triage rather than as a replacement for existing security controls.

By building a realistic enterprise-style lab environment with Active Directory, domain-joined endpoints, and simulated adversarial activity, the project generates meaningful authentication and attack telemetry similar to what would be seen in a real organization. Rule-based detections were intentionally used to keep alert logic transparent and understandable, while AI was introduced only after an alert had already been generated. This design choice reinforces analyst trust and ensures that AI is used to enhance context and understanding, not to make hidden or automated security decisions.

The AI-assisted triage component takes alert evidence and turns it into clear, structured summaries that explain what happened, why it may matter, and what an analyst should look at next. Instead of forcing analysts to manually piece together log entries, the system highlights key details such as affected users, hosts, source activity, and patterns over time. This reduces cognitive load during triage and helps create more consistent interpretations of alerts, especially in scenarios involving high alert volume or repetitive attack patterns.

Automation plays an important role in tying the entire workflow together. By connecting Splunk alerts to automated workflows and AI analysis, the project demonstrates how security teams can reduce manual steps while still keeping humans in control of decision-making and response. Alerts are enriched and delivered in a way that is immediately usable, showing how automation and AI can complement existing SOC processes rather than complicate them.

Although this project was built in a controlled lab environment and is not intended to represent a production deployment, the ideas behind it are directly applicable to real-world security operations. Future improvements could include expanding detections, adding response actions similar to SOAR platforms, and refining how AI analyzes and presents context. As security environments continue to grow in complexity and alert volume, approaches like this can help analysts stay focused on what matters most.

Overall, this project demonstrates that AI can be a useful and realistic addition to security operations when it is applied thoughtfully. Instead of replacing analysts, AI acts as a force multiplier that helps them work more efficiently, make better-informed decisions, and spend less time digging through raw logs. The project highlights how combining SIEM, automation, and AI can lead to clearer, more effective incident triage while keeping human expertise at the center of the process.
