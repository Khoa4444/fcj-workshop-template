---
title: "Event 1"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Event Participation Report: “Cloud Architect”

## 1. Event information

- **Event name:** Cloud Architect
- **Time:** 09:00 (the event date was not provided in the materials)
- **Location:** 26th Floor, Bitexco Tower, 02 Hai Trieu Street, Saigon Ward, Ho Chi Minh City
- **Role:** Attendee

## 2. Overview

The event focused on practical AWS knowledge and career direction for cloud work. Its three complementary sessions covered preparation for AWS Cloud Practitioner, service monitoring from the user-experience perspective, and automated web-application security with an AWS Security Agent.

## 3. Key content

### 3.1. Inside the Exam: AWS Cloud Practitioner

Speaker **Ngo Le Tan Huy** introduced a preparation roadmap for AWS Certified Cloud Practitioner (CLF-C02), a foundational certification that tests understanding of the AWS landscape rather than deep programming or system configuration.

The presentation covered the four exam domains—Cloud Concepts (24%), Security and Compliance (30%), Cloud Technology and Services (34%), and Billing, Pricing, and Support (12%)—as well as cloud benefits, the Well-Architected and Cloud Adoption Frameworks, the Shared Responsibility Model, IAM, global infrastructure, compute, storage, databases, networking, and EC2 pricing models.

Useful preparation practices included learning services through keywords and real use cases, analyzing incorrect practice questions, trying EC2, S3, and IAM on the Free Tier, and using elimination carefully for words such as “Not”, “Least cost”, and “Most scalable”.

### 3.2. SLA and Monitoring: What Really Matters

Speaker **Nguyen Huynh Son** explained the relationship between SLAs, risk management, and system monitoring. A healthy-looking infrastructure does not automatically mean users have a good experience: CPU, memory, and health checks can appear normal while users cannot log in because a database connection has failed.

Monitoring should therefore be organized in layers:

1. Customer journeys, such as login, purchasing, and payment.
2. Business metrics, such as successful-login rate, orders, and revenue.
3. Application metrics, such as latency, errors, and requests.
4. Infrastructure and AWS-service metrics for CPU, memory, disk, network, EC2, RDS, ALB, and S3.

The demonstration showed how to monitor failed-login metrics, define a CloudWatch Alarm threshold, and send SNS alerts so that teams can follow an incident-response process before an SLA is affected.

### 3.3. Securing Web Applications with AWS Security Agent

Speaker **Nguyen Tuan Thinh** introduced AWS Security Agent as an approach to automate web-application security across design review, source-code review, and penetration testing.

- **Design Security Review:** review Markdown documentation or Terraform against PCI DSS, NIST CSF, and AWS Well-Architected requirements.
- **Code Security Review:** integrate with GitHub/GitLab pull requests to identify vulnerabilities and secrets and suggest fixes.
- **Automated Pentesting:** perform multi-step exploitation sequences, authenticate like a real user, and provide testing evidence.

The session also identified limitations: MFA, biometrics, and mTLS can block the agent; business-logic flaws need more context; and task-hour costs can grow quickly for complex applications. Usage therefore needs monitoring, results need verification, and the tool should complement a team’s security process.

## 4. Knowledge and experience gained

- A structured view of AWS concepts, services, and effective preparation for AWS Cloud Practitioner.
- A clearer understanding of the Shared Responsibility Model: AWS secures **of** the cloud while customers secure **in** the cloud.
- The insight that monitoring must track user journeys and business metrics, not only infrastructure metrics.
- Practical understanding of connecting custom metrics, CloudWatch Alarms, and SNS for early warning.
- An understanding of the role and limitations of AI agents in design review, code review, and pentesting.

## 5. Possible applications

I can create a staged AWS learning plan and begin with Free Tier exercises. For web projects, I can add user-journey metrics such as successful-login or payment rates and configure CloudWatch and SNS alerts for risk thresholds. I can also introduce design review, secret scanning, and code review earlier in development to identify security issues before deployment.

## 6. Personal reflection

The event provided a balanced view of AWS foundations, system operations, and application security. The strongest message for me was that a system is only truly healthy when users can complete their journeys—not simply when an infrastructure dashboard looks normal. The sessions helped me see how AWS, monitoring, and security knowledge can be combined in practical work.

## 7. Participation evidence

![Cloud Architect event participation evidence](/images/4-EventParticipated/event-1-evidence.jpg)

The presentation materials are retained in the event record; this website publishes participation evidence only.
