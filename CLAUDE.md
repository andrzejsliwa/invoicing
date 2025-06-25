# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Rails 8.0.2 invoicing application using:
- Ruby 3.4.2
- PostgreSQL database
- Hotwire (Turbo + Stimulus) for interactive features
- Tailwind CSS for styling
- Kamal for deployment
- Docker for containerization

## Common Development Commands

### Initial Setup
```bash
bin/setup              # Install dependencies, create DB, start server
```

### Development Server
```bash
bin/dev                # Start Rails server + Tailwind CSS watcher
bin/rails server       # Start only Rails server
```

### Database
```bash
bin/rails db:create    # Create development and test databases
bin/rails db:migrate   # Run migrations
bin/rails db:seed      # Load seed data
bin/rails db:drop      # Drop databases
bin/rails db:reset     # Drop, create, migrate, and seed
```

### Testing
```bash
bin/rails test                # Run all tests
bin/rails test test/models    # Run model tests
bin/rails test test/system    # Run system tests
bin/rails test TEST=test/models/user_test.rb        # Run single test file
bin/rails test TEST=test/models/user_test.rb:10     # Run specific test line
```

### Code Quality
```bash
bin/rubocop            # Run RuboCop linter
bin/rubocop -a         # Auto-fix RuboCop violations
bin/brakeman           # Run security scanner
```

### Console & Tasks
```bash
bin/rails console      # Rails console
bin/rails routes       # Show all routes
bin/rails generate     # Generate models, controllers, etc.
bin/rails destroy      # Remove generated files
```

### Deployment
```bash
bin/kamal setup        # Initial deployment setup
bin/kamal deploy       # Deploy application
bin/kamal rollback     # Rollback to previous version
```

## Architecture Overview

### Application Structure
- **MVC Pattern**: Standard Rails architecture with models, views, and controllers
- **Asset Pipeline**: Uses Propshaft with Importmap for JavaScript and Tailwind for CSS
- **Background Jobs**: Solid Queue (database-backed, no Redis needed)
- **Caching**: Solid Cache (database-backed)
- **WebSockets**: Solid Cable (database-backed ActionCable)

### Key Directories
- `app/models/`: ActiveRecord models for business logic
- `app/controllers/`: Request handling and response
- `app/views/`: ERB templates with Hotwire integration
- `app/javascript/`: Stimulus controllers and JavaScript modules
- `config/`: Application configuration, routes, and database settings
- `db/`: Database migrations and schema
- `test/`: Minitest test files

### Database Architecture
The application uses multiple PostgreSQL databases:
- **Primary**: Main application data
- **Cache**: Solid Cache storage
- **Queue**: Solid Queue job storage
- **Cable**: WebSocket connection storage

### Frontend Architecture
- **Hotwire**: Server-side rendering with Turbo for SPA-like navigation
- **Stimulus**: Modest JavaScript framework for interactivity
- **Tailwind CSS**: Utility-first CSS framework
- **Importmap**: Native ES modules without bundling

### Deployment Architecture
- **Docker**: Multi-stage Dockerfile for production builds
- **Kamal**: Zero-downtime deployments with health checks
- **Thruster**: HTTP/2 proxy server wrapper
- **SSL**: Let's Encrypt integration via Kamal

## Development Workflow

1. Always run `bin/rubocop` before committing code
2. Run tests with `bin/rails test` to ensure nothing is broken
3. Use `bin/rails generate` for creating new models/controllers
4. Database changes require migrations: `bin/rails generate migration`
5. Use Stimulus for JavaScript interactions, avoid inline scripts
6. Follow Rails conventions for naming and file organization

## Security Considerations

- Credentials are encrypted in `config/credentials.yml.enc`
- Use `Rails.application.credentials` to access secrets
- Run `bin/brakeman` to check for security vulnerabilities
- Never commit sensitive data or API keys

## MCP (Model Context Protocol) Servers

This project uses MCP servers to enhance the development experience with Claude Code. The following MCP servers are required:

### Prerequisites
Ensure you have Claude Code installed and configured:
```bash
# Install Claude Code CLI
npm install -g @anthropic-ai/claude-code

# Initialize Claude Code in your project
claude-code init
```

### 1. Rails MCP Server
Provides Rails-specific functionality and access to Rails, Stimulus, Turbo, and Kamal guides.

**Installation:**
```bash
# Already included in Gemfile under development group
bundle install

# Add to Claude Code MCP configuration
claude-code mcp add rails-mcp-server rails-mcp-server
```

**Usage:**
```bash
# Run in stdio mode (default)
bundle exec rails-mcp-server

# Run in HTTP mode
bundle exec rails-mcp-server --mode http --port 6029

# With debug logging
bundle exec rails-mcp-server --log-level debug
```

### 2. GitHub MCP Server
Provides GitHub integration for repository management, issues, pull requests, and more.

**Setup:**
```bash
# Add GitHub MCP server to Claude Code
claude mcp add github-mcp-server \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=your_github_token_here \
  -- docker run -i --rm -e GITHUB_PERSONAL_ACCESS_TOKEN ghcr.io/github/github-mcp-server

```

**Functionality:**
- Repository management
- Issue and PR creation/management
- Code search across GitHub
- Notifications management
- File operations on GitHub repos

**Note:** The GitHub MCP server requires GitHub API authentication. You'll need to provide a GitHub personal access token during configuration.

### 3. HT MCP Server
Provides terminal session management and command execution capabilities.

**Features:**
- Create and manage terminal sessions
- Execute commands with output capture
- Take terminal snapshots
- Session control and monitoring

### 4. Browser MCP Server
Enables web browser automation and interaction capabilities.

**Features:**
- Navigate to URLs and control web pages
- Take screenshots and page snapshots
- Click elements and fill forms
- Interact with web applications for testing
- Extract page content and data

### 5. Memory MCP Server
Handles session memory management and context persistence.

**Features:**
- Maintain conversation context across sessions
- Store and retrieve development notes
- Persist important project information

### 6. File System MCP Server
Provides enhanced file operations beyond standard file tools.

**Features:**
- Advanced file search and pattern matching
- Bulk file operations
- Directory tree operations
- File metadata access

### 7. Web Fetch MCP Server
Enables web content retrieval and processing.

**Features:**
- Fetch content from URLs
- Process and analyze web pages
- Extract specific information from websites
- Handle various web content formats

**Note:** These additional MCP servers are typically configured at the Claude Code level and provide enhanced capabilities for development, testing, and automation tasks.
