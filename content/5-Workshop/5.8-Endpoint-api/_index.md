---
title: "Endpoint and scoring API"
date: 2026-07-29
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

Deploy the endpoint only for a short demo window, wait for InService, then deploy the Lambda/HTTP API. Call the new API URL with safe and risky trajectories. The risky payload must return `block` because the destructive-command rule overrides model score. Historical URLs are invalid after cleanup.

