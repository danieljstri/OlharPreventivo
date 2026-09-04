# Olhar Preventivo - Sistema de Controle de Extintores com AR

Bem-vindo ao repositório do **Olhar Preventivo**, um Sistema de Controle de Extintores de Incêndio com suporte a Realidade Aumentada (AR).

Este projeto tem como objetivo digitalizar e otimizar o controle de extintores de incêndio (inicialmente desenhado para instalações de grande porte como portos), garantindo rastreabilidade e conformidade com as normas **NBR 12962** e **NBR 12693**. 

O principal diferencial do sistema é o uso de **Realidade Aumentada (AR)** e **OCR (Reconhecimento Óptico de Caracteres)** através da câmera do dispositivo móvel do usuário (celular ou tablet). Ao apontar a câmera para a etiqueta padrão do extintor, o sistema lê o número de série e projeta um *overlay* na tela informando instantaneamente o status do equipamento, validade da carga, última e próxima inspeção, eliminando a necessidade de QR Codes adicionais.

## 🚀 Principais Funcionalidades

- **Identificação via AR/OCR**: Escaneamento de etiquetas de extintores em tempo real direto pela câmera, com feedback visual em Realidade Aumentada.
- **Gestão Completa de Extintores**: Cadastro de extintores georreferenciados, hierarquia de locais (unidade, áreas, pavimento).
- **Inspeções e Checklist**: Registro de inspeções (1º, 2º e 3º níveis) com assinatura digital e suporte a uso **Offline** (sincronização automática quando a rede retorna).
- **Alertas e Notificações**: Trabalhador (worker) integrado para disparar alertas automáticos por e-mail quando extintores estão próximos do vencimento.
- **Dashboards e Relatórios**: Exportação de relatórios de conformidade (PDF/Excel) prontos para envio ao Corpo de Bombeiros (AVCB).
- **Perfis de Acesso (RBAC)**: Controle de acesso granular entre Brigadista, Técnico, Gestor e Administrador.

## 🏗 Arquitetura e Tecnologias

O sistema utiliza o padrão de **Monolito Modular** no backend e uma Single Page Application (SPA) convertida para PWA no frontend, totalmente orquestrados em contêineres Docker.

### Backend
- **Node.js** com **Fastify**: Alta performance para APIs RESTful.
- **Prisma ORM**: Modelagem de dados, type-safety e migrations.
- **PostgreSQL**: Banco de dados relacional robusto.
- **Redis**: Cache em memória para sessões e otimização da rota de AR.
- **Zod**: Validação rigorosa de dados.
- **Arquitetura**: Controller-Service-Repository e validações defensivas.

### Frontend
- **Vue 3** com **Vite**: Reatividade e build super-rápido.
- **Tesseract.js**: Processamento de OCR isolado em Web Worker.
- **PWA (Progressive Web App)**: Service Workers e IndexedDB para suporte offline (essencial em áreas industriais).
- **Vee-Validate**: Validação de formulários no lado do cliente.

### Infraestrutura
- **Docker e Docker Compose**: Instalação reproduzível com um único comando.
- **Nginx**: Proxy reverso gerenciando requisições estáticas e da API.
- **Object Storage (R2/S3)**: Armazenamento seguro de fotos, certificados PDF e plantas baixas.

## 🛠 Como Instalar (Ambiente de Produção/Homologação)

O projeto é distribuído integralmente via Docker, não sendo necessária a instalação de Node.js ou PostgreSQL na máquina host.

**Pré-requisitos:**
- Servidor Linux (Ubuntu 22.04+ recomendado)
- Git (2.30+)
- Docker Engine (24.0+) e Docker Compose (2.20+)

**Passo a passo:**

1. Clone o repositório:
```bash
git clone https://github.com/danieljstri/OlharPreventivo.git
cd OlharPreventivo
```

2. Configure as variáveis de ambiente baseadas nos arquivos de exemplo:
```bash
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
```
*(Certifique-se de configurar a variável `VITE_API_URL` no frontend e os dados de banco e JWT no backend)*

3. Inicialize os contêineres:
```bash
docker compose -f docker/docker-compose.prod.yml build
docker compose -f docker/docker-compose.prod.yml up -d
```

4. Aplique as migrations e carregue os dados iniciais do sistema:
```bash
docker compose exec backend npx prisma migrate deploy
docker compose exec backend npx prisma db seed
```

## 📚 Manuais
O sistema conta com um Manual do Usuário detalhado cobrindo o uso da câmera AR, registro de inspeções e geração de relatórios, que pode ser consultado na documentação oficial anexada aos releases do projeto.

---
**Desenvolvido para garantir máxima segurança e agilidade preventiva.**
