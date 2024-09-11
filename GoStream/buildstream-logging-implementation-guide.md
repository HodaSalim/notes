# Implementing Elasticsearch Logging Infrastructure for BuildStream

## 1. Setup and Configuration

### 1.1 Docker Compose Configuration

Add the following services to your `docker-compose.yml`:

```yaml
version: '3'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.10.0
    environment:
      - discovery.type=single-node
    ports:
      - "9200:9200"
    volumes:
      - elasticsearch-data:/usr/share/elasticsearch/data

  logstash:
    image: docker.elastic.co/logstash/logstash:7.10.0
    volumes:
      - ./logstash/pipeline:/usr/share/logstash/pipeline
    ports:
      - "5000:5000"
    depends_on:
      - elasticsearch

  kibana:
    image: docker.elastic.co/kibana/kibana:7.10.0
    ports:
      - "5601:5601"
    depends_on:
      - elasticsearch

volumes:
  elasticsearch-data:
```

### 1.2 Logstash Configuration

Create a file `logstash/pipeline/logstash.conf`:

```
input {
  tcp {
    port => 5000
    codec => json
  }
}

filter {
  if [service] == "user-service" {
    mutate { add_field => { "[@metadata][index]" => "buildstream-user-service-%{+YYYY.MM.dd}" } }
  } else if [service] == "streaming-service" {
    mutate { add_field => { "[@metadata][index]" => "buildstream-streaming-service-%{+YYYY.MM.dd}" } }
  } else {
    mutate { add_field => { "[@metadata][index]" => "buildstream-general-%{+YYYY.MM.dd}" } }
  }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "%{[@metadata][index]}"
  }
}
```

## 2. Implementing Logging in Go Services

### 2.1 Install Required Packages

```bash
go get gopkg.in/sohlich/elogrus.v7
go get github.com/sirupsen/logrus
```

### 2.2 Configure Logging in Each Service

```go
package main

import (
    "os"
    "gopkg.in/sohlich/elogrus.v7"
    "github.com/sirupsen/logrus"
    "github.com/olivere/elastic/v7"
)

func setupLogging() (*logrus.Logger, error) {
    log := logrus.New()
    log.SetFormatter(&logrus.JSONFormatter{})
    
    client, err := elastic.NewClient(elastic.SetURL("http://elasticsearch:9200"), elastic.SetSniff(false))
    if err != nil {
        return nil, err
    }
    
    hook, err := elogrus.NewElasticHook(client, "localhost", logrus.DebugLevel, "buildstream-user-service")
    if err != nil {
        return nil, err
    }
    
    log.Hooks.Add(hook)
    return log, nil
}

func main() {
    log, err := setupLogging()
    if err != nil {
        log.Fatal("Failed to set up logging: ", err)
    }
    
    // Use the logger
    log.WithFields(logrus.Fields{
        "service": "user-service",
        "method": "CreateUser",
    }).Info("Creating new user")
    
    // ... rest of your application code
}
```

## 3. Using Kibana for Log Analysis

### 3.1 Setting Up Index Patterns

1. Open Kibana (http://localhost:5601)
2. Go to Management > Stack Management > Index Patterns
3. Create index patterns for your logs (e.g., `buildstream-*`)

### 3.2 Creating Dashboards

1. Go to Dashboard
2. Click "Create dashboard"
3. Add visualizations based on your log data

Example visualizations:
- Line chart of error rates over time
- Pie chart of log levels distribution
- Data table of recent error messages

## 4. Best Practices for Effective Logging

### 4.1 Consistent Log Levels

- DEBUG: Detailed information for debugging
- INFO: General information about system operation
- WARN: Warning events that might lead to an error
- ERROR: Error events that might still allow the application to continue running
- FATAL: Very severe error events that will lead the application to abort

### 4.2 Structured Logging

Use fields to add context to your logs:

```go
log.WithFields(logrus.Fields{
    "user_id": user.ID,
    "action": "login",
    "status": "success",
}).Info("User logged in")
```

### 4.3 Avoid Logging Sensitive Information

Be cautious about logging personally identifiable information (PII) or secrets.

### 4.4 Use Correlation IDs

Implement correlation IDs to track requests across services:

```go
log.WithFields(logrus.Fields{
    "correlation_id": ctx.Value("correlation_id"),
    "service": "streaming-service",
    "method": "StartStream",
}).Info("Starting new stream")
```

## 5. Monitoring and Alerting

### 5.1 Set Up Alerting in Kibana

1. Go to Management > Stack Management > Alerting
2. Create alerts based on log patterns or thresholds

Example alert: Notify when error rate exceeds 5% in the last 5 minutes

### 5.2 Implement Health Checks

Create a health check endpoint in each service that reports its status to Elasticsearch.

## 6. Troubleshooting with Logs

### 6.1 Using Kibana for Troubleshooting

1. Use the Discover tab to search for specific error messages
2. Use the timeline to correlate events across services
3. Create saved searches for common issues

### 6.2 Log Analysis Techniques

- Use Kibana's query language to filter logs
- Analyze log trends over time to identify recurring issues
- Correlate logs from different services to trace request flows

## 7. Performance Optimization

Use logging data to identify performance bottlenecks:

1. Create visualizations for response times
2. Monitor resource usage (CPU, memory) through logs
3. Identify slow database queries or API calls

By implementing and effectively using this logging infrastructure, you'll gain valuable insights into your BuildStream application, enabling faster troubleshooting, better performance optimization, and improved overall system reliability.
