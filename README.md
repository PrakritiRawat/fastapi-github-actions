# FastAPI Dockerized Application with GitHub Actions

## 📌 Overview
This project demonstrates Continuous Delivery by automating the creation and deployment of a **Dockerized FastAPI application** using **GitHub Actions**.

---

## 🚀 Installation & Running Locally

### **1️⃣ Clone the Repository**
```sh
git clone https://github.com/kriti0917/your-repo-name.git
cd your-repo-name
```

### **2️⃣ Install Dependencies**
Make sure you have Python and `pip` installed. Then, install dependencies:
```sh
pip install -r requirements.txt
```

### **3️⃣ Run the FastAPI Server**
```sh
uvicorn main:app --host 0.0.0.0 --port 8000
```

### **4️⃣ Test the API**
Open your browser or use **Postman** to test:
```
http://localhost:8000
```
Or check the interactive Swagger docs:
```
http://localhost:8000/docs
```

---

## 🐳 Running with Docker

### **1️⃣ Build the Docker Image**
```sh
docker build -t fastapi-app .
```

### **2️⃣ Run the Docker Container**
```sh
docker run -p 8000:8000 fastapi-app
```

### **3️⃣ Access the API**
Go to:
```
http://localhost:8000
```

---

## 🔄 GitHub Actions Workflow Explanation

The **GitHub Actions** workflow automates the process of building and pushing the Docker image to **Docker Hub**.

### **Workflow Trigger**
- Runs automatically **on every `push`** to the repository.

### **Steps in `.github/workflows/DockerBuild.yml`**
1. **Checkout Code**
2. **Login to Docker Hub** using secrets (`DOCKER_USERNAME` and `DOCKERTOKEN`).
3. **Build the Docker Image**
4. **Push the Image to Docker Hub**

#### **Workflow File:**
```yaml
name: Docker Image Build

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - name: Build & Push Image
        run: |
          echo ${{ secrets.DOCKERTOKEN }} | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
          docker build -t ${{ secrets.DOCKER_USERNAME }}/fastapi-app:latest .
          docker push ${{ secrets.DOCKER_USERNAME }}/fastapi-app:latest
```

---

## 🔑 Setting Up Docker Token and Secrets
To authenticate **GitHub Actions** with **Docker Hub**, follow these steps:

### **1️⃣ Generate a Docker Token**
1. Log in to [Docker Hub](https://hub.docker.com/)
2. Go to **Account Settings → Security → Access Tokens**
3. Click **Generate Token** and copy the token

### **2️⃣ Add Secrets to GitHub**
1. Go to your repository on **GitHub**
2. Click on **Settings → Secrets and variables → Actions → New repository secret**
3. Add the following secrets:
   - **DOCKER_USERNAME** = `your-docker-hub-username`
   - **DOCKERTOKEN** = `your-generated-docker-token`

---

## 📌 Submission Details
### **GitHub Repository**
🔗 [GitHub Repo](https://github.com/kriti0917/your-repo-name)

### **Docker Hub Image**
🔗 [Docker Hub Link](https://hub.docker.com/r/kriti0917/fastapi-app)

---

✅ **Now, every push to GitHub will automatically build and deploy the Docker image!** 🚀

