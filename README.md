# alex-fastapi-security-demo

A simple FastAPI security demo application with a GitHub Actions pipeline that builds, scans, tests, and publishes a Docker image.

## Current Setup

- FastAPI application in `main.py`
- Dependencies in `requirements.txt`
- Docker container build via `Dockerfile`
- GitHub Actions workflows in `.github/workflows/`
- Container image published to GitHub Container Registry: `ghcr.io/alexjelani/python-fastapi`
- Security scanning via OWASP ZAP and Trivy in CI

## Requirements

- Docker
- Python 3.12+
- `pip` or virtual environment support

## Project Structure

```bash
alex-fastapi-security-demo/
├── .github/workflows/          # CI workflows
├── Dockerfile                 # Docker image build definition
├── README.md                  # Project documentation
├── main.py                    # FastAPI app entry point
├── requirements.txt           # Python dependencies
├── sonar-project.properties   # SonarCloud project settings
└── tests/                     # Unit tests
```

## Running Locally

1. Install dependencies:

```bash
python -m pip install -r requirements.txt
```

2. Start the app locally:

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

3. Open the app in your browser:

```text
http://127.0.0.1:8000
```

## Docker

Build the Docker image locally:

```bash
docker build -t alex-fastapi-security-demo .
```

Run the container:

```bash
docker run -d -p 8000:8000 alex-fastapi-security-demo
```

Access the running app at:

```text
http://127.0.0.1:8000
```

## GitHub Actions

The repository includes a main CI pipeline in `.github/workflows/main.yml`.
It runs on pushes to `main` and manual dispatch.

The pipeline performs:

- Docker image build
- Python linting and formatting checks
- Unit tests
- Trivy vulnerability scan on the image
- OWASP ZAP app scan
- SonarCloud analysis
- Docker image publish via `.github/workflows/push-docker-image.yml`

## Published Image

The pipeline publishes to GitHub Container Registry:

- `ghcr.io/alexjelani/python-fastapi:${{ github.sha }}`
- `ghcr.io/alexjelani/python-fastapi:latest`
- `ghcr.io/alexjelani/python-fastapi:testing`

## Tests

Run unit tests locally with:

```bash
pytest tests/
```

## Notes

- The app is intentionally insecure in places for educational purposes.
- Keep the `main` branch as the production branch.
- The GitHub workflow currently requires a `GHCR_PAT` repository secret for image publish fallback.
