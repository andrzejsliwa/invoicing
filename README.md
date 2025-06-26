# 🧾 Rails Invoicing Application

A modern Rails 8.0.2 invoicing application built with PostgreSQL, Hotwire, Tailwind CSS, and enhanced with Claude Code MCP integration for an optimal development experience.

## 🚀 Features

- **Modern Rails Stack**: Rails 8.0.2 with Hotwire (Turbo + Stimulus) for SPA-like interactions
- **Solid Infrastructure**: Database-backed caching, job processing, and WebSockets (no Redis needed)
- **Responsive Design**: Tailwind CSS for modern, mobile-first UI
- **Production Ready**: Docker containerization with Kamal for zero-downtime deployments
- **AI-Enhanced Development**: Comprehensive MCP server integration for Claude Code
- **Security First**: Brakeman scanning, encrypted credentials, and comprehensive CI/CD

## 📋 Requirements

- **Ruby**: 3.4.2
- **Rails**: 8.0.2
- **Database**: PostgreSQL 12+
- **Node.js**: 18+ (for asset compilation)
- **Docker**: For containerized deployment (optional)

## 🛠️ Quick Start

### Initial Setup

```bash
# Clone the repository
git clone https://github.com/andrzejsliwa/invoicing.git
cd invoicing

# Install dependencies and set up database
bin/setup

# Start the development server (Rails + Tailwind watcher)
bin/dev
```

The application will be available at `http://localhost:3000`

### Manual Setup

If you prefer step-by-step setup:

```bash
# Install Ruby dependencies
bundle install

# Create and migrate databases
bin/rails db:create
bin/rails db:migrate
bin/rails db:seed

# Start development server
bin/rails server

# In another terminal, start Tailwind CSS watcher
bin/rails tailwindcss:watch
```

## 🏗️ Architecture

### Technology Stack

- **Backend**: Ruby on Rails 8.0.2 with MVC architecture
- **Frontend**: Hotwire (Turbo + Stimulus) with Tailwind CSS
- **Database**: PostgreSQL with multi-database configuration
- **Assets**: Propshaft pipeline with Importmap for JavaScript
- **Background Jobs**: Solid Queue (database-backed)
- **Caching**: Solid Cache (database-backed)
- **WebSockets**: Solid Cable (database-backed ActionCable)
- **Deployment**: Kamal with Docker containerization

### Database Architecture

The application uses multiple PostgreSQL databases:

- **Primary**: Main application data (invoices, customers, etc.)
- **Cache**: Solid Cache storage
- **Queue**: Background job processing
- **Cable**: WebSocket connections

## 🧪 Development

### Running Tests

```bash
# Run all tests
bin/rails test

# Run specific test types
bin/rails test test/models     # Model tests
bin/rails test test/system     # System tests

# Run specific test file
bin/rails test test/models/invoice_test.rb

# Run specific test line
bin/rails test test/models/invoice_test.rb:25
```

### Code Quality

```bash
# Run linter
bin/rubocop

# Auto-fix linting issues
bin/rubocop -a

# Run security scanner
bin/brakeman
```

### Database Operations

```bash
# Create migration
bin/rails generate migration CreateInvoices

# Run migrations
bin/rails db:migrate

# Rollback migration
bin/rails db:rollback

# Reset database
bin/rails db:reset

# Open Rails console
bin/rails console
```

## 🤖 AI-Enhanced Development

This project includes comprehensive MCP (Model Context Protocol) integration for enhanced development with Claude Code:

### Available MCP Servers

1. **Rails MCP Server** - Access to Rails, Stimulus, Turbo, and Kamal guides
2. **GitHub MCP Server** - Repository management and GitHub integration
3. **HT MCP Server** - Terminal session management
4. **Browser MCP Server** - Web automation and testing
5. **Memory MCP Server** - Session persistence and context
6. **File System MCP Server** - Enhanced file operations
7. **Web Fetch MCP Server** - Web content retrieval

### Setup MCP Integration

```bash
# Install Claude Code CLI
npm install -g @anthropic-ai/claude-code

# Initialize in project
claude init

# Add Rails MCP server
claude mcp add rails-mcp-server
```

See `CLAUDE.md` for detailed MCP setup instructions.

## 🚀 Deployment

### Production Deployment with Kamal

```bash
# Initial setup (first deployment)
bin/kamal setup

# Deploy application
bin/kamal deploy

# Rollback to previous version
bin/kamal rollback

# Check application status
bin/kamal app status
```

### Docker Development

```bash
# Build Docker image
docker build -t invoicing .

# Run with Docker Compose (if configured)
docker-compose up
```

## 🔧 Configuration

### Environment Variables

Create `.env` files for different environments:

```bash
# .env.development
DATABASE_URL=postgresql://username:password@localhost/invoicing_development
RAILS_MASTER_KEY=your_master_key_here

# .env.production
DATABASE_URL=postgresql://username:password@host/invoicing_production
RAILS_MASTER_KEY=your_production_master_key
```

### Credentials Management

```bash
# Edit credentials
bin/rails credentials:edit

# Edit environment-specific credentials
bin/rails credentials:edit --environment production
```

## 📊 Monitoring & Logging

- **Application Logs**: `log/development.log`, `log/production.log`
- **Background Jobs**: Monitor via Solid Queue dashboard
- **Performance**: Built-in Rails performance monitoring
- **Health Check**: Available at `/up` endpoint

## 🧾 Invoicing Features (Planned)

The application is designed to support comprehensive invoicing workflows:

- **Customer Management**: Create and manage customer profiles
- **Invoice Creation**: Generate professional invoices with line items
- **PDF Generation**: Export invoices as PDF documents
- **Email Integration**: Send invoices via email
- **Payment Tracking**: Track invoice payments and status
- **Reporting**: Generate financial reports and analytics
- **Multi-Currency**: Support for multiple currencies
- **Tax Management**: Handle various tax rates and calculations

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Run tests and ensure code quality (`bin/rails test && bin/rubocop`)
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Development Guidelines

- Follow Rails conventions and best practices
- Write tests for new functionality
- Ensure all CI checks pass
- Update documentation as needed
- Use descriptive commit messages

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Ruby on Rails](https://rubyonrails.org/)
- Styled with [Tailwind CSS](https://tailwindcss.com/)
- Enhanced with [Hotwire](https://hotwired.dev/)
- Deployed with [Kamal](https://kamal-deploy.org/)
- AI-enhanced development with [Claude Code](https://claude.ai/code)

---

**Ready to build amazing invoicing solutions!** 🚀

For detailed development guidance and MCP setup, see [CLAUDE.md](CLAUDE.md).

