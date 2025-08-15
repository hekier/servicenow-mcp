# Mock Service Architecture

This document describes the proposed architecture for the ServiceNow mock service.

## Technology Stack

- **Language**: Python
- **Framework**: FastAPI

FastAPI is chosen for its high performance, ease of use, and automatic generation of interactive API documentation.

## Architecture Overview

The mock service will be a single FastAPI application. It will read data from the JSON files located in the `/mock_server` directory to populate its responses.

### Directory Structure

The mock server will be implemented in a new `main.py` file inside the `/mock_server` directory:

```
/mock_server/
├── main.py
├── requirements.md
├── architecture.md
├── servicenow_endpoints.md
├── catalog/
│   └── sc_cat_item.json
└── ... (other data folders)
```

### API Endpoints

The FastAPI application will implement the following dynamic routes to handle all supported tables:

- `GET /api/now/table/{table_name}`
- `GET /api/now/table/{table_name}/{sys_id}`
- `POST /api/now/table/{table_name}`
- `PATCH /api/now/table/{table_name}/{sys_id}`
- `DELETE /api/now/table/{table_name}/{sys_id}`

A path parameter `{table_name}` will be used to determine which JSON file to access.

### Data Handling

- On startup, the service can load all JSON files from the `/mock_server` directory into memory to provide faster responses.
- For `GET` requests, the service will filter the data based on the provided query parameters (`sysparm_limit`, `sysparm_offset`, `sysparm_query`) and return the appropriate JSON response.
- For `POST`, `PATCH`, and `DELETE` requests, the service will perform no modifications to the in-memory data. It will simply return a pre-defined successful response to simulate the behavior of the actual ServiceNow API.

This architecture ensures that the mock service is lightweight, fast, and easy to maintain while providing a realistic simulation of the ServiceNow API for the MCP server.
