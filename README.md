# PontoPortaria - Sistema de Controle de Ponto para Portarias e Condomínios

Sistema web estático (client-side) para registro e gestão de ponto de funcionários de portaria e condomínio (Porteiros, Vigilantes, Zeladores e Recepcionistas), pronto para hospedagem direta no **GitHub Pages**.

---

## 🚀 Publicação no GitHub Pages

Este projeto foi desenvolvido sem dependências de Node.js, Express, npm ou servidores locais. Toda a lógica de negócio, interface gráfica, validação de regras e banco de dados mock em memória funcionam diretamente no navegador.

### Passo a Passo para Publicar:

1. Acesse o repositório no **GitHub**.
2. Vá até a aba **Settings** (Configurações) do repositório.
3. No menu lateral esquerdo, clique em **Pages**.
4. Em **Build and deployment**:
   - **Source**: Selecione `Deploy from a branch`.
   - **Branch**: Selecione a branch principal (ex: `main`) e a pasta `/ (root)`.
5. Clique em **Save**.
6. Aguarde a publicação. O site estará disponível no endereço fornecido pelo GitHub Pages (ex: `https://seu-usuario.github.io/seu-repositorio/`).

---

## 📁 Estrutura de Arquivos

- **`index.html`**: Página inicial do sistema com navegação entre Totem Tablet e Painel Gerencial.
- **`app.js`**: Regras de negócio, manipulação do DOM e cliente de API (com fallback de armazenamento em memória local ou integração opcional com Supabase).
- **`styles.css`**: Estilização responsiva Vanilla CSS (Clean UI).
- **`schema.sql`**: Script SQL para criação de tabelas e dados seed no Supabase (opcional).
- **`backlog.md`**: Histórico completo de versões, funcionalidades e alterações do sistema.

---

## 💼 Funcionalidades Principais

- **Totem Tablet (Portaria)**:
  - Registro de batida por matrícula ou seleção rápida.
  - Horário em tempo real e captura facial via webcam/camera.
  - Regra de tolerância de entrada (5 min para Porteiro, 10 min para os demais).
  - Controle de rondas de segurança para Vigilantes (`HORA_EXTRA_RONDA`).
  - Bloqueio de saída para Zelador e Recepcionista com base no status do Controle de Chaves.
  - Emissão de ticket/comprovante com hash de autenticidade único.

- **Painel Gerencial**:
  - Abertura e fechamento do Controle de Chaves do dia.
  - Banner de alertas em tempo real para atrasos críticos de portaria.
  - Consulta de Espelho de Ponto consolidado com totais e histórico de batidas.
  - Registro de justificativas de ausências e atestados.
  - Validação de autenticidade de tickets de ponto via Hash.