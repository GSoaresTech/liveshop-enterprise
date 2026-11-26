# Registro de decisões

> ADR, do inglês *Architecture Decision Record*, é o registro de uma decisão: o que se decidiu, em que contexto e o que muda por causa dela. Cada decisão fica em um arquivo.

## Quando uma decisão vira ADR

Vira ADR a decisão de arquitetura ou de contrato que atende a pelo menos uma destas condições:

- troca uma escolha de `docs/stack.md` ou uma regra do `CLAUDE.md` ou de `docs/diretrizes-de-desenvolvimento.md`;
- escolhe entre alternativas com custo alto de reversão: o modelo de dados central, o protocolo com um terceiro ou um serviço de infraestrutura;
- muda um contrato público: rota, formato de webhook ou evento.

Não vira ADR:

- mudança de número, limite ou configuração;
- decisão de tela;
- correção de defeito;
- escolha que o código explica sozinho.

A escolha da stack deste projeto é feita entre alternativas com custo alto de reversão, porque troca a base do LiveShop Enterprise original (Supabase, com a segurança no banco) por uma API própria. Por isso ela é escrita em `docs/stack.md` e registrada no ADR-0001, na E1-04 (`docs/backlog.md`).

Os ADRs do LiveShop Enterprise original valem só como contexto. Eles não valem neste repositório até uma decisão daqui os adotar.

## Como se escreve

- Um arquivo por decisão, chamado `NNNN-titulo-curto.md`: quatro dígitos, o número seguinte ao maior que existe na `main`, e o título em minúsculas, sem acento, com hífen entre as palavras.
- O título diz a decisão, de forma literal (`docs/backlog.md` §1.3).
- O ADR não é reescrito depois de mesclado. A decisão que troca outra nasce em ADR novo, e o antigo só muda o status para "Substituído pelo ADR-NNNN".
- O ADR entra no mesmo PR que aplica a decisão, e ganha a linha dele na tabela abaixo.
- Não se escreve nome de pessoa. Quando o papel importa, escreve-se Tech Lead.

## Formato

```markdown
# ADR-NNNN · Título que diz a decisão

- **Status:** Vigente
- **Data:** DD/MM/AAAA

## Contexto

O que obrigava a decidir.

## Decisão

O que vale, em frases que alguém consegue cumprir.

## Consequências

O que muda por causa da decisão, incluindo o custo aceito.

## Onde a regra está escrita

Os documentos e arquivos que aplicam a decisão.
```

## Decisões

| ADR | Decisão | Data | Status |
| --- | --- | --- | --- |
| | Nenhum ADR registrado | | |
