Seção 1

1.🔹 RUN e layers: cada RUN cria uma layer. Usar && junta comandos → menos layers.
🔹 Impacto: menos layers = imagem menor e melhor uso do cache (especialmente limpando arquivos no mesmo RUN).
🔹 docker history: mostra as layers, tamanho e comandos → serve para verificar se a imagem foi otimizada.
🔹 .dockerignore: evita enviar arquivos desnecessários/sensíveis no build → melhora performance e segurança.
Ex: .git, debug.log, .env

2.🔹 Bridge padrão (bridge):
Containers recebem IPs dinâmicos (ex: 172.17.0.x) que mudam ao reiniciar
❌ Não possui resolução de nomes (DNS) automática
Comunicação depende de IP → instável para produção
🔹 Bridge customizada:
Docker cria uma rede isolada com DNS automático embutido
Containers se comunicam pelo nome do serviço/container (ex: db, api)
✔ Não importa se o IP muda → o nome continua funcionando

3.🔹 Infraestrutura como Código (IaC) no Docker:
É tratar a “oficina” (containers, redes, volumes) como código versionado, usando arquivos como docker-compose.yml para definir tudo.
🔹 Imperativo (manual):
Vários docker run → você monta a oficina peça por peça, comando por comando (mais erro e difícil de repetir).
🔹 Declarativo (YAML):
No docker-compose.yml você descreve o estado final (ex: app + banco + rede) e o Docker monta tudo com um comando (docker compose up).
🔹 Vantagens (reprodutibilidade):
Mesmo ambiente em qualquer máquina
Menos erros humanos
Fácil versionar (Git)
Setup rápido (um comando)

Seção 2

# 🚀 Ambiente Docker - Python + Redis

## 📦 Subir o ambiente (background)
```bash
docker compose up -d --build

Ver logs em tempo real
docker compose logs -f

Limpeza do ambiente

Parar containers:

docker compose down


Remover tudo (containers + rede):

docker compose down --remove-orphans


Remover também o volume (⚠️ apaga dados):

docker compose down -v
