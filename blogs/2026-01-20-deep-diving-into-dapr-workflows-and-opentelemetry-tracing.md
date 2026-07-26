---
title: "Deep Diving into Dapr Workflows and OpenTelemetry – Tracing the Invisible Parts of Asynchronous Communication"
url: "https://dash0.com/blog/deep-diving-into-dapr-workflows-and-opentelemetry-tracing-the-invisible-parts-of-asynchronous"
date: "2026-01-20"
feed_url: "https://www.dash0.com/rss/posts.xml"
---
Tracing asynchronous workflows is one of the hardest observability problems to solve. In this post, we dive deep into how Dapr Workflows actually execute, why distributed tracing breaks across long-lived gRPC streams, and how we fixed it using OpenTelemetry and W3C Trace Context. The result: a single, end-to-end trace that follows a request from the frontend, through workflow orchestration, all the way to activity code and outbound calls—without requiring developers to write custom tracing logic.
