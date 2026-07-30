---
title: "Event 2"
date: 2026-07-25
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Event Participation Report: “First Cloud AI Journey × Agentic AI Build Week”

## 1. Event information

- **Event name:** First Cloud AI Journey × Agentic AI Build Week (FCAJ × AABW)
- **Date:** 25 July 2026
- **Location:** 26th Floor, Bitexco Tower, 02 Hai Trieu Street, Saigon Ward, Ho Chi Minh City
- **Role:** Attendee

## 2. Overview

FCAJ × AABW focused on building products with AWS and Agentic AI. Teams described how they turned real problems into short-cycle prototypes: defining the problem, designing the architecture, integrating AI agents, balancing cost, presenting a demo, and learning from the build process.

The event was strongly practical. Instead of only introducing technology, speakers described their product-building process, technical decisions, team challenges, and lessons from hackathon work.

## 3. Key content

### 3.1. Hackathon Journey – S.H.E.P.H.E.R.D.

Team **3KA** shared its 24-hour hackathon journey. Its project, **S.H.E.P.H.E.R.D.** (Smart Human-flow Evaluation, Prediction, Hazard Detection, Response, and Dispatch), supports crowded-space operations by analyzing camera feeds, detecting and tracking people, measuring density and queues, identifying congestion risk, and recommending early action.

The architecture used YOLO and ByteTrack for computer vision, Amazon SageMaker for inference, Amazon Bedrock AgentCore with Strands for the agentic layer, and a React dashboard. A monitoring agent reads indicators continuously, predicts overload, and issues proactive alerts. An Operator Copilot lets staff ask natural-language questions using real-time data.

The team highlighted challenges in stable video streaming, inference latency, object tracking between frames, camera placement, cost control, and scope management. Its main lessons were to define completion criteria, prepare tools and accounts early, assign roles from the start, and rehearse a concise demo story.

### 3.2. One Team – KFC Bot Agent

**One Team** presented KFC Bot Agent, a multichannel conversational ordering agent. It aims to let users order directly through channels such as Zalo and WhatsApp rather than switching applications, creating new accounts, or repeating needs to support staff.

The agent understands intent, plans steps, queries trusted business data, updates the cart and promotions, and confirms against the real cart state. Its “design once, deploy everywhere” approach adds channels through adapters, business functions through connectors, and capabilities through tools. The team discussed a target infrastructure cost of about USD 88 per month for 500 orders per day and 3–5 seconds end-to-end latency.

### 3.3. SA Professional AI Native App

This application supports Solution Architects who need to process system-design requests quickly. It can analyze natural-language and structured requirements, propose architecture options including hybrid-cloud and company standards, create editable Draw.io/AWS diagrams, estimate indicative costs for ap-southeast-1, identify assumptions and gaps, and support refinement through chat.

Its value is to shorten the process from reading BRD/PRD documents and starting from a blank page to producing a Requirements Catalogue, an initial architecture for discussion, automated IaC, and AWS cost estimates.

### 3.4. Signal Scout

Signal Scout is an AI platform for monitoring strategic business changes. It connects scattered enterprise signals, gathers and verifies evidence, analyzes indicators, and develops scenarios for strategy, risk, competitive-intelligence, and enterprise-account teams.

The system uses Bedrock, AgentCore, WAF, Amplify, CloudWatch, DynamoDB, Lambda, S3, API Gateway, and Cognito; Apify/TinyFish for collection; and Langfuse for AI observability. Estimated monthly cost ranges were about USD 81, USD 94, and USD 359 depending on load and external services, demonstrating why architecture and budget must be considered from the MVP stage.

## 4. Knowledge and experience gained

- A practical process for taking an AI idea from a real problem to a demonstrable MVP.
- The insight that agentic AI is effective when connected to trusted data, tools, and explicit verification steps.
- Examples of combining computer vision, AI agents, dashboards, and cloud inference for real-time monitoring.
- A better understanding of architectures that can expand by channel, business function, and capability.
- New perspectives on automating Solution Architect work, from requirement extraction to diagrams, IaC, and cost estimation.
- The importance of evidence, observability, cost control, and human-in-the-loop review in enterprise AI.

## 5. Possible applications

I can apply the hackathon mindset to personal projects by choosing a small problem, defining an MVP, and prioritizing one core feature. When building chatbots or AI agents, I will design action flows verified against business data rather than relying only on model responses. For AWS projects, I will consider cost, latency, observability, and scale early, and use AI tools to accelerate requirement reading, architecture drafting, and technical documentation.

## 6. Personal reflection

The event offered relatable examples of AWS and Agentic AI solving specific problems: crowd coordination, multichannel ordering, Solution Architect support, and business-signal monitoring. I was impressed by the teams’ willingness to experiment and share their challenges. It reinforced that valuable AI products need not only a good model, but also the right problem, trusted data and tools, a suitable architecture, and a clear demo for users.

## 7. Participation evidence

![FCAJ × AABW event participation evidence](/images/4-EventParticipated/event-2-evidence.jpg)

The presentation materials are retained in the event record; this website publishes participation evidence only.
