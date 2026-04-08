---
title: SQS
tags:
  - aws
  - infra
---
- Durable message queue
- Pull one at a time
- Retention: 14 days
- Used to combine with SNS topic (pub/sub broadcast channel that push/fan-out messages)

config properties
- `visibility_timeout_seconds` = vis. before message fades out
- `message_retention_seconds` 
- `receive_wait_time_seconds`
- `redrive_policy`
	- `deadLetterTargetArn`
	- `maxReceiveCount` : after 3 failures -> DLQ

queue types
- standard vs FIFO

| criteria      | standard        | FIFO                    |
| ------------- | --------------- | ----------------------- |
| throughput    | unlimited       | 300 msg/s               |
| ordering      | best-effort     | strict (fifo duh uh)    |
| delivery      | at least 1      | exactly 1               |
| deduplication | handle manually | built-in (5 min window) |
| cost          | cheaper         | 10x more expen          |

**best practice**
- if ordering matters (which is true for most business use-cases), use FIFO queue
- visibility timeout (`visibility_timeout_seconds)
	- Time consumer process + delete message before SQS assumes failure/redeliver
	- visibility_timeout > p99 processing time (3x buffer)
