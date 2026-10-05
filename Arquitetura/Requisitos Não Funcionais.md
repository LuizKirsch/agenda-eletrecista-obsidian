---
tags: [requisito, rnf]
---
# Requisitos Não Funcionais

- **RNF-1** o sistema deve ser uma aplicação web responsiva, acessível via navegador em dispositivo móvel (celular), já que o uso ocorre predominantemente em campo;
- **RNF-2** o sistema deve funcionar com conexão de internet disponível;
- **RNF-3** a interface deve ser extremamente simples e intuitiva, com curva de aprendizado baixa;
- **RNF-4** o sistema deve responder rapidamente mesmo em conexões móveis instáveis (3G/4G), evitando travamentos durante o atendimento;
- **RNF-5** os dados de clientes, endereços e ordens de serviço devem ser armazenados de forma persistente e com backup, evitando perda do histórico acumulado ao longo do tempo;
- **RNF-6** o sistema deve proteger os dados pessoais de clientes e usuários em conformidade com a LGPD: senhas armazenadas somente com hash bcrypt e nunca retornadas pela API; sessão por JWT assinado em cookie httpOnly, sameSite=lax e secure em produção; todas as rotas da API, exceto o login, exigem sessão válida;
- **RNF-7** a interface deve ser operável com toques grandes e poucos cliques, considerando o uso em campo (mãos sujas, luvas, pressa);
- **RNF-8** o sistema (web) deve ser compatível com os principais navegadores mobile (Chrome, Safari) e ter layout responsivo para diferentes tamanhos de tela, dispensando instalação de aplicativo nativo.

> Fonte: Documentação Técnica V6, seção 5.
