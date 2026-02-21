
name: lambda-event-generator
description: Skill to generate test events for AWS Lambda functions using the `sam local generate-event <resource> <event>` command. Quickly creates example files in /events/ to simulate invocations from AWS services (API Gateway, S3, DynamoDB, etc.) and facilitate local testing.

---

# Lambda Event Generator Skill

## Context
Use this skill to generate realistic event payloads for Lambda testing, leveraging the AWS SAM CLI. Supports common AWS resources and event types. If a resource/event is not supported, generate the closest event and manually edit the JSON as needed.

## Usage
- Specify the AWS resource and event type you want to simulate (e.g., `s3 put`, `apigateway aws-proxy`, `dynamodb update`).
- The agent will generate the appropriate `sam local generate-event` command and create the event file in `/events/`.
- If the event is not natively supported, the agent will provide a template and instructions for manual editing.

## Example Prompt
```
Generate a put event for S3 using sam local generate-event.
```

## Example Response
Command:
```bash
sam local generate-event s3 put > events/s3-put.json
```
File generated: `events/s3-put.json`

## Best Practices
- Check supported resources/events with `sam local generate-event --help`.
- Use descriptive filenames for event files (e.g., `s3-put.json`, `apigateway-proxy.json`).
- Integrate generated events into automated and manual tests.
- If the event is not supported, edit the JSON manually to match your use case.
- Document customizations for future reference.

## Advanced Usage
- For complex events (e.g., scheduled events, EventBridge), start from a similar event and adjust fields as needed.
- Validate event structure against Lambda handler requirements.