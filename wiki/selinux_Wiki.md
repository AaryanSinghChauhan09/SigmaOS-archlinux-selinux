# SigmaOS-archlinux-selinux Component Wiki

## Overview
SigmaOS-archlinux-selinux provides SELinux (Security-Enhanced Linux) compatibility and security policy management for the SigmaOS operating system. It demonstrates the security module integration and policy management within the SigmaOS ecosystem, following the principles of clear abstraction and deterministic security initialization.

## Principles
- Single Responsibility
- Security-Enhanced Abstraction
- Fail-Fast on Security Policy Errors
- Deterministic SELinux Initialization
- Clear Abstraction Over SELinux APIs
- Composition over Inheritance for security module extensions

## Architecture
SigmaOS-archlinux-selinux follows a SELinux compatibility pattern:
- **Security Core**: Provides SELinux policy compatibility and management primitives
- **Policy Management**: Handles SELinux policy loading, versioning, and enforcement
- **Context Management**: Manages security contexts and label operations
- **Audit Integration**: Integrates with system audit logging for security events

## API
The component provides the following public APIs:
- `selinux::load_policy(path)` - Load an SELinux policy file
- `selinux::get_context(path)` - Get the SELinux context of a file
- `selinux::set_context(path, context)` - Set the SELinux context of a file
- `selinux::is_enabled()` - Check if SELinux is enabled
- Error types for policy loading failures or context operation errors

## Test Structure (Arrange-Act-ASSERT)
All tests follow the AAA pattern:
1. **Arrange**: Set up test environment with specific SELinux configuration
2. **Act**: Execute the code under test (policy loading, context operations)
3. **Assert**: Verify the expected SELinux results

Example:
```rust
#[test]
fn test_selinux_policy_load_aaa() {
    // Arrange
    let policy_path = "/etc/selinux/policy.25";
    
    // Act
    let result = selinux::load_policy(policy_path);
    
    // Assert
    assert!(result.is_ok());
    assert!(selinux::is_enabled());
}
```

## Development
- Follows Rust best practices with `#![forbid(unsafe_code)]`
- SELinux initialization is best-effort; gracefully degrades on unsupported configurations
- Comprehensive error types for all SELinux failure scenarios
- Unit tests provided for policy loading and context operations
- Integration tests for full SELinux compatibility with actual policy files

## TODO
- Add support for additional SELinux policy versions and types
- Expand context management capabilities
- Add audit integration and event logging features
- Create integration tests with actual SELinux policy files
- Implement policy versioning and migration features