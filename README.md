# LiveShop B2B

Plataforma de live commerce da LiveShop Turbo para o mercado B2B. A indústria apresenta os produtos em combos numa transmissão ao vivo, e o varejista assiste, monta o carrinho e registra o interesse de compra, que o representante da indústria leva adiante.

O projeto reescreve o LiveShop Enterprise original ([`GSoaresTech/liveshop-enterprise-v1`](https://github.com/GSoaresTech/liveshop-enterprise-v1)) com API e banco próprios, sem o Supabase. As mudanças em relação ao original estão em [`docs/notes.md`](docs/notes.md).

**Estado atual:** fase de planejamento. O repositório contém o documento de regras recebido, as anotações das mudanças e o backlog do primeiro épico. Ainda não há código de produto. As histórias abertas estão em [`docs/backlog.md`](docs/backlog.md).

## Documentos

Todo documento do repositório está nesta lista. Quem cria um documento acrescenta a linha aqui.

| Documento | Para que serve |
| --- | --- |
| [`docs/backlog.md`](docs/backlog.md) | As regras de escrita de história e de ClickUp, as pendências com terceiros, as decisões em aberto, os defeitos e os épicos |
| [`docs/registro-de-codigos-de-historia.md`](docs/registro-de-codigos-de-historia.md) | Todo código de história já usado, com o estado de cada um, para nenhum código ser reaproveitado |
| [`docs/adr/README.md`](docs/adr/README.md) | Quando uma decisão vira registro de decisão (ADR) e em que formato |
| [`docs/inventario-do-sistema-original.md`](docs/inventario-do-sistema-original.md) | As funções do LiveShop Enterprise original, cada uma com a decisão de manter, mudar ou retirar aprovada pelo Tech Lead em 27/11/2026, as respostas de P1 a P4 (26/11/2026) e o que foi feito só para a campanha Appel Home |
| [`docs/notes.md`](docs/notes.md) | O objetivo do projeto, a stack pedida e as mudanças em relação ao LiveShop Enterprise original |
| [`docs/Enterprise B2B-.pdf`](docs/Enterprise%20B2B-.pdf) | O documento de regras de negócio recebido. Só as seções 1 a 3 têm conteúdo |

Os documentos seguintes são criados pelas histórias do É1: `CLAUDE.md` e `docs/diretrizes-de-desenvolvimento.md` (E1-02), `docs/modelo-de-dominio.md` (E1-03), `docs/stack.md` e o ADR-0001 (E1-04), `docs/integracoes/panda-video.md` (E1-05) e `docs/fluxo-de-git.md` (E1-06).

## API (`apps/api`)

Requer o [`uv`](https://docs.astral.sh/uv/). O `uv` lê o Python 3.13 de `apps/api/.python-version` e baixa essa versão se ela não estiver instalada. Todos os comandos rodam de dentro de `apps/api`.

```bash
cd apps/api
cp .env.example .env   # ajuste DATABASE_URL, no formato postgresql+asyncpg://...
```

| Para quê | Comando |
| --- | --- |
| Instalar as dependências do `uv.lock` | `uv sync --frozen` |
| Rodar a API | `uv run fastapi dev main.py` |
| Testar | `uv run pytest` |
| Lint | `uv run ruff check .` |
| Formatação | `uv run ruff format --check .` |
| Tipos | `uv run mypy .` |
| Aplicar as migrations | `uv run alembic upgrade head` |

O `.env` não é versionado. O `alembic.ini` não tem URL: o Alembic e a API leem `DATABASE_URL` pelo mesmo `core/settings.py`.

## Pastas que não são versionadas

| Pasta | Para que serve |
| --- | --- |
| `local/` | Rascunhos e propostas de trabalho de cada pessoa |
| `reports/` | Arquivos gerados para uso único, como o CSV de importação do ClickUp, apagados depois do uso |
