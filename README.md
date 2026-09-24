# Olhar Preventivo - Sistema de Validação de Projetos de Combate a Incêndio

Bem-vindo ao repositório do **Olhar Preventivo**, uma plataforma digital voltada para a auditoria, vistoria e validação de conformidade de **Projetos de Prevenção e Combate a Incêndio** aprovados pelo Corpo de Bombeiros (PPCI / AVCB).

---

## 🎯 Visão Geral do Novo Escopo

O projeto expandiu seu escopo original (que era focado exclusivamente em extintores) para contemplar **todos os sistemas e medidas de segurança contra incêndio e pânico** de uma edificação ou instalação industrial, tais como:

- Extintores de Incêndio (portáteis e sobre-rodas);
- Sistemas de Hidrantes e Mangotinhos;
- Iluminação de Emergência;
- Sinalização de Emergência e Rotas de Fuga;
- Sistemas de Alarme e Detecção de Fumaça/Calor;
- Chuveiros Automáticos (*Sprinklers*);
- Portas Corta-Fogo e Compartimentação;
- Saídas de Emergência e Pressurização de Escadas.

O principal objetivo é permitir que técnicos, engenheiros e bombeiros civis façam a validação em campo confrontando **o que foi aprovado no projeto técnico** com o que está **efetivamente instalado no local**, garantindo conformidade com as normas técnicas vigentes e agilidade nas inspeções periódicas.

---

## 📅 Roadmap de Desenvolvimento (3 Sprints)

O desenvolvimento está estruturado em 3 fases principais:

### 🔹 Sprint 1: Sistema Base e Formulários de Vistoria
- **Estrutura Base do Sistema:** Autenticação, controle de perfis de acesso (RBAC) e arquitetura modular da aplicação.
- **Modelagem de Projetos e Edificações:** Cadastro das instalações, plantas e projetos técnicos aprovados.
- **Formulários e Checklists de Vistoria:** Interface e lógica para preenchimento dos dados de inspeção de cada medida de segurança (especificações, conformidade física, validades, avarias, etc.).
- **Suporte Offline (PWA):** Capacidade de preenchimento dos formulários mesmo sem conectividade com a internet, sincronizando os dados quando a conexão for restabelecida.

### 🔹 Sprint 2: Planta Geral e Geolocalização em Tempo Real
- **Mapeamento na Planta Geral:** Visualização gráfica interativa da planta da edificação com os pontos e itens de combate a incêndio georreferenciados.
- **Geolocalização / Posicionamento do Usuário:** Leitura da localização do dispositivo móvel do vistoriador no espaço da edificação.
- **Chaveamento Automático:** Conforme o usuário caminha pela instalação, o sistema identifica em qual ponto/item ele está fisicamente próximo e abre automaticamente a tela de vistoria correspondente àquele equipamento.

### 🔹 Sprint 3: Realidade Aumentada (AR) e Reconhecimento
- **Interface com Realidade Aumentada (AR):** Projeção de dados sobre a imagem da câmera em tempo real ao mirar nos equipamentos e pontos de combate a incêndio.
- **Comparativo Visual Projeto vs. Realidade:** Exibição de *overlays* informando se o item encontrado no local corresponde exatamente ao especificado no projeto aprovado.
- **Reconhecimento Inteligente / OCR:** Identificação automática de etiquetas, seriais e placas para validação instantânea sem necessidade de entrada manual de dados.

---

## 🏗 Arquitetura e Tecnologias

O sistema segue o padrão de **Monolito Modular** no backend e uma Single Page Application (**SPA/PWA**) no frontend, orquestrados via contêineres Docker.

### Backend
- **Node.js** com **Fastify**: Alta performance para processamento e APIs RESTful.
- **Prisma ORM**: Modelagem de dados, migrations e tipagem estrita.
- **PostgreSQL**: Banco de dados relacional robusto para projetos, plantas e vistorias.
- **Redis**: Cache em memória para otimização de sessões e rotas de localização/AR.
- **Zod**: Validação rigorosa de esquemas de dados.

### Frontend
- **Vue 3** com **Vite**: Interface reativa, modular e de carregamento rápido.
- **PWA (Progressive Web App)**: Service Workers e IndexedDB para operação em áreas sem sinal.
- **Bibliotecas de Georreferenciamento e Canvas/SVG**: Manipulação interativa de plantas baixas.
- **Tesseract.js / Web Workers**: Processamento de imagem e OCR no dispositivo do cliente.

### Infraestrutura
- **Docker e Docker Compose**: Ambiente de desenvolvimento e produção padronizado.
- **Nginx**: Proxy reverso gerenciando tráfego e distribuição estática.
- **Object Storage (S3/R2)**: Armazenamento seguro de plantas, fotos de evidências e relatórios gerados.

---

## 🛠 Como Executar Localmente

### Pré-requisitos
- Docker Engine (24.0+) e Docker Compose (2.20+)
- Git

### Inicialização
1. Configure as variáveis de ambiente:
   ```bash
   cp backend/.env.example backend/.env
   cp frontend/.env.example frontend/.env
   ```

2. Suba os contêineres:
   ```bash
   docker compose -f docker/docker-compose.prod.yml up -d --build
   ```

3. Execute as migrations do banco de dados:
   ```bash
   docker compose exec backend npx prisma migrate deploy
   ```

---
*Olhar Preventivo — Da aprovação à vistoria em campo com tecnologia inteligente.*
