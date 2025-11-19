# 🚀 Production-Grade CI/CD Pipeline Stack

A complete, production-ready CI/CD infrastructure stack featuring monitoring, logging, security scanning, and secrets management. Built for local development but cloud-ready.

## 🎯 What This Is

This is a **reusable template** for setting up a complete DevOps infrastructure locally using Docker. Once set up, you can plug ANY project into this pipeline and get:

- ✅ Automated CI/CD with Jenkins
- ✅ Real-time monitoring with Prometheus & Grafana
- ✅ Centralized logging with ELK Stack
- ✅ Code quality scanning with SonarQube
- ✅ Container security scanning with Trivy
- ✅ Secrets management with Vault
- ✅ Alert management with AlertManager

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **CI/CD** | Jenkins + BlueOcean | Pipeline orchestration |
| **Monitoring** | Prometheus + Grafana + Node Exporter | Metrics collection & visualization |
| **Logging** | ELK Stack (Elasticsearch, Logstash, Kibana) | Centralized log aggregation |
| **Code Quality** | SonarQube | Static code analysis & security |
| **Secrets** | HashiCorp Vault | Secrets management |
| **Alerts** | AlertManager | Alert routing & management |
| **Reverse Proxy** | NGINX | Unified access point |

## 📋 Prerequisites

- **Docker Desktop** (Windows/Mac) or Docker Engine (Linux)
- **WSL2** enabled (for Windows)
- **Git**
- **Minimum 16GB RAM** (32GB+ recommended)
- **20GB+ free disk space**

## 🚀 Quick Start

### 1. Clone this repository
```bash
git clone https://github.com/YOUR_USERNAME/cicd-production-stack.git
cd cicd-production-stack
```

### 2. Start the entire stack
```bash
docker-compose pull
docker-compose up -d
```

### 3. Access the services

Wait 2-3 minutes for everything to initialize, then access:

| Service | URL | Default Credentials |
|---------|-----|---------------------|
| **Jenkins** | http://localhost:8080 | Get password: `docker exec production-jenkins cat /var/jenkins_home/secrets/initialAdminPassword` |
| **Grafana** | http://localhost:3000 | admin / admin123 |
| **Prometheus** | http://localhost:9090 | No auth |
| **SonarQube** | http://localhost:9000 | admin / admin (change on first login) |
| **Kibana** | http://localhost:5601 | No auth |
| **Vault** | http://localhost:8200 | Token: root-token-change-me |

## 📁 Project Structure
```
cicd-production-stack/
├── docker-compose.yml           # Main orchestration file
├── jenkins/
│   ├── shared-libraries/        # Reusable pipeline code
│   ├── pipelines/               # Language-specific Jenkinsfiles
│   └── jobs/                    # Job DSL for automation
├── monitoring/
│   ├── prometheus/              # Metrics configuration
│   ├── grafana/                 # Dashboards
│   └── alertmanager/            # Alert rules
├── security/
│   ├── sonarqube/               # Code quality config
│   ├── trivy/                   # Container scanning
│   └── vault/                   # Secrets config
├── logging/
│   ├── elasticsearch/           # Search & storage
│   ├── logstash/                # Log processing
│   └── kibana/                  # Visualization
└── docs/                        # Documentation
```

## 🎓 How to Use This for Your Projects

1. **Start this infrastructure** (once, runs 24/7)
2. **Copy the appropriate Jenkinsfile** template for your project language
3. **Customize 5-10 lines** (app name, test commands, etc.)
4. **Push to Git** → Jenkins automatically picks it up
5. **Watch your pipeline run** with full monitoring!

## 🔒 Security Notes

**⚠️ CRITICAL: Change default passwords before production use!**

Default credentials are for **LOCAL DEVELOPMENT ONLY**. For production:

1. Change all passwords in `.env` file
2. Enable HTTPS on NGINX
3. Set up proper authentication
4. Rotate Vault tokens
5. Configure firewall rules

## 📊 Monitoring & Alerts

### Grafana Dashboards

Pre-configured dashboards for:
- Jenkins pipeline metrics
- System resources (CPU, RAM, Disk)
- Docker container stats
- Application-specific metrics

### Prometheus Alerts

Alerts configured for:
- High CPU/Memory usage (>80%)
- Jenkins down (>2 minutes)
- Build failures (>3 in 1 hour)
- Disk space low (<10%)

## 🐛 Troubleshooting

### Services won't start?
```bash
# Check logs
docker-compose logs -f [service-name]

# Restart a specific service
docker-compose restart [service-name]

# Full reset (⚠️ deletes all data)
docker-compose down -v
docker-compose up -d
```

### Out of memory?
```bash
# Check resource usage
docker stats

# Reduce services (comment out in docker-compose.yml)
# Start with just Jenkins + Prometheus + Grafana
```

### Port conflicts?

Edit `docker-compose.yml` and change the port mappings:
```yaml
ports:
  - "8081:8080"  # Change 8080 to something else
```

## 🤝 Contributing

This is a personal learning project, but suggestions welcome!

## 📝 License

MIT License - Use freely for learning and personal projects

---

**⭐ Star this repo if it helped you!**