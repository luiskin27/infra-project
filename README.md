# Infra project
Repository for midterm DevOps.
Edited from GitHub UI.
neo@neo-VirtualBox:~/infra-project$ git pull
git log --oneline
Already up to date.
6a8deac (HEAD -> main, origin/main) Merge pull request #1 from luiskin27/feature/ansible-curl
190f1d9 feat(ansible): install curl package
990be1a Update README.md
8bb60a6 merge: resolve app_port conflict
6279062 fix(ansible): change app port to 8000
ddb9802 (fix/app-port) fix(ansible): change app port to 9090
3bc6ab6 feat(docker): add healthcheck instruction
1b0d30f docs: clean up readme text
e5420cb docs: add project description
dfc522f Update README.md
273673b feat: add ansible playbooks
b1cb15c feat: add docker files
364edcd docs: add readme and env example
4888407 chore: add gitignore so extra files dont leak

## Запуск в Docker
```bash
docker build -t infra-web:1.0 docker/
docker run -d --name infra-web -p 8080:80 infra-web:1.0
curl http://localhost:8080
docker rm -f infra-web
