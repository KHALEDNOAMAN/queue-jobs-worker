# Queue Jobs Worker - Advanced Usage

## Architecture
```
Producer --> Job Queue --> Worker Pool --> Result Store
              |              |
          Scheduler     Retry Logic
              |              |
        Cron Jobs      Dead Letter Queue
```

## Configuration Options
| Option | Type | Default | Description |
|--------|------|---------|-------------|
| concurrency | number | 5 | Max parallel jobs |
| maxRetries | number | 3 | Retry attempts |
| retryDelay | number | 1000 | Delay between retries (ms) |
| timeout | number | 30000 | Job timeout (ms) |
| deadLetterQueue | boolean | true | Store failed jobs |

## Job Types
```typescript
// Immediate job
await queue.add("send-email", { to: "user@example.com" });

// Delayed job
await queue.add("reminder", data, { delay: 60000 });

// Scheduled job (cron)
await queue.add("cleanup", {}, { cron: "0 0 * * *" });

// Priority job
await queue.add("urgent", data, { priority: 1 });
```

## Error Handling
- Automatic retry with exponential backoff
- Dead letter queue for permanently failed jobs
- Failure hooks for custom error handling

## Monitoring
- Job completion rate
- Average processing time
- Queue depth metrics
- Worker utilization