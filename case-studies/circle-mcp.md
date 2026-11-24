# Circle MCP: an AI interface for community operations

**Status:** implemented server with public documentation. The public repository does not contain the server implementation.

[Public documentation](https://github.com/iamnortey/circle-mcp) · [Portfolio](../README.md)

## The problem and work

A community operator needs to understand spaces, posts, members and unanswered questions before deciding what to do. I built a 16-tool interface that connects an AI assistant to those tasks, including community-health summaries and content operations.

The implementation includes read and diagnostic tools, plus post creation, updates and comments. A dated development validation record reports 95 passing offline tests. This is historical evidence, not a fresh test run or a claim that every API operation works in every community.

## A lesson in careful integration

Reads and writes need different treatment. The implementation can publish posts, and a draft must be requested explicitly. Comment creation also has a documented Circle API permission limitation. These details matter when teaching someone to operate a connected assistant.

## Small-business relevance

The integration demonstrates a pattern for connecting AI to an existing business system: retrieve useful information, explain what it means, and make actions explicit. An educator or community business could use the information to prioritize questions and maintain content.

No measured time savings or public installation experience is claimed here.
