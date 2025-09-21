# Example Workflows

This directory contains example workflow files demonstrating different use cases for the build-push-image action.

## Available Examples

- [`basic-workflow.yml`](basic-workflow.yml) - Simple build and push on main branch
- [`semantic-versioning.yml`](semantic-versioning.yml) - Build with semantic version tags
- [`multi-environment.yml`](multi-environment.yml) - Different images for different environments
- [`pull-request.yml`](pull-request.yml) - Build (but don't push) on pull requests
- [`scheduled-builds.yml`](scheduled-builds.yml) - Scheduled builds for base image updates
- [`matrix-builds.yml`](matrix-builds.yml) - Build multiple variants of the same application

## How to Use

1. Copy the relevant example to your `.github/workflows/` directory
2. Modify the image names and other parameters to match your project
3. Ensure you have the required secrets configured in your repository
4. Commit and push to trigger the workflow

## Required Secrets

All examples require these secrets to be configured in your repository:

- `DOCKER_USERNAME` - Your Docker registry username
- `DOCKER_PASSWORD` - Your Docker registry password or token