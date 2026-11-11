# Technical Interview Question Bank

These prompts are for interview practice. For every problem, clarify inputs and constraints, explain a baseline and improved approach, analyze complexity, and test edge cases. For system design, clarify requirements and scale first, then discuss APIs, data, architecture, trade-offs, reliability, and operations.

## DSA questions

### Arrays, strings, and hashing
1. Given an integer array and a target, return the indices of two values that sum to the target. Discuss the time-space trade-off between a hash map and sorting.
2. Find the length of the longest substring with no repeated characters.
3. Given daily temperatures, return how many days must pass before a warmer temperature; use an efficient approach for large inputs.
4. Merge overlapping intervals and explain how you handle touching endpoints.
5. Find the smallest missing positive integer in an unsorted array, aiming for linear time and constant extra space.
6. Given a stream of events, report the top K most frequent event types as the stream grows.

### Linked lists, stacks, and queues
7. Reverse a linked list in groups of size K; describe behavior when the final group is incomplete.
8. Detect whether a linked list contains a cycle and, if so, find the cycle's entry node.
9. Design a min-stack that supports push, pop, top, and retrieving the minimum in constant time.
10. Implement a queue using two stacks and analyze amortized operation costs.

### Trees and graphs
11. Serialize and deserialize a binary tree, including empty trees and negative values.
12. Find the lowest common ancestor of two nodes in a binary tree; then discuss how the solution changes for a BST.
13. Given course prerequisites, determine whether all courses can be completed and return a valid ordering if possible.
14. Find the shortest path in a grid with obstacles when up to K obstacles may be removed.
15. Given a weighted graph with non-negative edges, find shortest paths from one source and explain how you would reconstruct a path.
16. Maintain connected components while edges are added; explain the data structure and its limitations for edge removals.

### Dynamic programming and advanced patterns
17. Given coin denominations and a target amount, find the minimum number of coins or report that it is impossible.
18. Find the length of the longest increasing subsequence; compare the O(n²) and O(n log n) approaches.
19. Given a string and a dictionary, determine whether the string can be segmented into dictionary words.
20. Find the maximum sum of a non-empty contiguous subarray and explain how to handle all-negative input.
21. Solve the 0/1 knapsack problem and explain how the state can be compressed to one dimension.
22. Given a list of jobs with start/end times and profits, choose a compatible set with maximum total profit.

## System design questions

For each design, start by asking about users, functional requirements, traffic, data size, latency, availability, consistency, security, and cost. State assumptions when details are unspecified.

1. Design a URL-shortening service with custom aliases, expiration, redirects, and click analytics.
2. Design a social news feed for users who follow many accounts, including ranking and feed freshness.
3. Design a one-to-one and group messaging service with online delivery, offline history, and message ordering.
4. Design a globally distributed rate-limiting service with per-user and per-tenant policies.
5. Design a file storage and sharing service with resumable uploads, permissions, versioning, and downloads.
6. Design a video-on-demand platform covering upload, transcoding, playback, and adaptive bitrate delivery.
7. Design a notification platform supporting email, push, and SMS with preferences, retries, deduplication, and delivery status.
8. Design search autocomplete with low-latency suggestions, ranking, and frequently updated terms.
9. Design a ride-hailing dispatch system that matches nearby drivers and riders while handling location updates at scale.
10. Design a payment processing platform with idempotent requests, ledger correctness, reconciliation, and failure recovery.
11. Design a distributed job scheduler with delayed jobs, retries, priorities, and worker failures.
12. Design a metrics and alerting platform that ingests time-series data and evaluates user-defined alert rules.

## Behavioral and project deep-dive prompts

1. Describe a difficult technical problem you solved. What alternatives did you consider, and what was the result?
2. Tell me about a production issue or project setback. How did you diagnose it, communicate, and prevent recurrence?
3. Describe a disagreement about a technical decision and how the team reached a resolution.
4. Tell me about a time you improved reliability, performance, or developer experience. How did you measure the impact?
5. Walk through a project you built: architecture, your contribution, key trade-offs, and what you would change now.
6. Describe a time you had to learn an unfamiliar technology quickly to deliver a result.

## Self-review checklist

- Did I clarify requirements and constraints before jumping into a solution?
- Can I explain why the chosen approach works and its time/space or operational cost?
- Did I test boundary cases, failure modes, and concurrency or scale concerns where relevant?
- Did I communicate trade-offs and identify what I would improve with more time?
