# Build and Push Docker Image Action

A GitHub Action that builds and pushes Docker images to a registry with intelligent caching support.

## Features

- 🐳 Build and push Docker images to any Docker registry
- 🚀 Built-in caching using GitHub Actions cache for faster builds
- 🔒 Secure credential handling
- 📦 Configurable image tagging with version support
- 🛠️ Docker Buildx support for advanced build features

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `docker_username` | Docker registry username | ✅ | - |
| `docker_password` | Docker registry password/token | ✅ | - |
| `docker_image_name` | Full Docker image name (e.g., `myorg/myapp`) | ✅ | - |
| `release_version` | Version tag for the image | ❌ | `0.0.0` |

## Outputs

| Output | Description |
|--------|-------------|
| `image` | Complete Docker image name with tag (e.g., `myorg/myapp:1.0.0`) |

## Usage

### Basic Example

```yaml
name: Build and Deploy

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
    
    - name: Build and push Docker image
      id: build
      uses: tylerdgenius/build-push-image@v1
      with:
        docker_username: ${{ secrets.DOCKER_USERNAME }}
        docker_password: ${{ secrets.DOCKER_PASSWORD }}
        docker_image_name: myorg/myapp
        release_version: ${{ github.sha }}
    
    - name: Print image name
      run: echo "Built image: ${{ steps.build.outputs.image }}"
```

### With Semantic Versioning

```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
    
    - name: Get version from tag
      id: version
      run: echo "VERSION=${GITHUB_REF#refs/tags/v}" >> $GITHUB_OUTPUT
    
    - name: Build and push Docker image
      uses: tylerdgenius/build-push-image@v1
      with:
        docker_username: ${{ secrets.DOCKER_USERNAME }}
        docker_password: ${{ secrets.DOCKER_PASSWORD }}
        docker_image_name: myorg/myapp
        release_version: ${{ steps.version.outputs.VERSION }}
```

### Multi-environment Example

```yaml
name: Build and Deploy

on:
  push:
    branches: [ main, develop ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4
    
    - name: Set environment
      id: env
      run: |
        if [[ ${{ github.ref }} == 'refs/heads/main' ]]; then
          echo "ENV=prod" >> $GITHUB_OUTPUT
          echo "VERSION=${{ github.sha }}" >> $GITHUB_OUTPUT
        else
          echo "ENV=dev" >> $GITHUB_OUTPUT
          echo "VERSION=dev-${{ github.sha }}" >> $GITHUB_OUTPUT
        fi
    
    - name: Build and push Docker image
      uses: tylerdgenius/build-push-image@v1
      with:
        docker_username: ${{ secrets.DOCKER_USERNAME }}
        docker_password: ${{ secrets.DOCKER_PASSWORD }}
        docker_image_name: myorg/myapp-${{ steps.env.outputs.ENV }}
        release_version: ${{ steps.env.outputs.VERSION }}
```

## Setup Instructions

### 1. Repository Secrets

Add the following secrets to your repository:

- `DOCKER_USERNAME`: Your Docker registry username
- `DOCKER_PASSWORD`: Your Docker registry password or access token

**For Docker Hub:**
- Username: Your Docker Hub username
- Password: Your Docker Hub password or access token

**For GitHub Container Registry:**
- Username: Your GitHub username
- Password: A Personal Access Token with `write:packages` scope

**For AWS ECR:**
- Username: `AWS`
- Password: ECR login token (you'll need additional steps to get this)

### 2. Dockerfile Requirements

Ensure your repository contains a `Dockerfile` in the root directory. The action will build using the current directory as context.

Example Dockerfile:
```dockerfile
FROM node:18-alpine

ARG VERSION=0.0.0
ENV APP_VERSION=$VERSION

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

### 3. Registry Configuration

**Docker Hub:**
- No additional configuration needed
- Images will be pushed to `docker.io/username/image-name:tag`

**GitHub Container Registry:**
- Use `ghcr.io/username/image-name` as your image name
- Ensure your token has `write:packages` permission

**AWS ECR:**
- Use full ECR URI: `123456789012.dkr.ecr.region.amazonaws.com/image-name`
- Additional ECR login steps may be required

## Caching

This action uses GitHub Actions cache to speed up Docker builds:

- **Cache key**: Based on the Docker build context
- **Cache scope**: Shared across workflow runs in the same repository
- **Cache type**: GitHub Actions cache (gha)

The cache will significantly reduce build times for subsequent runs when only small changes are made.

## Troubleshooting

### Common Issues

**Authentication Failed:**
- Verify your Docker registry credentials are correct
- Check that secrets are properly set in repository settings
- For registries other than Docker Hub, ensure the correct hostname format

**Build Context Issues:**
- Ensure Dockerfile exists in repository root
- Check that all required files are not in `.dockerignore`
- Verify build context permissions

**Caching Issues:**
- Cache may be cold on first run - this is normal
- Cache effectiveness depends on Docker layer structure
- Consider optimizing Dockerfile for better caching

### Debug Mode

Enable debug logging by setting the `ACTIONS_STEP_DEBUG` secret to `true` in your repository.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with different scenarios
5. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Support

- 📖 [Docker Build Push Action Docs](https://github.com/docker/build-push-action)
- 🐳 [Docker Documentation](https://docs.docker.com/)
- 🔧 [GitHub Actions Documentation](https://docs.github.com/en/actions)