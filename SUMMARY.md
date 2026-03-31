# Language Servers Repository Summary

## Overview

This repository is a **monorepo for AWS Language Servers** that provides intelligent language support for AWS services and related technologies across multiple Integrated Development Environments (IDEs). The language servers implement the Language Server Protocol (LSP) and its extensions, enabling rich editing experiences including code completion, diagnostics, hover information, and formatting for AWS-related file types and query languages.

The repository is designed to support both desktop IDE integrations and browser-based environments, making it versatile for various development scenarios.

## Primary Purpose

The primary purpose of this repository is to:

1. **Centralize AWS Language Server Development**: Provide a unified codebase for developing, maintaining, and distributing language servers that support AWS services and related technologies
2. **Enable Cross-IDE Integration**: Support multiple IDE platforms (VSCode, Visual Studio, JetBrains) through standardized LSP implementations
3. **Facilitate AWS Service Integration**: Offer seamless integration with AWS services like CodeWhisperer (Amazon Q), S3, CloudFormation, and CodeBuild
4. **Support Multiple Runtime Environments**: Enable language servers to run in both Node.js desktop environments and browser-based webworker contexts

## Language Server Implementations

The repository includes the following language server implementations:

### Core Language Servers

#### **CodeWhisperer (Amazon Q) Language Server** (`aws-lsp-codewhisperer`)
- Provides AI-powered code recommendations and suggestions through Amazon Q
- Supports inline completions with ghost text
- Features security scanning capabilities
- Includes customization support for enterprise customers
- Supports developer profiles and workspace configurations
- Integrates with Q Chat for conversational AI assistance
- Handles code references and telemetry management

#### **PartiQL Language Server** (`aws-lsp-partiql`)
- Provides language support for the PartiQL query language
- Uses WebAssembly-compiled Rust parser for high-performance parsing
- Offers diagnostics, syntax highlighting, and language features
- Leverages the official PartiQL team's parser implementation
- Includes ANTLR-based lexer and parser for advanced language features

#### **CloudFormation Language Server** (`aws-lsp-cloudformation`)
- Supports AWS CloudFormation template authoring in YAML and JSON
- Provides schema-based validation and completion
- Offers infrastructure-as-code assistance for AWS resource definitions

#### **JSON Language Server** (`aws-lsp-json`)
- Generic JSON language service with schema support
- Provides completion, diagnostics, hover information, and formatting
- Reusable foundation for JSON-based AWS configuration files

#### **YAML Language Server** (`aws-lsp-yaml`)
- Generic YAML language service with schema support
- Offers language features including hover, completion, diagnostics, and formatting
- Reusable foundation for YAML-based AWS configuration files
- Includes custom patches for enhanced functionality

#### **Identity Language Server** (`aws-lsp-identity`)
- Manages authentication and identity operations
- Handles AWS SSO (Single Sign-On) flows
- Supports multiple authentication mechanisms
- Manages token lifecycle and automatic refresh
- Integrates with AWS shared configuration and credentials files

#### **BuildSpec Language Server** (`aws-lsp-buildspec`)
- Provides language support for AWS CodeBuild buildspec files
- Supports both YAML and JSON formats
- Offers schema-based validation specific to CodeBuild configurations

#### **S3 Language Server** (`aws-lsp-s3`)
- Example language server demonstrating AWS service integration
- Provides S3 bucket name completions
- Showcases credential passing from IDE extensions to servers

#### **Notification Language Server** (`aws-lsp-notification`)
- Handles notification management across language servers
- Coordinates messaging between servers and clients

#### **ANTLR4 Language Server** (`aws-lsp-antlr4`)
- Generic ANTLR4 LSP server for grammar development
- Provides diagnostics and completion for ANTLR grammars
- Supports parsers/lexers generated from `*.g4` files by antlr4ng and antlr4-c3
- Includes integration test support with PostgreSQL grammar examples

### Example/Template Servers

#### **Hello World Language Server** (`hello-world-lsp`)
- Template and example implementation for creating new language servers
- Demonstrates best practices and basic structure
- Useful starting point for custom language server development

#### **Device SSO Auth Language Server** (`device-sso-auth-lsp`)
- Example implementation of Device authentication SSO flow
- Port of SSO flow implementation from VSCode sample client as LSP server
- Supports only standalone AWS Server Runtime (requires Node.js `fs` access)
- Demonstrates device authentication flow with token caching

## Supported IDE Clients

The repository provides sample client integrations for three major IDE platforms:

### **Visual Studio Code** (`client/vscode`)
- Minimal VSCode extension for testing language servers
- Demonstrates credential management and bearer token authentication
- Shows integration patterns for VSCode extensions
- Includes examples of IAM credential and SSO authentication flows

### **Visual Studio** (`client/visualStudio`)
- Minimal Visual Studio extension implementation
- Enables testing of language servers in Visual Studio environment
- Provides Windows-specific integration examples

### **JetBrains IDEs** (`client/jetbrains`)
- Gradle-based JetBrains plugin implementation
- Supports IntelliJ IDEA, PyCharm, WebStorm, and other JetBrains IDEs
- Demonstrates LSP integration in JetBrains plugin architecture

## Authentication Mechanisms

The repository supports multiple authentication mechanisms for secure AWS service integration:

### **IAM Credentials (SigV4)**
- Traditional AWS access key and secret key authentication
- Supports profile-based credentials from AWS shared credentials file
- Encrypted credential transmission from IDE to language server
- Session token support for temporary credentials

### **Bearer Tokens**
- Token-based authentication for API access
- Secure token management and transmission
- Support for token refresh flows

### **AWS Builder ID**
- Personal AWS account SSO authentication
- Device code flow and PKCE (Proof Key for Code Exchange) authorization
- Automatic token refresh and caching
- Reserved SSO region (`us-east-1`) for Builder ID

### **IAM Identity Center (AWS SSO)**
- Enterprise SSO integration
- Support for multiple SSO sessions and profiles
- Authorization code flow with PKCE
- Device code flow for headless environments
- Client registration caching
- Integration with AWS shared configuration files

### Authentication Features
- Encrypted credential storage and transmission
- Automatic token refresh with background auto-refresher
- Profile and session management
- Support for proxy configurations
- Token invalidation and cleanup

## Technology Stack

### **Primary Languages and Frameworks**
- **TypeScript**: Primary development language for type safety and maintainability
- **Node.js**: Runtime environment (version 18+)
- **Language Server Protocol (LSP)**: Standard protocol for language server communication

### **Core Dependencies**
- **@aws/language-server-runtimes**: AWS's LSP runtime framework providing protocol implementations
- **vscode-languageserver**: LSP server implementation library
- **vscode-languageserver-textdocument**: Document management utilities

### **Build and Bundling**
- **Webpack**: Module bundler for creating standalone applications
- **TypeScript Compiler**: For transpiling TypeScript to JavaScript
- **npm Workspaces**: For monorepo management and dependency handling

### **AWS SDK Integration**
- **@aws-sdk/client-sso-oidc**: For SSO authentication flows
- **@aws-sdk/token-providers**: Token management and provisioning
- **@smithy/types**: Type definitions for AWS SDK v3

### **Specialized Technologies**
- **WebAssembly (WASM)**: For high-performance parsers (PartiQL with Rust parser, Tree-sitter for parsing)
- **ANTLR4**: For lexer and parser generation (PartiQL, generic ANTLR4 server)
- **ANTLR4ng**: Next-generation ANTLR4 TypeScript runtime for grammar processing
- **ANTLR4-c3**: Code completion core library for ANTLR4 grammars
- **MynahUI**: Web-based chat interface for Amazon Q
- **Tree-sitter**: Incremental parsing library used via WebAssembly

### **Testing Frameworks**
- **Jest**: Testing framework for PartiQL and ANTLR4 servers
- **Mocha**: Testing framework for CodeWhisperer, identity and notification servers
- **Chai**: Assertion library used with Mocha tests
- **Sinon**: Test doubles and mocking library
- **ts-mocha**: TypeScript-enabled Mocha test runner

### **Development Tools**
- **ESLint**: Code linting and quality enforcement
- **Prettier**: Code formatting
- **Husky**: Git hooks for pre-commit checks
- **Commitlint**: Conventional commit message enforcement

## Key Capabilities and Integration Points

### Language Features
- **Code Completion**: Context-aware suggestions for AWS resources, configurations, and queries
- **Diagnostics**: Real-time error detection and validation
- **Hover Information**: Documentation and type information on hover
- **Formatting**: Automatic code formatting for JSON and YAML files
- **Syntax Highlighting**: Rich syntax support through language services

### AWS Service Integration

#### **Amazon Q (CodeWhisperer)**
- AI-powered code generation and recommendations
- Inline suggestions with real-time streaming
- Security scanning for code vulnerabilities
- Reference tracking for suggested code
- Customization support for enterprise-specific patterns
- Chat interface for conversational coding assistance
- Support for quick actions and follow-up suggestions

#### **AWS S3**
- Bucket name completion and discovery
- Example of authenticated AWS API calls from language servers

#### **AWS CloudFormation**
- Template validation against CloudFormation schema
- Resource property completion
- Template structure assistance

#### **AWS CodeBuild**
- BuildSpec file validation
- Phase and command completion
- Build configuration assistance

### Chat and Conversational AI
- **Q Chat Client**: Web-based chat interface using MynahUI
- **Bidirectional Communication**: PostMessage-based communication between webview and host
- **Chat Operations**: Prompt sending, tab management, context commands
- **User Interactions**: Follow-ups, feedback, link handling, file operations
- **Conversation History**: Listing and navigation of past conversations
- **Serialization**: Chat state persistence and restoration

### Cross-Platform Support
- **Desktop Environments**: Full Node.js runtime with file system access
- **Browser Environments**: WebWorker-compatible bundles with browser APIs
- **Module Overrides**: Ability to substitute Node.js modules with browser-compatible alternatives

### Credential Management
- **Encrypted Communication**: Credentials encrypted during transmission
- **Provider Pattern**: Abstraction layer for credential sources
- **Multiple Providers**: Support for IDE-provided, profile-based, and SSO credentials
- **Automatic Refresh**: Background token refresh to maintain authentication

### Developer Experience
- **Workspace Configurations**: Support for workspace-specific settings
- **Proxy Support**: HTTP/HTTPS proxy configuration for corporate environments
- **Telemetry Control**: Opt-in/opt-out telemetry configuration
- **Customization**: Enterprise customization ARN support
- **Hot Reload**: Development mode with watch compilation

## Architecture

The repository follows a three-layer architecture designed for reusability and maintainability:

### **Layer 1: Language Services** (`core/`)
- Inner-most layer containing business logic
- Implement the `AwsLanguageService` interface
- Insulated from LSP protocol details
- Reusable across different language server implementations
- Designed to work in both browser and Node.js environments
- Components injected for platform-specific functionality (file I/O, etc.)

### **Layer 2: Language Servers** (`server/`)
- Middle layer implementing LSP protocol
- Wrap language services with LSP communication
- Handle protocol requests and responses
- Route client requests to appropriate language service methods
- Manage server lifecycle and initialization

### **Layer 3: Binaries/Applications** (`app/`)
- Outer-most layer for distribution
- Instantiate language servers with platform-specific components
- Bundle into standalone JavaScript applications
- Package for specific runtime environments
- One binary can contain multiple language servers
- Designed for integration into IDE extensions
- Includes specialized bundles like `aws-lsp-yaml-json-webworker` for browser environments

### Monorepo Structure
```
language-servers/
├── app/                    # Bundled runtime applications
├── chat-client/            # Q Chat web interface
├── client/                 # Sample IDE integrations
│   ├── jetbrains/         # JetBrains plugin
│   ├── visualStudio/      # Visual Studio extension
│   └── vscode/            # VSCode extension
├── core/                   # Supporting libraries
│   ├── aws-lsp-core/      # Core utilities and interfaces
│   ├── codewhisperer-streaming/  # CodeWhisperer streaming client package
│   └── q-developer-streaming-client/  # Q Developer streaming client package
├── server/                 # Language server implementations
│   ├── aws-lsp-codewhisperer/
│   ├── aws-lsp-partiql/
│   ├── aws-lsp-cloudformation/
│   ├── aws-lsp-json/
│   ├── aws-lsp-yaml/
│   ├── aws-lsp-identity/
│   ├── aws-lsp-buildspec/
│   ├── aws-lsp-s3/
│   ├── aws-lsp-notification/
│   ├── aws-lsp-antlr4/
│   ├── device-sso-auth-lsp/
│   └── hello-world-lsp/
└── script/                 # Build and maintenance scripts
```

## Development Workflow

### Building
```bash
npm install          # Install dependencies
npm run compile      # Build all packages
npm run clean        # Clean build artifacts
```

### Testing
```bash
npm run test         # Run all tests
npm run test-unit    # Run unit tests
npm run test-integ   # Run integration tests
```

### Packaging
```bash
npm run package      # Create distributable bundles
```

### Code Quality
```bash
npm run lint         # Run linting
npm run format       # Format code with Prettier
```

## Integration Patterns

### For IDE Extension Developers
1. **Launch Language Server**: Start the appropriate binary as a child process
2. **Connect Streams**: Provide stdin/stdout streams to IDE's LSP client
3. **Handle Authentication**: Resolve credentials and send to server via encrypted channel
4. **Manage Lifecycle**: Handle server initialization, configuration updates, and shutdown

### For Language Server Developers
1. **Implement Language Service**: Create service implementing `AwsLanguageService` interface
2. **Wrap in Language Server**: Use language-server-runtimes to create LSP wrapper
3. **Create Application Bundle**: Package server for distribution
4. **Test with Sample Client**: Use provided IDE clients for testing

## Security Considerations

- **Credential Encryption**: All credentials encrypted during transmission
- **Token Security**: Secure storage and automatic cleanup of authentication tokens
- **Proxy Support**: Corporate proxy support for secure network environments
- **Content Sharing Control**: User-controlled options for sharing code with AWS
- **Reference Tracking**: Transparency in code suggestion sources

## Contributing

The repository follows AWS open source contribution guidelines:
- Apache 2.0 License
- Conventional Commits for commit messages
- Pre-commit hooks for code quality
- Comprehensive testing requirements
- Code of Conduct enforcement

For detailed contribution guidelines, see [CONTRIBUTING.md](CONTRIBUTING.md).

## Key Resources

- **Main README**: [README.md](README.md)
- **Architecture Details**: [ARCHITECTURE.md](ARCHITECTURE.md)
- **Contribution Guide**: [CONTRIBUTING.md](CONTRIBUTING.md)
- **Language Server Runtimes**: https://github.com/aws/language-server-runtimes
- **Language Server Protocol**: https://microsoft.github.io/language-server-protocol/

---

This repository represents AWS's commitment to providing world-class developer tools that integrate seamlessly with AWS services across multiple IDE platforms, enabling developers to build on AWS with confidence and efficiency.
