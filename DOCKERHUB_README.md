# CloudFlow API

[![Docker Pulls](https://img.shields.io/docker/pulls/ahmedmusa/cloudflow-api)](https://hub.docker.com/r/ahmedmusa/cloudflow-api)
[![Docker Image Size](https://img.shields.io/docker/image-size/ahmedmusa/cloudflow-api/latest)](https://hub.docker.com/r/ahmedmusa/cloudflow-api)

A lightweight FastAPI backend for user profile management with MongoDB support.

## Quick Start

```bash
docker pull ahmedmusa/cloudflow-api:latest
docker run -p 3001:3001 \
  -e MONGO_URI="mongodb://host:27017/cloudflow" \
  -e DB_NAME="cloudflow" \
  -e FRONTEND_ORIGINS="http://localhost:3000" \
  ahmedmusa/cloudflow-api:latest
```

## Features

- **FastAPI** - Modern, high-performance web framework
- **MongoDB** - Async MongoDB driver (Motor)
- **RESTful API** - Full CRUD operations for user profiles
- **CORS Support** - Configurable cross-origin requests
- **Lightweight** - Based on Python 3.11-slim

## Environment Variables

| Variable | Required | Description | Example |
|----------|----------|-------------|---------|
| `MONGO_URI` | Yes | MongoDB connection string | `mongodb://admin:pass@host:27017/cloudflow?authSource=admin` |
| `DB_NAME` | Yes | Database name | `cloudflow` |
| `FRONTEND_ORIGINS` | Yes | Comma-separated allowed CORS origins | `http://localhost:3000,https://app.example.com` |

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/profiles` | Create a new profile |
| GET | `/api/profiles` | List all profiles |
| GET | `/api/profiles/{id}` | Get profile by ID |
| PATCH | `/api/profiles/{id}` | Update profile |
| DELETE | `/api/profiles/{id}` | Delete profile |

## Docker Compose Example

```yaml
version: '3.8'
services:
  api:
    image: ahmedmusa/cloudflow-api:latest
    ports:
      - "3001:3001"
    environment:
      MONGO_URI: mongodb://mongodb:27017/cloudflow?authSource=admin
      DB_NAME: cloudflow
      FRONTEND_ORIGINS: http://localhost:3000
    depends_on:
      - mongodb
  
  mongodb:
    image: mongo:6
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

## Running with Environment File

Create a `.env` file:
```
MONGO_URI=mongodb://admin:password@host.docker.internal:27017/cloudflow?authSource=admin
DB_NAME=cloudflow
FRONTEND_ORIGINS=http://localhost:3000
```

Run with:
```bash
docker run --env-file .env -p 3001:3001 ahmedmusa/cloudflow-api:latest
```

## Health Check

The API exposes a health endpoint at the root path. Once running, verify with:
```bash
curl http://localhost:3001/
```

## Source Code

- GitHub: https://github.com/iAhmedMusa/clowflow_api

## Supported Tags

- `latest` - Latest stable release
- `v1.0.0` - Version tags (coming soon)

## License

MIT License - See GitHub repository for details.
