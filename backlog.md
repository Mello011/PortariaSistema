# Backlog do Projeto - Sistema de Controle de Ponto (Portaria)

Este arquivo registra continuamente todas as funcionalidades implementadas, corrigidas ou alteradas no sistema de ponto da portaria/condomínio.

---

## 📌 Registros de Alterações

### [Versão 1.0.0] - Implementação Completa
- [x] **Criação do arquivo de registro `backlog.md`**: Estrutura inicial e controle incremental de tarefas.
- [x] **Modelagem de Banco de Dados (`schema.sql`)**:
  - Tabelas de `jornadas_trabalho`, `funcionarios`, `controle_chaves`, `rondas_em_andamento`, `registros_ponto` e `ocorrencias`.
  - Dados de Seed para os cargos exigidos: Portaria (Porteiro), Segurança (Vigilante - Rondas), Zeladoria (Zelador) e Recepção (Recepcionista).
- [x] **Interface e Experiência do Usuário (HTML5/CSS3 Vanilla)**:
  - Layout Clean UI (`#FFFFFF`), responsivo com foco em Tablets e Desktop.
  - Uso estrito de ícones vetoriais **Lucide Icons** via CDN (sem emojis na interface).
  - Componentes de navegação entre Totem Tablet e Painel Gerencial.
- [x] **Integracão Supabase e APIs do Sistema (`app.js`)**:
  - Inicialização do cliente Supabase via CDN com fallback para motor local em memória.
  - Implementação do endpoint `POST /ponto/registrar`:
    - Validação de tolerância na entrada por cargo (5 minutos para Portaria, 10 minutos para demais).
    - Disparo automático de ocorrência/alerta no painel do gerente em caso de atraso na Portaria.
    - Regra de virada de meia-noite (`data_referencia_turno`) vinculando a saída à data de entrada do turno.
    - Condicionamento de saída da Zeladoria e Recepção à devolução/fechamento do controle de chaves no sistema, com suporte a Override Gerencial e `SAIDA_FORCADA_EMERGENCIA`.
    - Classificação automática de `HORA_EXTRA_RONDA` para vigilantes com rondas em andamento.
    - Geração de hash único de comprovante para cada batida.
  - Implementação do endpoint `GET /ponto/comprovante/:hash`: Validação de autenticidade de tickets emitidos.
  - Implementação do endpoint `POST /ocorrencias/justificar`: Registro e anexação de comprovantes/atestados de ausências ou saídas forçadas.
  - Implementação do endpoint `GET /funcionarios/:id/espelho`: Exibição consolidada do histórico de batidas e inconsistências.
- [x] **Recursos Nativos**:
  - Câmera (`navigator.mediaDevices.getUserMedia`) para validação e captura facial no tablet.
  - Geolocalização (`navigator.geolocation`) para validação de raio (Geofencing) no aplicativo.

### [Versão 2.0.0] - Retema: Pizzaria → Portaria/Condomínio
- [x] **Rebranding completo da interface**: nome do sistema alterado de `PontoPizzaria` para `PontoPortaria`; paleta de cores migrada de tons quentes (laranja/dourado) para azul-marinho institucional, alinhado ao universo de portaria/segurança predial.
- [x] **Reclassificação de cargos** (mantendo a mesma lógica de negócio):
  - `PIZZAIOLO` (Cozinha) → `PORTEIRO` (Portaria/Guarita) — tolerância crítica de 5 min mantida, com alerta ao síndico/gerente em caso de atraso.
  - `ENTREGADOR` (Motoboy) → `VIGILANTE` (Segurança/Rondas) — saída flexível mantida; ocorrência `HORA_EXTRA_ENTREGA` renomeada para `HORA_EXTRA_RONDA`, disparada quando há ronda de segurança em andamento no fim do turno.
  - `CAIXA` → `ZELADOR` — regra de bloqueio de saída mantida, agora condicionada à devolução/fechamento do **Controle de Chaves** (antes "fechamento do caixa").
  - `ATENDENTE` → `RECEPCIONISTA` — mesma regra de bloqueio de saída da Zeladoria.
- [x] **Banco de dados**: tabela `status_caixa` renomeada para `controle_chaves`; tabela `entregas_em_andamento` renomeada para `rondas_em_andamento`; coluna `exige_fechamento_caixa` renomeada para `exige_fechamento_chaves`; horários de jornada ajustados para escalas típicas de portaria/segurança predial (incluindo turno noturno do Vigilante cruzando a meia-noite).
- [x] **Código (`app.js`)**: funções e variáveis renomeadas para refletir o novo domínio (`toggleStatusChaves`, `updateChavesUI`, `updatePorteiroAlerts`, `mockStore.statusChaves`, `rondaEmAndamento`, etc.), sem alteração nas regras de negócio originais.
- [x] **Dados de exemplo (seed)**: colaboradores fictícios renomeados para refletir os novos cargos (Porteiro, Vigilante, Zelador, Recepcionista).
