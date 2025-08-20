# Docker commands
build
```bash
docker build -t devops-final-order .
```

image security scanning
```bash
trivy image devops-final-order
```

run
```bash
docker run -d -p 3002:3002 --name devops_final_order --env-file .env devops-final-order
```

tag
```bash
docker tag devops-final-order denture8278/devops-final-order:v1.0
docker tag devops-final-order denture8278/devops-final-order:latest
```

push
```bash
docker push denture8278/devops-final-order:v1.0
docker push denture8278/devops-final-order:latest
```