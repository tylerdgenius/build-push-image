# Contributing to Build Push Image Action

Thank you for your interest in contributing! This document provides guidelines for contributing to this GitHub Action.

## Development Setup

1. Fork the repository
2. Clone your fork locally
3. Create a new branch for your feature/fix
4. Make your changes
5. Test thoroughly
6. Submit a pull request

## Testing Your Changes

### Local Testing

Since this is a GitHub Action, local testing is limited. However, you can:

1. **Validate the action.yml syntax:**
   ```bash
   # Use GitHub's action validator or YAML linter
   yamllint action.yml
   ```

2. **Test in a fork:**
   - Create a test repository
   - Reference your fork/branch in a workflow
   - Run the workflow to test functionality

### Integration Testing

Create test workflows in `.github/workflows/test-*.yml` that:
- Build sample applications
- Test different input combinations
- Verify outputs are correct
- Test with different registries

## Code Standards

### action.yml Guidelines

- Keep inputs well-documented with clear descriptions
- Use appropriate `required` flags
- Provide sensible defaults where possible
- Follow GitHub Actions naming conventions

### Documentation

- Update README.md for any new features
- Add examples for new functionality
- Update CHANGELOG.md following [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format
- Ensure all examples work as documented

## Pull Request Process

1. **Before submitting:**
   - Test your changes thoroughly
   - Update documentation
   - Add changelog entry
   - Ensure examples still work

2. **Pull request requirements:**
   - Clear description of changes
   - Reference any related issues
   - Include test results
   - Follow the template

3. **Review process:**
   - Maintainer review required
   - All checks must pass
   - Documentation must be updated

## Reporting Issues

When reporting bugs or requesting features:

1. **Search existing issues** first
2. **Use issue templates** when available
3. **Provide clear reproduction steps** for bugs
4. **Include relevant workflow examples**

### Bug Reports

Include:
- Action version being used
- Complete workflow YAML
- Error messages/logs
- Expected vs actual behavior
- Environment details (runner OS, etc.)

### Feature Requests

Include:
- Clear use case description
- Proposed API/interface
- Examples of how it would be used
- Any alternatives considered

## Release Process

1. Update version in documentation examples
2. Update CHANGELOG.md
3. Create GitHub release with tag
4. Update marketplace listing

## Code of Conduct

Be respectful and professional in all interactions. This project follows the GitHub Community Guidelines.

## Questions?

Feel free to open an issue for questions about contributing or using this action.