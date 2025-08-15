# Mock Service Requirements

This document outlines the requirements for a mock service that simulates a ServiceNow instance for the MCP server to connect to.

## General Requirements

- The mock service MUST simulate the ServiceNow Table API.
- The base URL for all table-related endpoints MUST be `/api/now/table`.
- The service MUST handle JSON request and response bodies.
- The service SHOULD support common ServiceNow query parameters such as `sysparm_limit`, `sysparm_offset`, and `sysparm_query` to allow for filtering and pagination.

## Supported Tables

The mock service shall provide endpoints for the following tables:

- `change_request`
- `incident`
- `item_option_new`
- `kb_knowledge`
- `pm_project`
- `question_answer`
- `rm_epic`
- `rm_scrum_task`
- `rm_story`
- `sc_catalog`
- `sc_category`
- `sc_cat_item`
- `sc_cat_item_category`
- `sc_item_option`
- `sc_item_option_mtom`
- `sc_request`
- `sc_req_item`
- `sys_remote_update_set`
- `sys_script_include`
- `sys_update_xml`
- `sys_user`
- `wf_workflow`
- `wf_workflow_version`

## Endpoint Specifications

For each table listed above, the following endpoints must be supported:

- `GET /api/now/table/{table_name}`: Returns a list of records from the corresponding JSON file in the `mock_server` directory.
- `GET /api/now/table/{table_name}/{sys_id}`: Returns a single record identified by `{sys_id}` from the corresponding JSON file.
- `POST /api/now/table/{table_name}`: Accepts a JSON payload for a new record and returns a successful response. The data does not need to be persisted.
- `PATCH /api/now/table/{table_name}/{sys_id}`: Accepts a JSON payload to update a record and returns a successful response. The underlying data does not need to be changed.
- `DELETE /api/now/table/{table_name}/{sys_id}`: Deletes a record identified by `{sys_id}` and returns a successful response. The underlying data does not need to be deleted.
