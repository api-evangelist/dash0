---
title: "Observing Traefik with OpenTelemetry and Dash0"
url: "https://dash0.com/blog/observing-traefik-with-opentelemetry-and-dash0"
date: "2025-09-29"
feed_url: "https://www.dash0.com/rss/posts.xml"
---
Ingress controllers are the gatekeepers of Kubernetes, handling TLS termination, routing, and middleware at the edge of your cluster. That makes them a prime vantage point for observability, but also a tricky one to instrument. In this post, we dive into Traefik’s OpenTelemetry support - from native tracing and semantic HTTP metrics to experimental OTLP log export - and show how to bring it all together with the OpenTelemetry Collector and Dash0.
