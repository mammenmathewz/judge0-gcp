# Judge0 Deployment for Octaview SaaS

This repository contains a **self-hosted Judge0** instance deployed on **Google Cloud Platform (GCP)**. Judge0 is an open-source **online code execution system** that powers **Octaview's** coding assessments and interview automation.

---

## 🚀 Features

- Supports multiple programming languages
- Secure and isolated code execution
- Scalable deployment on **GCP Compute Engine**
- Integrated into **Octaview B2B SaaS** for real-time evaluations

---

## 📌 Deployment Setup

### 1️⃣ Prerequisites

Ensure you have the following installed:

```sh
- Docker & Docker Compose
- Google Cloud SDK (gcloud CLI)
- A running GCP Compute Engine instance
```

### 2️⃣ Clone the Repository

```sh
git clone https://github.com/mammenmathewz/judge0-octaview.git
cd judge0-octaview
```

### 3️⃣ Environment Variables

Create a `.env` file and configure necessary variables:

```sh
JUDGE0_TELEMETRY_ENABLE=false  # Disable telemetry
REDIS_HOST=localhost
POSTGRES_USER=judge0
POSTGRES_PASSWORD=yourpassword
POSTGRES_DB=judge0
```

### 4️⃣ Start Judge0 with Docker

```sh
docker-compose up -d
```

### 5️⃣ Verify the Deployment

After deployment, check if Judge0 is running:

```sh
curl http://localhost:2358/languages
```

Expected Output:

```json
[
  {"id": 1, "name": "C (GCC 9.2.0)", "version": "9.2.0"},
  {"id": 2, "name": "C++ (GCC 9.2.0)", "version": "9.2.0"}
]
```

---

## ⚡ API Usage

### 🔹 Submit Code for Execution

```sh
curl -X POST "http://localhost:2358/submissions" \
     -H "Content-Type: application/json" \
     -d '{
           "language_id": 4,
           "source_code": "print(\"Hello, Octaview!\")",
           "stdin": ""
         }'
```

### 🔹 Retrieve Execution Result

```sh
curl -X GET "http://localhost:2358/submissions/{TOKEN}"
```

Replace `{TOKEN}` with the actual token received from the submission request.

---

## 🛠 Configuration

You can customize **Judge0** by modifying the `config` files in this repository.

For example, to adjust memory limits, update:

```sh
vi config/default.conf
```

Change:

```sh
MAX_MEMORY=512MB
MAX_TIME=10s
```

---

## 📡 Logging & Monitoring

To check logs:

```sh
docker logs -f judge0
```

---

## 🔒 Security Notes

- **Firewall Rules**: Ensure your **GCP VM firewall** allows only necessary traffic.
- **Sandboxing**: Execution is containerized to prevent security risks.

---

## 📝 License

This project is licensed under **MIT License**, while Judge0 itself follows its respective **license terms**.

---

## 👨‍💻 Maintainers

This Judge0 instance is maintained by **Mammen Mathew** for **Octaview SaaS**. Feel free to contribute or report issues!

---

### 🌟 Star this repo if you found it useful!
