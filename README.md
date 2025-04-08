# CI/CD Pipeline with Node.js, Docker & GitHub Actions 🚀

This project demonstrates a simple **CI/CD pipeline** using a sample Node.js app, **Docker**, and **GitHub Actions**.

---

## 📦 Tech Stack

- Node.js
- Docker
- GitHub Actions
- DockerHub (for image storage)

---

## 🎯 What This Project Does

- Runs `npm install` to install dependencies
- Optionally runs `npm test` (with dummy or real tests)
- Builds a Docker image from the app
- Logs into DockerHub (via GitHub Secrets)
- Pushes the image to DockerHub on every push to the `main` branch

---

## 🛠️ CI/CD Workflow (`.github/workflows/main.yml`)

```yaml
on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-node@v3
      with:
        node-version: '16'
    - run: npm install
    - run: npm test  # optional or replaced with dummy script
    - run: docker build -t your-dockerhub-username/nodejs-app .
    - run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
    - run: docker push your-dockerhub-username/nodejs-app
