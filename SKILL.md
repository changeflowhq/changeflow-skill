---
name: changeflow
description: "Monitor any website and get AI-enriched change intelligence. Use when the user wants to track web pages, create monitoring sources, search their changes, or manage their Changeflow account. Requires CHANGEFLOW_API_TOKEN env var."
allowed-tools: WebFetch, Bash(curl *), Read
disable-model-invocation: true
---

# Changeflow - Web Intelligence

Monitor any website. Get AI-enriched change briefings. Manage sources, search changes, and automate web monitoring.

## Setup

Requires a Changeflow API token. Get one from https://changeflow.com/account/api

Set the environment variable:
```bash
export CHANGEFLOW_API_TOKEN=your_token_here
```

## API Endpoint

```
POST https://changeflow.com/mcp
Content-Type: application/json
Accept: application/json
Authorization: Bearer $CHANGEFLOW_API_TOKEN
```

All requests use JSON-RPC 2.0 format. Include the Bearer token in every request.

## Tools

### list_sources

List all monitored sources.

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "list_sources",
    "arguments": { "tag": "compliance" }
  }
}
```

**Arguments:** `tag` (optional filter), `limit`

### get_source

Get details for a specific source.

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_source",
    "arguments": { "source_id": "ABC123" }
  }
}
```

**Arguments:** `source_id` (required - the share code)

### get_changes

Search recent changes across all sources.

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_changes",
    "arguments": { "query": "pricing update", "limit": 10 }
  }
}
```

**Arguments:** `query`, `since` (ISO date), `type` (link or change), `tag`, `source_id`, `limit`

### get_change

Get full details of a single change.

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_change",
    "arguments": { "change_id": "v_456" }
  }
}
```

**Arguments:** `change_id` (required - format v_123 for page changes, l_456 for link discoveries)

### create_source

Create a new source to monitor.

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "create_source",
    "arguments": {
      "url": "https://www.fda.gov/regulatory-information/search-fda-guidance-documents",
      "looking_for": "New FDA guidance documents on drug manufacturing",
      "frequency": "daily"
    }
  }
}
```

**Arguments:** `url` (required), `looking_for`, `frequency`, `tags`

### check_source

Trigger an immediate check on a source.

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "check_source",
    "arguments": { "source_id": "ABC123" }
  }
}
```

### pause_source / resume_source

Pause or resume monitoring.

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "pause_source",
    "arguments": { "source_id": "ABC123" }
  }
}
```

## How to Call

Use WebFetch or curl with the Bearer token:

```
WebFetch POST https://changeflow.com/mcp
Headers: Authorization: Bearer $CHANGEFLOW_API_TOKEN
Body: {"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_sources","arguments":{}}}
```

Parse `result.content[0].text` as JSON from the response.

## Presenting Results

1. **Sources** - show title, URL, status (running/paused/error), last change date
2. **Changes** - show AI summary, date, source name. For link discoveries, show the new URL found.
3. **Creating sources** - confirm the URL and prompt, tell the user their first check will run within the hour
4. **Errors** - if auth fails, tell user to check their CHANGEFLOW_API_TOKEN

## Links

- [Changeflow](https://changeflow.com) - Enterprise web intelligence
- [API Settings](https://changeflow.com/account/api) - Get your API token
- [Pricing](https://changeflow.com/pricing) - Plans from $99/mo
- [GovPing](https://govping.org) - Free regulatory intelligence (powered by Changeflow)
