# Anotações para o B2B

## Objetivo do projeto
O objetivo da plataforma é facilitar e estruturar a implementação do serviço de LiveShop na nova frente de atuação da LiveShop Turbo, voltada ao mercado B2B (Business to Business). 
Trata-se de uma solução SaaS de live commerce que conecta indústrias e varejistas por meio de transmissões ao vivo, permitindo a apresentação de produtos em formato de combos, com foco em geração de demanda, engajamento comercial e apoio à operação de vendas entre empresas.

## Documentação a ser consultada
- Enterprise LiveShop Turbo - Documentação Técnica: /Documentos/b2b-liveshop/docs/Enterprise B2B-.pdf
- Projeto original do LiveShop enterprise: /Documentos/liveshop-enterprise, [GitHub Repo](https://github.com/GSoaresTech/liveshop-enterprise-v1)
- Documentação do Panda Video: [Panda Video](https://docs.pandavideo.com/)
- Documentação do Unnichat: (questionar a equipe de automação sobre a documentação e conhecimento, ou com os desenvolvedores da ferramenta)


## Stack de tecnologias
- **Frontend:** React, Next.js, TypeScript, Tailwind CSS
- **Backend:** FastAPI, Python, PostgreSQL
- **Infraestrutura:** AWS (EC2, S3, RDS), Docker
- **Autenticação e Autorização:** OAuth 2.0, JWT

## Mudanças em relação á versão presente no PDF
- Presença de uma API e banco de dados proprios, sem uso do supabase como no projeto original.
- Possibilidade de logout do usuário, com redirecionamento para a página de login.
- Player de lives ser o Panda video [Panda Video](https://docs.pandavideo.com/), com suporte a múltiplas transmissões ao vivo simultâneas.
- Melhoria e refatoração do código, com foco em performance e escalabilidade.
- Ajuste no carrinho de compras, permitindo a adição de múltiplos produtos e combos, com cálculo automático do valor total, além de historico salvo do mesmo (podendo ser editado, usando redis, localstorage ou outras tecnologias).
- Integração para envio de notificações via e-mail além do whatsapp.
- Identificação de acessos dos varejistas, por ID unico de acesso, permitindo varios acessos com o mesmo CNPJ, mas com ID unico de acesso para cada usuário, permitindo rastreabilidade e controle de acessos.
- Comentários no momento da live, e possibilidade de comentários anônimos, com moderação e filtro de palavras.
- Rastreabilidade de carrinhos abandonados, com envio de notificações para os varejistas, incentivando a finalização da compra.