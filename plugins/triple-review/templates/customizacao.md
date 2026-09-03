# Customização do projeto — /triple-review (overlay)

Copie este arquivo para `docs/triple-review-tuning/customizacao.md` **no seu projeto** e preencha.
Os agentes do triple-review leem estas seções em runtime. Os títulos `##` são FIXOS (os agentes
os citam pelo nome) — não renomeie. Sem este arquivo a skill funciona, mas com defaults genéricos:
sem regras críticas de domínio, sem convenções próprias, com perfis de usuário deduzidos.

## Stack

<!-- Declare o stack real (framework, versões, front, banco). Complementa a detecção automática. -->
- Ex: Laravel 10 / PHP 8.1 / Blade / MySQL 8

## Regras críticas do domínio (QA)

<!-- Regras de negócio cujo bypass é GRAVE. Alimentam o conjunto CRIT da Etapa 0 do QA,
     os exemplos dos itens QA-BLOCK-* e a decisão de severidade [BLOCKER]. Seja específico:
     tabelas, fluxos obrigatórios, operações irreversíveis, mecanismo de permissão. -->
- Ex: nunca gravar direto na tabela X — sempre via fluxo Y
- Ex: operações do tipo Z são irreversíveis — nunca emitir reversão automática
- Ex: permissões via middleware/policy W em toda rota nova
- Exemplos de duplicidade proibida (QA-BLOCK-03): ...
- Exemplos de estado inconsistente (QA-BLOCK-05): ...
- Comandos proibidos no projeto (ex: suíte de teste que reseta banco): ...

## Precisão numérica (QA-FRONT-07)

<!-- Padrão decimal de campos monetários/saldo/quantidade. -->
- Ex: decimal(18,4) em campos de saldo

## Convenções de código (Sênior — itens SR-CONV do projeto)

<!-- Cada linha é um item de checklist com ID estável (SR-CONV-01, 02, ...; pule o 09, que é
     genérico e vive no base). Marque com (crítica) as convenções cuja violação é [BLOCKER].
     Termine cada item com a condição de N/A. -->
- `SR-CONV-01` — ...
- `SR-CONV-02` **(crítica)** — ...

## Perfil dos usuários (UX)

<!-- Quem usa o sistema, em que condição física/operacional, com que nível de treinamento.
     2 a 4 perfis. A Etapa 0 do Gerente UX mapeia cada superfície para um destes perfis. -->
- **Perfil A**: ...
- **Perfil B**: ...

## Padrões visuais e de interação (UX — UX-CONSIST-02 / UX-TOUCH-01)

<!-- Padrões de UI que o projeto exige (botões, modais, mensagens) e quais superfícies são
     touch/mobile (para o item de alvo de toque). Sem padrões declarados, UX-CONSIST-02 fica N/A. -->
- Ex: botões de ação na ordem Visualizar → Editar → Excluir, com classes X/Y/Z
- Superfícies touch (UX-TOUCH-01): ...

## Ambiente de navegação (E2E)

<!-- Sem esta seção, QA e UX revisam sem abrir a tela: os itens QA-E2E-* e UX-E2E-* saem N/A
     e a revisão perde a classe de defeito que só aparece no browser (tela em branco, botão
     que não dispara, erro de JS). Exige o servidor MCP Playwright configurado:
     claude mcp add playwright -s user -- npx @playwright/mcp@latest --headless --isolated -->

- **Base URL**: ex. `http://127.0.0.1:8000`
- **Como subir a aplicação**: ex. `php artisan serve --port=8000` (rodar a partir da raiz do repo)
- **Rota de smoke test** (tela leve que prova que o ambiente respondeu): ex. `/login`
- **Fluxo de login**: ex. abrir `/login`, preencher os campos `usuario` e `password`, submeter
- **Credenciais de teste**: ex. `usuario_teste` / `senha_teste`
  <!-- Use um usuário dedicado de automação, nunca credencial pessoal. -->
- **Estratégia de limpeza para fluxos que gravam**: descreva como desfazer o que um teste
  criar (dump/restore, limpeza por ID, registro de sandbox). **Se não houver estratégia,
  escreva "nenhuma — apenas fluxos de leitura"**: os agentes param antes de qualquer
  gravação. Navegação é irreversível; não existe transação envolvendo um clique.

## Acesso ao banco

<!-- Como consultar o banco em modo LEITURA (o comando exige read-only sempre).
     Se não houver banco acessível, escreva "indisponível" — os itens de verificação
     em banco sairão como N/A — não verificável. -->
- Ex: MySQL 8, credenciais no .env (DB_HOST, DB_DATABASE, DB_USERNAME, DB_PASSWORD)
