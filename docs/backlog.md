# Backlog

> Este arquivo é a fonte da verdade do backlog. O ClickUp é o lugar de gestão das tarefas e reflete o que está aqui.
>
> A Parte 1 diz como o backlog se escreve e como a história vira tarefa no ClickUp. A Parte 2 lista as pendências com terceiros e as decisões em aberto. A Parte 3 lista defeitos e dívida técnica. A Parte 4 traz os épicos. O registro dos códigos de história fica em `docs/registro-de-codigos-de-historia.md`.

---

## Parte 1 · Regras

### 1.1 Hierarquia e identificadores

| Nível | Identificador | O que é |
| --- | --- | --- |
| Épico | `É1` | Uma área do produto que serve ao objetivo dele. A ordem dos épicos não é a ordem de construção |
| Feature | `F1.1` | Um resultado que se entrega dentro do épico, descrito em uma frase |
| História | `E1-01` | Uma unidade de trabalho que cabe em um PR pequeno |

O `É` com acento no épico e o `E` sem acento na história são intencionais.

O código da história nunca é reaproveitado. A história nova recebe o número seguinte ao maior do épico em `docs/registro-de-codigos-de-historia.md`, e ganha a linha dela lá no mesmo PR que a escreve. O número da feature, o da pergunta da Parte 2 e o do defeito da Parte 3 não têm registro, e um número que falta na sequência é normal.

### 1.2 Só o que serve ao objetivo

- O backlog tem apenas os épicos e as features que servem ao objetivo do produto. Enquanto o `CLAUDE.md` não existe (E1-02), o objetivo é o de `docs/notes.md`: uma plataforma de live commerce que conecta indústrias e varejistas por transmissões ao vivo, com apresentação de produtos em combos, para gerar demanda e apoiar a venda entre empresas.
- Os épicos não são construídos um depois do outro. Cada sprint tem um objetivo, e as histórias que entram nela são as que cumprem esse objetivo, de um ou de vários épicos (§1.5).
- Toda feature tem uma frase que diz o que ela entrega e as histórias que a entregam, escritas no formato do §1.3. Quando as histórias de uma feature dependem umas das outras, a frase diz a ordem de construção e o motivo.
- A história que falta para cumprir o objetivo de uma sprint é escrita na preparação do planejamento.
- A história cabe em um PR pequeno, perto de 400 linhas, e termina em até uma semana. A que passa disso é dividida.
- Não entra história para necessidade que ainda não existe.

### 1.3 Como se escreve uma história

A história é lida por quem decide negócio e por quem implementa. Uma pessoa de negócio precisa entender qualquer história.

Regras de escrita, que valem para todo documento, tarefa, branch, commit e PR, e passam para `docs/diretrizes-de-desenvolvimento.md` quando ele for criado:

- Todo nome é literal: sem apelido, metáfora, jargão nem abreviação que precise de explicação. O termo técnico inevitável é explicado na primeira vez em que aparece.
- Um conceito tem um nome só, o da tabela de vocabulário do `CLAUDE.md` (E1-02).
- O teste do nome: quem não participou da decisão entende o nome sem abrir outro arquivo.
- Não se usa travessão como pontuação.

Toda história tem quatro partes, nesta ordem:

| Parte | Regra |
| --- | --- |
| Título | Diz o trabalho ou o resultado, de forma literal. Não conta uma cena e não usa apelido |
| História | Uma frase: "Como [pessoa], quero [ação], para [benefício]" |
| O que precisa ser feito | Uma a três frases no modelo "Precisa ser feito X, pois Y". O motivo é obrigatório |
| Critérios de aceite | Lista de condições verificáveis. Uma condição por critério. Sem adjetivo |

A história se explica sozinha. Referência a outro documento é complemento e nunca substitui a explicação.

**As pessoas deste produto** (conforme `docs/Enterprise B2B-.pdf` §2; a lista é confirmada na E1-02):

| Pessoa | Quem é |
| --- | --- |
| Admin | A equipe interna da LiveShop Turbo, que gerencia a plataforma, os clientes B2B e as lives de todos eles |
| Indústria | A empresa fornecedora que contrata a LiveShop Turbo, cria as lives e os combos e acompanha os resultados |
| Varejista | A empresa compradora que se cadastra, assiste à live e registra o interesse nos combos |
| Representante | O vendedor da indústria, que leva o varejista à live e dá sequência ao atendimento. Não tem acesso à plataforma: só assiste à live pelo link de exibição, sem interagir (resposta de 26/11/2026, `docs/inventario-do-sistema-original.md`, linha 3.4) |
| Equipe técnica | Quem desenvolve o produto. Usada na história que não muda o que as outras pessoas veem |

**Exemplos:**

| Ruim | Bom |
| --- | --- |
| "Ajustar o carrinho" | "Edição do carrinho salvo depois do fim da live" |
| "Precisa melhorar a live" (o que precisa ser feito) | "Precisa ser testada a API do Panda Video com duas transmissões ao mesmo tempo, pois o player é a peça que o varejista mais usa" |
| "O sistema deve ser rápido e confiável" (critério) | "Duas transmissões ao mesmo tempo são exibidas em duas páginas sem interferência" (critério) |

### 1.4 Critério de entrada e definição de pronto

- A história sem critério de aceite não entra em sprint.
- Só marca a história como concluída quem verificou os critérios, e nunca quem escreveu o código ou o documento. A verificação é do Tech Lead.
- A história está pronta quando: o trabalho foi revisado; um teste automático cobre a regra; os critérios de aceite foram verificados; a versão está publicada em homologação; e a documentação foi atualizada no mesmo PR. Enquanto não há homologação, a história que só entrega documento ou decisão está pronta quando o PR foi revisado e mesclado na `main`, os critérios de aceite foram verificados pelo Tech Lead e a linha dela em `docs/registro-de-codigos-de-historia.md` foi atualizada (decisão do Tech Lead de 27/11/2026).
- A história entregue sai inteira da Parte 4 no PR que a entrega. Ela não fica marcada como concluída nem resumida, e a linha dela em `docs/registro-de-codigos-de-historia.md` passa a dizer `entregue`. A história descartada sai do mesmo jeito, com o estado `descartada`.
- A feature sai quando o resultado que ela descreve foi entregue e nenhuma história dela continua aberta. O épico sai quando não sobra feature nele.
- O backlog guarda só o que falta fazer, para quem o lê não carregar o contexto do que já foi entregue. O trabalho entregue está no histórico do Git e no registro de códigos.

### 1.5 Sprint e objetivo da sprint

- A sprint dura duas semanas.
- Toda sprint tem um objetivo, definido na reunião de planejamento. O objetivo diz o resultado que a sprint entrega e o que precisa ser verdade para ele estar cumprido.
- Entram na sprint as histórias necessárias para cumprir o objetivo. História que não contribui para o objetivo fica no backlog.
- O objetivo, a prioridade e os sprint points são definidos na reunião de planejamento, no ClickUp. Eles não são escritos neste arquivo.

O objetivo se escreve neste formato:

```text
Objetivo N · O resultado da sprint, em uma frase

Uma a três frases: o que a sprint entrega e quando o objetivo está cumprido.

Entregas:
1. Um resultado verificável, com o código das histórias que o entregam (E1-02).
2. ...
```

A entrega diz o resultado, e não a atividade: "a `main` só recebe mudança por PR com verificação aprovada", e não "configurar o GitHub".

### 1.6 ClickUp

**Onde fica.** Na lista `Backlog Enterprise` do ClickUp (id `901114114159`), onde as tarefas deste projeto já estão. Essa lista também guarda as tarefas já concluídas do LiveShop Enterprise original, que têm códigos iguais aos deste projeto (`E1-01` a `E8-04` do original). A tarefa deste projeto se distingue pelo título, que é o da história neste arquivo. A pasta das listas de sprint é a pergunta da Parte 2 §2.3.

**Como a história vira tarefa:**

- Uma tarefa por história. Épico e feature não viram tarefa: aparecem na descrição. O critério de aceite não vira tarefa: é item de checklist dentro dela.
- A história nova entra na lista `Backlog Enterprise`. A história escolhida no planejamento vai para a lista da sprint.
- Defeito e dívida técnica ficam em lista separada das histórias (Parte 3).

**Campos da tarefa:**

| Campo | Conteúdo |
| --- | --- |
| Nome | `E1-01 · Título da história` |
| Descrição | Nesta ordem: `Épico: ...`, `Feature: ...`, a frase da história, o texto de "O que precisa ser feito" e os critérios de aceite como `- [ ]` |
| Tags | De uma a três, do vocabulário abaixo, com no máximo uma tag de área do produto e uma de superfície |
| Checklist | Os critérios de aceite, um por item e na mesma ordem da descrição |

**Tags, em três eixos:**

- **Área do produto:** nenhuma ainda. As tags deste eixo são criadas com o primeiro épico de produto, a partir do vocabulário do `CLAUDE.md` (E1-02).
- **Superfície:** nenhuma ainda. As tags deste eixo nomeiam as telas (por exemplo, o painel da indústria e a sala da live) e são criadas com a primeira história que tem tela.
- **Ofício:** `front-end`, `back-end`, `infraestrutura`, `testes e ci`, `integrações`, `segurança`, `documentação`, `limpeza`, `decisão`. São as tags que os outros projetos do time já usam no ClickUp.

Tag nova só entra quando nomeia algo que nenhuma tag existente nomeia.

**Como a tarefa entra no ClickUp:**

- O connector do ClickUp disponível hoje só lê tarefas. Por isso, a tarefa entra por um arquivo CSV gerado na pasta `reports/`, que não é versionada, e a importação é feita à mão. O arquivo é apagado depois da importação. A criação pela API do ClickUp passa a ser o padrão quando houver um token com permissão de criar tarefa na lista (Parte 2 §2.3).
- O CSV tem as colunas `Task Name`, `Description`, `Tags`, `Lista` e `Checklist`, e a coluna `Lista` leva `Backlog Enterprise`. Na coluna `Checklist`, cada item fica em uma linha, tem até 100 caracteres e não leva vírgula, ponto e vírgula nem barra vertical, porque o importador do ClickUp parte o campo nesses sinais. Por isso, o item do checklist pode ser uma versão mais curta do critério, e a descrição mantém o critério completo.

---

## Parte 2 · Pendências com terceiros e decisões em aberto

Item resolvido sai desta parte no PR que registra a resposta ou a decisão. A resposta é escrita no documento que a coluna "Resolve em" aponta.

### 2.1 Perguntas de produto

O PDF de regras (`docs/Enterprise B2B-.pdf`) só tem conteúdo nas seções 1 a 3. As seções de regras, dados, cálculos e requisitos têm só o título. As respostas abaixo mudam o modelo de dados e o escopo dos épicos seguintes.

| # | Pergunta | O que a documentação já diz | O que depende da resposta | Resolve em |
| --- | --- | --- | --- | --- |
| P5 | O que é o "ID único de acesso" de `docs/notes.md`: um código enviado por e-mail, um link pessoal, o e-mail ou o CPF da pessoa? A entrada do varejista continua sem senha? | O PDF §2.3 diz que o varejista entra no dia da live só com o CNPJ, sem senha | A forma de entrada do varejista e a tabela de acessos | E1-03 |
| P6 | Uma empresa, identificada pelo CNPJ, pode ser varejista de mais de uma indústria? | O original permite um varejista por CNPJ e por indústria, com condição registrada para rever a regra (ADR 0020 do original) | A separação entre a empresa e o acesso de cada pessoa | E1-03 |
| P7 | O varejista passa a comprar produto fora de combo? | O PDF §1.1 diz que os produtos são apresentados em combos | O carrinho e a vitrine da live | E1-03 |
| P8 | Até quando o carrinho salvo pode ser editado: só durante a live, por um prazo depois dela ou sem prazo? O carrinho salvo passa a ser o pedido, ou o varejista ainda confirma o envio? | O PDF §2.3 diz que o varejista confirma os dados antes de enviar a intenção de compra e não paga dentro da plataforma | O ciclo de vida do carrinho e do pedido | E1-03 |
| P9 | Quando o carrinho passa a contar como abandonado? Quantos lembretes são enviados, e por qual canal? | Nada | O envio de lembrete ao varejista | E1-03 |
| P10 | "Múltiplas transmissões ao vivo simultâneas" quer dizer várias lives ao mesmo tempo ou vários ângulos na mesma live? A conta do Panda Video é uma só, da LiveShop Turbo, ou uma por indústria? A plataforma cria a live pela API do Panda Video, ou a indústria cola o endereço? | O PDF §2.2 diz que a indústria insere a URL da transmissão no YouTube | O cadastro da live e o teste da E1-05 | E1-03 e E1-05 |
| P11 | O comentário anônimo é anônimo para os outros espectadores, com a plataforma sabendo quem escreveu, ou é feito sem entrada nenhuma? Quem modera: a indústria, o Admin ou só o filtro de palavras? A moderação acontece antes de o comentário aparecer ou depois, removendo? | Nada | O modelo do comentário e o envio em tempo real | E1-03 |
| P16 | O varejista só entra na live em que está cadastrado, ou entra em toda live da indústria em cuja base ele está? | Em 14/09/2026 o produto do original respondeu que "apenas alguém cadastrado naquela live possui acesso", e o código do original faz o contrário: vincula à live corrente todo varejista ativo da indústria (`docs/inventario-do-sistema-original.md`, linha 1.4) | Quem entra em cada live e a taxa de comparecimento da analytics. Dono: Tech Lead | E1-03 |
| P17 | O combo tem lista de produtos inclusos, desconto, os dois ou nenhum? | O PDF §3.3 lista "produtos inclusos" e "desconto" como dados do combo. O original tem as tabelas de produto e de item do combo sem nenhuma tela que as use, e não tem desconto (linha 5.3 do inventário) | O cadastro do combo e o cálculo do total do carrinho. Dono: Tech Lead | E1-03 |
| P18 | O Admin acompanha as lives e a analytics de todas as indústrias, ou só gerencia clientes e usuários? | O PDF §2.1 dá ao Admin acompanhar todas as lives, as métricas gerais e a analytics. No original o Admin só tem a tela de usuários (inventário, seção 2) | As telas e as permissões do Admin. Dono: Tech Lead | E1-03 |
| P19 | O número de WhatsApp do botão de suporte da sala da live é da LiveShop Turbo, da indústria ou de cada live? | No original o número está escrito no código, sem dizer de quem é (linha 7.8 do inventário) | Onde o número é cadastrado. Dono: Tech Lead | E1-03 |
| P20 | A indústria marca o andamento de cada pedido, como em negociação, convertido ou cancelado? | O original tem esses estados no banco, e nenhuma tela os muda (linhas 8.3 e 8.4 do inventário) | O ciclo de vida do pedido. Dono: Tech Lead | E1-03 |

### 2.2 Perguntas técnicas

| # | Pergunta | O que a documentação já diz | O que depende da resposta | Resolve em |
| --- | --- | --- | --- | --- |
| P12 | A entrada do Admin e da indústria é por e-mail e senha, com o token de sessão emitido pela API própria, ou por um provedor externo, como o Google ou o Amazon Cognito? | `docs/notes.md` cita OAuth 2.0 e JWT (o token assinado que identifica a sessão) | A autenticação | E1-04 |
| P13 | O e-mail sai pelo Resend ou pelo Amazon SES? | O original usa Resend para e-mail. O WhatsApp continua pela Unnichat, resposta de 26/11/2026 (`docs/inventario-do-sistema-original.md`, linha 9.3) | O envio de notificações | E1-04 |
| P14 | O servidor na AWS roda em EC2 ou em Fargate (o serviço que roda contêineres sem servidor próprio), descrito em Terraform como no `livequevende-ecommerce`? | `docs/notes.md` cita EC2, S3, RDS e Docker | O ambiente de homologação e o de produção | E1-04 |
| P15 | O Redis entra como serviço da AWS (ElastiCache)? | `docs/notes.md` cita "redis, localstorage ou outras tecnologias" para o histórico do carrinho | A fila de notificações, o carrinho salvo e o envio dos comentários em tempo real | E1-04 |

### 2.3 Ações que dependem de terceiros

| Ação | Quem faz | Quando |
| --- | --- | --- |
| Criar o repositório no GitHub e a proteção da `main` | Tech Lead | Na E1-06, antes do primeiro PR |
| Definir a pasta e as listas de sprint deste projeto no ClickUp | Tech Lead | Antes do planejamento da primeira sprint |
| Conseguir um token da API do ClickUp com permissão de criar tarefa na lista do projeto | Tech Lead | Antes da segunda leva de histórias |
| Abrir a conta de teste no Panda Video | Tech Lead | Antes do início da E1-05 |

### 2.4 Decisões em aberto

| Decisão | Situação |
| --- | --- |
| Nome da lista de defeitos e dívida técnica no ClickUp | A definir |
| Nome da branch principal: o repositório local foi iniciado na `master`, e as histórias E1-06 e E1-07 usam `main` | A definir na E1-06 |

---

## Parte 3 · Defeitos e dívida técnica

Lista separada das histórias. Cada linha diz o que acontece, o impacto e do que depende a correção. Item corrigido sai da lista no PR que o corrige.

| # | Item | Impacto | Dependência |
| --- | --- | --- | --- |
| | Nenhum item registrado | | |

---

## Parte 4 · Épicos

### É1 · Fundação do repositório e estruturação do projeto

**Objetivo:** deixar escritos e verificados o produto, a stack e o repositório, para que a primeira história de produto comece sem decisão em aberto que mude o banco, a API ou a entrada do varejista.

**F1.1 · Produto definido por escrito**
As regras do produto, as pessoas, o vocabulário e o modelo de dados estão escritos e confirmados pelo Tech Lead. As histórias são construídas na ordem E1-02 e E1-03, pois o modelo de dados usa os nomes do vocabulário do `CLAUDE.md` §4. Elas partem de `docs/inventario-do-sistema-original.md`, que diz o que entra do sistema original.

- **E1-02 · Objetivo, perfis, regras inegociáveis e vocabulário do produto**
  - **História:** Como equipe técnica, quero o objetivo, as pessoas, as regras que não podem falhar e o nome de cada conceito escritos, para que cada regra tenha um teste que a prove e cada conceito tenha um nome só.
  - **O que precisa ser feito:** Precisam ser preenchidos o `CLAUDE.md` §1 a §4 e a tabela de provas de `docs/diretrizes-de-desenvolvimento.md`, pois o original usa "intenção de compra", "pedido" e "carrinho" para conceitos que se sobrepõem, e um nome gravado no banco é caro de trocar.
  - **Critérios de aceite:**
    - [ ] O `CLAUDE.md` §1 tem o objetivo e as pessoas: Admin, Indústria, Varejista e Representante (sem acesso à plataforma, conforme a resposta da P4 de 26/11/2026).
    - [ ] O `CLAUDE.md` §3 lista as regras inegociáveis, numeradas, e cada uma tem uma linha na tabela de provas.
    - [ ] O `CLAUDE.md` §3 diz qual dado pessoal o produto grava (CNPJ, e-mail, telefone, comentário).
    - [ ] O `CLAUDE.md` §4 tem um nome por conceito, em documento e no código.

- **E1-03 · Modelo de domínio e ciclos de vida**
  - **História:** Como equipe técnica, quero as entidades, as relações e os estados escritos, para que o banco nasça com as restrições certas.
  - **O que precisa ser feito:** Precisa ser escrito `docs/modelo-de-dominio.md`, pois três mudanças das notas alteram o centro do modelo e são caras de reverter depois do primeiro dado gravado: o acesso por ID único com vários usuários no mesmo CNPJ, o carrinho salvo e editável e o comentário anônimo moderado.
  - **Critérios de aceite:**
    - [ ] Cada entidade tem o nome igual ao vocabulário do `CLAUDE.md` §4.
    - [ ] Cada relação diz quantos existem de cada lado, como empresa (CNPJ) → acessos → indústrias.
    - [ ] Cada estado de live, carrinho, pedido e comentário tem a transição, quem a faz e o que fica no histórico.
    - [ ] O carrinho abandonado tem definição verificável: o tempo e o evento que o marcam.
    - [ ] As perguntas P5 a P11 da Parte 2 têm resposta ou saem como decisão em aberto com dono.

**F1.2 · Stack decidida e contrato do player validado**
Cada camada da stack tem a escolha e a justificativa escritas, e o Panda Video foi testado antes de a sala da live ser escrita. A E1-05 pode ser feita junto com a E1-04, e o resultado dela entra no ADR-0001.

- **E1-04 · Requisitos que guiam a stack e escolha da stack registrada em ADR**
  - **História:** Como equipe técnica, quero a stack escolhida a partir de requisitos escritos, para que cada peça tenha uma justificativa que outra pessoa consiga conferir.
  - **O que precisa ser feito:** Precisam ser escritos `docs/stack.md` e o ADR-0001, pois a troca da base do original (Supabase com segurança no banco) por uma API própria muda onde mora toda regra de acesso, e trocar uma peça depois do primeiro código custa uma migração.
  - **Critérios de aceite:**
    - [ ] O `docs/stack.md` tem os requisitos com valor: lives simultâneas, espectadores por live e tempo de entrega do comentário.
    - [ ] O `docs/stack.md` tem a escolha de cada camada: web, API, banco, cache e fila, autenticação, arquivos, e-mail, WhatsApp e hospedagem.
    - [ ] O ADR-0001 registra onde mora a regra de acesso a dados: só na API, ou na API e no banco.
    - [ ] O ADR-0001 registra como o comentário e a vitrine chegam ao varejista em tempo real.
    - [ ] As perguntas P12 a P15 da Parte 2 têm resposta.

- **E1-05 · Teste da API do Panda Video com transmissões simultâneas**
  - **História:** Como equipe técnica, quero testar o Panda Video numa conta de teste antes de escrever a sala da live, para que a escolha do player se apoie em comportamento medido.
  - **O que precisa ser feito:** Precisa ser criada uma live de teste pela API do Panda Video e exibida numa página local, pois o player é a peça que o varejista mais usa e é a única integração nova sem uso anterior no time.
  - **Critérios de aceite:**
    - [ ] Uma live criada pela API aparece no player embutido numa página local.
    - [ ] Duas transmissões ao mesmo tempo são exibidas em duas páginas sem interferência.
    - [ ] O atraso entre a câmera e o player está medido e registrado.
    - [ ] O `docs/integracoes/panda-video.md` registra as rotas usadas, a autenticação, os eventos de estado da live e os limites do plano.

**F1.3 · Repositório e projeto verificados**
A `main` só recebe mudança por PR verificado, e o projeto roda na máquina de qualquer pessoa do time. As histórias são construídas na ordem E1-06, E1-07 e E1-08, pois a verificação da E1-07 só bloqueia o merge com a proteção da E1-06, e o Docker Compose da E1-08 sobe o projeto da E1-07.

- **E1-06 · Repositório no GitHub com a branch main protegida**
  - **História:** Como equipe técnica, quero que a `main` só receba mudança por PR verificado e revisado, para que nenhuma mudança fora das regras de `docs/fluxo-de-git.md` chegue ao histórico.
  - **O que precisa ser feito:** Precisam ser criados o repositório no GitHub e a proteção da `main`, pois a verificação automática só bloqueia o merge quando está marcada como obrigatória.
  - **Critérios de aceite:**
    - [ ] O repositório existe no GitHub, com a organização e o nome registrados no `README.md`.
    - [ ] A `main` recusa push direto.
    - [ ] O PR só é mesclado com a verificação aprovada e a aprovação de uma pessoa diferente do autor.
    - [ ] Só o merge por rebase está habilitado.
    - [ ] A branch é apagada depois do merge.

- **E1-07 · Monorepo com web e API, com lint, build e teste na verificação automática**
  - **História:** Como equipe técnica, quero o projeto criado na stack do ADR-0001 com lint, build e teste em todo PR, para que o primeiro código de produto já entre verificado.
  - **O que precisa ser feito:** Precisa ser criada a estrutura `apps/web` (Next.js) e `apps/api` (FastAPI), cada uma com a sua verificação, pois a regra que não tem mecanismo desde o início vira exceção no código que vem depois.
  - **Critérios de aceite:**
    - [ ] As versões de Node e de Python estão em um arquivo só cada, e a verificação automática as lê de lá.
    - [ ] As dependências estão em versão exata, e a verificação instala o arquivo de trava de versões congelado.
    - [ ] A rota `/health` da API responde e tem teste.
    - [ ] O lint, a checagem de tipos, o teste e o build da web e da API rodam em todo PR.
    - [ ] Os comandos estão no `README.md`.

- **E1-08 · Ambiente local completo com Docker Compose**
  - **História:** Como equipe técnica, quero subir web, API e banco com um comando, para que qualquer pessoa do time rode e teste o projeto do mesmo jeito na máquina dela.
  - **O que precisa ser feito:** Precisa ser criado o `compose.yaml` com os serviços do ADR-0001, pois os testes da API precisam do PostgreSQL real e o original dependia do Supabase local para isso.
  - **Critérios de aceite:**
    - [ ] `docker compose up` sobe web, API e PostgreSQL, e o Redis se o ADR-0001 o escolher.
    - [ ] As migrations do banco rodam na subida.
    - [ ] Um teste da API roda contra o PostgreSQL do compose, na máquina e na verificação automática.
    - [ ] O `.env.example` lista toda variável, sem valor secreto.

**F1.4 · Caminho validado com o time**
O time confirmou ou corrigiu as decisões do épico antes de os épicos de produto serem abertos. A E1-09 é a última do épico, pois revisa o que as outras decidiram.

- **E1-09 · Validação do caminho com o time de desenvolvimento**
  - **História:** Como equipe técnica, quero revisar com o time as decisões da sprint antes de abrir os épicos de produto, para corrigir o rumo enquanto a mudança ainda é só documento.
  - **O que precisa ser feito:** Precisa ser feita uma reunião com o Tech Lead e o time, com a pauta tirada da Parte 2 do backlog e dos ADRs, pois as próximas sprints constroem em cima do modelo e da stack decididos aqui.
  - **Critérios de aceite:**
    - [ ] Cada decisão do épico foi confirmada ou alterada, e a alteração está escrita no documento correspondente.
    - [ ] Cada pergunta que restou na Parte 2 tem dono e data de resposta.
    - [ ] Os épicos seguintes têm título e objetivo de uma frase na Parte 4.
