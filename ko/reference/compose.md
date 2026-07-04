# Model-Compose Configuration Reference

This reference guide provides comprehensive documentation for all configuration options in model-compose. Use this as your authoritative source for YAML configuration syntax, available options, and usage patterns.

## Quick Navigation

### Core Configuration
- [Controller](/model-compose/ko/reference/compose/controller.md) - HTTP and MCP server configuration
- [Workflow](/model-compose/ko/reference/compose/workflow.md) - Job orchestration and execution logic
- [Component](/model-compose/ko/reference/compose/component.md) - Reusable service definitions and common properties

### Infrastructure & Services
- [System](/model-compose/ko/reference/compose/system.md) - Infrastructure service management (Docker Compose)
- [Listener](/model-compose/ko/reference/compose/listener.md) - Webhook and callback handling
- [Gateway](/model-compose/ko/reference/compose/gateway.md) - Tunneling and external access
- [Tracer](/model-compose/ko/reference/compose/tracer.md) - Tracing configuration and observability
- [Logger](/model-compose/ko/reference/compose/logger.md) - Logging configuration and output management

### Reference
- [Language Codes](/model-compose/ko/reference/compose/language-codes.md) - Standardized language codes for multilingual components

### Components
- [HTTP Client](/model-compose/ko/reference/compose/components/http-client.md) - External API integration
- [HTTP Server](/model-compose/ko/reference/compose/components/http-server.md) - Web server hosting
- [MCP Client](/model-compose/ko/reference/compose/components/mcp-client.md) - Model Context Protocol client
- [MCP Server](/model-compose/ko/reference/compose/components/mcp-server.md) - Model Context Protocol server
- [Model](/model-compose/ko/reference/compose/components/model.md) - AI/ML model inference
- [Vector Store](/model-compose/ko/reference/compose/components/vector-store.md) - Vector database operations
- [Key-Value Store](/model-compose/ko/reference/compose/components/key-value-store.md) - Key-value data storage
- [Shell](/model-compose/ko/reference/compose/components/shell.md) - System command execution
- [Text Splitter](/model-compose/ko/reference/compose/components/text-splitter.md) - Document processing
- [Workflow](/model-compose/ko/reference/compose/components/workflow.md) - Nested workflow execution

## Configuration Structure Overview

A complete model-compose.yml file typically includes these top-level sections:

```yaml
# Server configuration
controller:
  type: http-server | mcp-server
  # ... controller settings

# Workflow definitions
workflow:  # or workflows: for multiple
  # ... workflow configuration

# Component definitions
component:  # or components: for multiple
  # ... component configuration

# Infrastructure services (optional)
system:     # or systems: for multiple
  # ... system configuration (e.g., docker-compose)

listener:   # or listeners: for multiple
  # ... listener configuration

gateway:    # or gateways: for multiple
  # ... gateway configuration

tracer:     # or tracers: for multiple
  # ... tracing configuration

logger:     # or loggers: for multiple
  # ... logging configuration
```

## Configuration Patterns

### Single vs Multiple Definitions

Most configuration sections support both singular and plural forms:

```yaml
# Single definition
controller:
  type: http-server
  port: 8080

# Multiple definitions  
components:
  - id: api-client
    type: http-client
  - id: local-model
    type: model
```

### Variable Interpolation

All configuration sections support dynamic values through variable interpolation:

- **Environment Variables**: `${env.API_KEY}`
- **Input Data**: `${input.field}`  
- **Job Results**: `${job-name.output}`
- **Type Conversion**: `${input.count as number}`
- **Default Values**: `${input.optional | default}`

### Common Properties

Many configuration objects share common properties:

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `id` | string | varies | Unique identifier |
| `type` | string | required | Configuration type |
| `runtime` | string | `embedded` | Runtime environment (`embedded` or `docker`) |
| `max_concurrent_count` | integer | varies | Maximum concurrent operations |

## Getting Started

1. **Choose Your Controller**: Start with [Controller](/model-compose/ko/reference/compose/controller.md) to set up your server
2. **Define Your Workflow**: Use [Workflow](/model-compose/ko/reference/compose/workflow.md) to orchestrate your logic
3. **Add Components**: Select from [Component](/model-compose/ko/reference/compose/component.md) types for your functionality
4. **Configure Infrastructure**: Add [Listener](/model-compose/ko/reference/compose/listener.md), [Gateway](/model-compose/ko/reference/compose/gateway.md), [Tracer](/model-compose/ko/reference/compose/tracer.md), or [Logger](/model-compose/ko/reference/compose/logger.md) as needed

## Examples Directory

For working examples of these configurations, see the `examples/` directory in the repository:

- `examples/providers/openai/openai-chat-completions/` - Simple HTTP client workflow
- `examples/make-inspiring-quote-voice/` - Multi-step workflow with dependencies
- `examples/model-tasks/` - Various local model configurations
- `examples/vector-store/` - Vector database usage patterns
- `examples/key-value-store/` - Key-value store usage patterns
- `examples/mcp-servers/` - MCP server implementations

## Configuration Validation

Model-compose validates all configuration at startup. Common validation errors include:

- **Missing required fields**: Ensure all required properties are specified
- **Invalid types**: Check data types match expected values (string, integer, boolean)
- **Invalid references**: Verify component IDs and job names exist
- **Conflicting options**: Some fields are mutually exclusive (e.g., `endpoint` vs `path`)

## Best Practices

1. **Environment Variables**: Store sensitive data like API keys in environment variables
2. **Descriptive IDs**: Use clear, descriptive names for components, jobs, and workflows
3. **Modular Design**: Break complex configurations into smaller, reusable pieces  
4. **Documentation**: Use `title` and `description` fields to document your configurations
5. **Version Control**: Keep your model-compose.yml files in version control
6. **Testing**: Test configurations with different input scenarios

## Need Help?

- **Issues**: Report problems at [GitHub Issues](https://github.com/anthropics/claude-code/issues)
- **Examples**: Browse the `examples/` directory for working configurations
- **Field Definitions**: Check the source code for detailed field definitions and constraints