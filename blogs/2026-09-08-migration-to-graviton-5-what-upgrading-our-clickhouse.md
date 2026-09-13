---
title: "Migration to Graviton 5: What upgrading our ClickHouse cluster actually accomplished"
url: "https://dash0.com/blog/migration-to-graviton-5-what-upgrading-our-clickhouse-cluster-actually-accomplished"
date: "2026-09-08"
feed_url: "https://www.dash0.com/rss/posts.xml"
---
We recently upgraded one of our production ClickHouse database clusters from m8g.48xlarge instances to the newer m9g.48xlarge generation. To ensure a fair "apples-to-apples" comparison, we kept the core count, memory, and storage configuration identical. While the new servers cost 9% more per hour, the upgrade was a clear win.
