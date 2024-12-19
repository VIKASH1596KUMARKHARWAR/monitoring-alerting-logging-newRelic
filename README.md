# Monitoring, Logging, and Alerting for Host, Node.js Processes, and EC2 Instances Using New Relic

## Overview
This document outlines best practices and implementation steps for monitoring, logging, and alerting for hosts, Node.js processes, and EC2 instances using New Relic.

---

## Prerequisites
1. **New Relic Account:** Ensure you have an active New Relic account.
2. **New Relic Agent:** Install the appropriate New Relic agent (Node.js or Infrastructure) on your target systems.
3. **Access Permissions:** Ensure proper permissions for the New Relic dashboard and API access.

---

## Monitoring

### Host Monitoring
New Relic Infrastructure provides visibility into your host's performance metrics:

- **Install the Infrastructure Agent:**
  
- **Key Metrics Collected:**
  - CPU utilization
  - Memory usage
  - Disk I/O
  - Network performance

### Node.js Process Monitoring
New Relic APM (Application Performance Monitoring) helps track Node.js application performance:

1. **Install the Node.js Agent:**
   ```bash
   npm install newrelic --save
   ```
2. **Configure the Agent:**
   Add the `newrelic.js` file to your application root directory and set the New Relic license key:
   
3. **Start the Application with Monitoring:**
   ```bash
   node -r newrelic app.js
   ```
4. **Key Metrics Tracked:**
   - Request throughput
   - Response times
   - Error rates
   - Database queries

### EC2 Instance Monitoring

1. **Install the Infrastructure Agent:** Use the same steps as host monitoring.
2. **Enable Cloud Integrations:**
   - Log in to New Relic.
   - Navigate to **Infrastructure > AWS > Connect Account**.
   - Set up the IAM role and permissions for EC2 monitoring.
3. **Key Metrics Tracked:**
   - Instance status
   - Auto-scaling activities
   - CPU credits and utilization
   - Disk and network performance

---

## Logging
New Relic Logs enables centralized log collection and analysis:

1. **Enable Log Forwarding:**
   - Install the New Relic Fluent Bit or Infrastructure agent.
   - Configure the agent to forward logs to New Relic.

2. **Node.js Logging:**
   Use a logging library like `winston` or `bunyan` and configure log forwarding:
   ```javascript
   const winston = require('winston');
   const logger = winston.createLogger({
     level: 'info',
     transports: [
       new winston.transports.Console(),
       new winston.transports.File({ filename: 'combined.log' })
     ]
   });
   logger.info('Logging initialized');
   ```

3. **EC2 Instance Logs:**
   Collect system logs and application logs using CloudWatch and forward them to New Relic:
   - Install the CloudWatch Agent.
   - Configure CloudWatch to integrate with New Relic Logs.

---

## Alerting

### Setting Up Alerts
Use New Relic Alert Policies to configure notifications for thresholds and anomalies:

1. **Create an Alert Policy:**
   - Navigate to **Alerts & AI > Policies and Conditions**.
   - Create a new policy and add conditions for metrics like CPU, memory, error rate, or response time.

2. **Define Conditions:**
   - Set thresholds for warnings and critical alerts.
   - Examples:
     - CPU usage > 80% for 5 minutes.
     - Error rate > 5% for 10 minutes.

3. **Notification Channels:**
   - Add channels such as email, Slack, PagerDuty, or custom webhooks for alert delivery.

### Example Alert Configuration (Node.js):
- **Condition:** Error rate exceeds 5%.
- **Action:** Notify the development team via Slack.

### Example Alert Configuration (EC2):
- **Condition:** CPU credits drop below 20.
- **Action:** Trigger an alert on PagerDuty.

---

## Dashboards
1. **Custom Dashboards:**
   - Create custom dashboards for aggregated views of host, application, and EC2 metrics.
   - Use pre-built widgets for quick visualization.

2. **Examples:**
   - Application response time trends.
   - EC2 instance performance metrics.
   - Consolidated error rates across hosts.

---

## Best Practices
1. Use descriptive names for alert policies and dashboard widgets.
2. Regularly review and adjust thresholds for alerts.
3. Implement log rotation for application logs.
4. Use tagging for EC2 instances and applications to simplify monitoring and alerting configurations.

---

## References
- [New Relic Node.js Agent Documentation](https://docs.newrelic.com/docs/agents/nodejs-agent/)
- [New Relic Infrastructure Monitoring](https://docs.newrelic.com/docs/infrastructure/)
- [New Relic Logs](https://docs.newrelic.com/docs/logs/)
