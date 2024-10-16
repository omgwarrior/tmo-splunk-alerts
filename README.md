# Splunk HTTP 400 Response Ratio Monitor

This repository contains the configuration files for a Splunk dashboard and alert to monitor the ratio of HTTP 400 responses within a 24-hour period. If the ratio exceeds **10:20 (50%)**, an alert is triggered and notifications are sent via email or Microsoft Teams.

## Files Included
- **dashboard.json**: Configuration for the Splunk dashboard that visualizes the ratio of HTTP 400 responses.
- **alert_config.json**: Configuration for the Splunk alert that sends notifications based on the defined ratio.

## Setup Instructions

### Prerequisites
- A Splunk Enterprise or Splunk Cloud instance.
- Access to an index and sourcetype with HTTP status codes.
- A Microsoft Teams webhook URL (if using Teams for notifications).

### Dashboard Setup
1. In **Splunk Web**, go to **Dashboards**.
2. Click **Create New Dashboard**.
3. Select **Import JSON** and upload the `dashboard.json` file.

### Alert Setup
1. Open the **Search & Reporting** app and paste the query from `alert_config.json`.
2. Save the search as an **Alert** with the following settings:
   - **Time Range**: Last 24 hours.
   - **Trigger Condition**: When the ratio is greater than or equal to 50%.
   - **Actions**: Configure Email or Webhook notifications.

### For Microsoft Teams Notifications
1. Go to your Teams channel.
2. Click **More Options** (three dots) → **Connectors** → **Incoming Webhook**.
3. Generate a webhook URL and use it in the alert action.

### Example Teams Webhook Payload
```json
{
  "text": "HTTP 400 Ratio Alert: {{ratio}}% over the past 24 hours."
}
