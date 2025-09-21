# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial release of build-push-image action
- Docker image building and pushing with caching
- Support for custom image names and version tags
- GitHub Actions cache integration for faster builds
- Comprehensive documentation and examples

### Features
- Docker Hub, GitHub Container Registry, and ECR support
- Automatic Docker Buildx setup
- Build argument support for version injection
- Secure credential handling through GitHub secrets
- Output variables for downstream workflow usage

## [1.0.0] - 2025-09-21

### Added
- Initial public release
- Basic Docker build and push functionality
- Caching support using GitHub Actions cache
- Configurable inputs for username, password, image name, and version
- Output variable for complete image name with tag

### Documentation
- Complete README with usage examples
- Example workflows for common scenarios
- Troubleshooting guide
- Setup instructions for different registries