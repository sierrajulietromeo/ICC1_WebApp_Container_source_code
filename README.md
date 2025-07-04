# ICC1_WebApp_Container_source_code

## Tech Stack & Setup

This repository contains a sample Flask web application configured for deployment with Docker and Azure Cosmos DB. The app is designed for cloud-native deployment and demonstrates separation of compute and database using managed services.

### Key Technologies

- **Flask**: Python web framework
- **Azure Cosmos DB**: Serverless NoSQL database (cloud-managed)
- **Docker**: Containerization for consistent deployment
- **python-dotenv**: Loads environment variables from a `.env` file

### Repository Structure

- `app.py` — Main Flask application
- `requirements.txt` — Python dependencies
- `Dockerfile` — Container build instructions
- `.dockerignore` — Files/directories excluded from Docker build context
- `.env` — Environment variables (should NOT be committed; see below)
- `templates/` — HTML templates
- `static/` — Static files (CSS, images)

### Environment Variables

Sensitive configuration (such as Cosmos DB credentials) is managed via a `.env` file. Example:

```
COSMOS_ENDPOINT=your-cosmos-endpoint
COSMOS_KEY=your-cosmos-key
```

**Note:** The `.env` file should be excluded from version control using `.dockerignore` and `.gitignore`.

### Building and Running with Docker

1. Build the image:
   ```bash
   docker build -t my-todoapp .
   ```
2. Run the container (mapping port 8080):
   ```bash
   docker run -p 8080:8080 --env-file .env my-todoapp
   ```

#### Building for a Different Architecture (e.g., AMD64 on ARM64)

If you are on ARM64 and need an AMD64 image:
```bash
docker buildx create --use
docker buildx build --platform linux/amd64 -t my-todoapp-amd64 . --load
```

### Python Environment

If running locally (not in Docker), install dependencies with:
```bash
pip install -r requirements.txt
```

### License

MIT License