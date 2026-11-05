# Erros do conector SOL

Diga a causa em uma frase e o próximo passo. Não repita a chamada que falhou em sequência. Nunca peça token ou senha para "resolver" um erro.

## Erros de `sol:list_projects`, `sol:get_project` e `sol:get_project_files`

| O que aparece | Causa | O que dizer (pt-BR) | What to say (en-US) |
|---|---|---|---|
| O app pede login de novo, a tool some ou a chamada volta com HTTP 401 | A conexão venceu, foi revogada, ou a organização deixou de estar liberada para o MCP | "Sua conexão com o SOL expirou. Reconecte o SOL no app (veja como abaixo) e faça o login de novo." Siga [conexao.md](conexao.md). | "Your SOL connection expired. Reconnect SOL in the app and sign in again." |
| "Conexão sem identidade. Reconecte o SmartOpsLayer." | A conexão ficou sem os dados de login | "A conexão com o SOL precisa ser refeita: reconecte o SOL no app." | "The SOL connection needs to be set up again: reconnect SOL in the app." |
| "Você não é mais membro desta organização. Reconecte o SmartOpsLayer." | A pessoa saiu (ou foi removida) da organização escolhida no login | "Você não faz mais parte dessa organização no SOL. Reconecte o SOL escolhendo outra organização; se deveria ter acesso, fale com um ADMIN da organização." | "You're no longer a member of that organization in SOL. Reconnect SOL and pick another organization; if you should have access, ask an organization ADMIN." |
| "O SmartOpsLayer recusou o acesso aos projetos desta organização." | A conta não tem acesso aos projetos dessa organização (papel ou situação da organização no SOL) | "O SOL recusou o acesso aos projetos dessa organização. Peça a um ADMIN da organização para conferir o seu acesso no SOL." | "SOL refused access to this organization's projects. Ask an organization ADMIN to check your access in SOL." |
| "A lista de projetos está indisponível agora. Tente de novo." ou HTTP 503 | Falha temporária do SOL | "O SOL não respondeu agora. Vou tentar de novo em alguns segundos." Tente uma vez só; se falhar de novo, peça para a pessoa tentar mais tarde. | "SOL didn't respond right now. I'll try again in a few seconds." |
| "Projeto não encontrado nesta organização. Use list_projects para ver os projetos." | O `project_id` não é de um projeto desta organização (ou o projeto foi excluído) | Chame `sol:list_projects` e confirme o projeto com a pessoa. Se ela espera ver o projeto, ele pode ser de outra organização: reconecte escolhendo a outra. | "That project isn't in this organization. Let me list your projects to find it." |
| "Arquivo não encontrado no código atual do projeto. Use get_project para ver os arquivos." | O `path` não está na lista `files` do projeto (ou é um arquivo que não sai pelo conector, como `tfstate`, `tfvars` ou log) | Chame `sol:get_project`, use um caminho de `files` ou leia sem `path`. | "That file isn't in the project's current code. Let me check the file list." |
| "Os arquivos do projeto estão indisponíveis agora. Tente de novo." | Falha temporária do SOL ao ler os arquivos | "O SOL não conseguiu ler os arquivos agora. Vou tentar de novo em alguns segundos." Tente uma vez só. | "SOL couldn't read the files right now. I'll try again in a few seconds." |
| HTTP 429 ou mensagem de limite de uso | Muitas chamadas em pouco tempo | Diga quando tentar de novo, se a resposta disser; senão, peça para tentar em alguns minutos. Não repita a chamada em seguida. | Say when to try again if the response says so; otherwise, in a few minutes. |
| Erro de validação do argumento | `limit` fora de 1 a 100, `query` com mais de 200 caracteres, `project_id` que não veio de `sol:list_projects`, ou `offset` negativo | Corrija o argumento e chame de novo, uma vez. | Fix the argument and call again, once. |

## Erros de `sol:ask_ai_builder` e `sol:get_turn`

| O que aparece | Causa | O que dizer (pt-BR) | What to say (en-US) |
|---|---|---|---|
| "Esta conexão não tem permissão de conversar com o AI Builder…" | No login, a permissão "Conversar com o AI Builder" não foi marcada | "A conexão com o SOL é só de leitura. Para conversar com o AI Builder, reconecte o SOL e marque essa permissão no login." | "This SOL connection is read-only. To talk to the AI Builder, reconnect SOL and allow it at sign-in." |
| "Seu papel nesta organização só permite leitura pelo MCP…" | A pessoa é GUEST na organização | "Seu papel nessa organização só permite consultar. Para pedir mudanças ao AI Builder, peça a um ADMIN da organização um papel TECH ou ADMIN." | "Your role in that organization is read-only. Ask an organization ADMIN for the TECH or ADMIN role." |
| "A organização está sem pagamento ativo…" | A organização está sem pagamento ativo no SOL | "O AI Builder está bloqueado porque a organização está sem pagamento ativo. Um ADMIN regulariza em Configurações → Billing." | "The AI Builder is blocked because the organization has no active payment. An ADMIN can fix it in Settings → Billing." |
| "Limite de 20 turnos por hora…" ou "Limite de 100 turnos por dia…" | A cota de conversa com o AI Builder acabou | Diga o horário que vem na mensagem e não tente antes. | Tell the person the time in the message and don't retry before it. |
| "Já há um turno do AI Builder rodando neste projeto…" ou "…já tem 3 turnos…rodando" | Outro pedido (pela tela ou por outra conexão) ainda está rodando | "O AI Builder ainda está trabalhando num pedido deste projeto. Espere terminar e tente de novo." Se o pedido for desta conversa, chame `sol:get_turn` com o `turn_id`. | "The AI Builder is still working on a request for this project. Wait for it to finish and try again." |
| "Aprovar deploy ou destroy não existe por esta conexão…" | A mensagem tentou aprovar um deploy | "Deploy só é aprovado por uma pessoa, na tela do projeto no SOL: <url>." | "Deploys are approved by a person on the project's page in SOL: <url>." |
| "Turno não encontrado nesta conexão…" | O `turn_id` não é de um pedido desta conexão | Use o `turn_id` que `sol:ask_ai_builder` devolveu nesta conversa. | Use the `turn_id` returned by `sol:ask_ai_builder` in this conversation. |
| "O AI Builder está indisponível agora. Tente de novo." | Falha temporária do SOL | Tente uma vez só; se falhar de novo, peça para a pessoa tentar mais tarde. | "SOL didn't respond right now. I'll try once more." |
| `status` = `interrupted` | O SOL reiniciou no meio do pedido | "O pedido foi interrompido. O que já foi gravado continua no projeto; quer que eu peça de novo?" | "The request was interrupted. What was saved stays in the project; want me to ask again?" |

## Erros de `sol:create_project` e `sol:run_validation`

As recusas de permissão, de pagamento e de projeto são as mesmas de `sol:ask_ai_builder` (tabela acima).

| O que aparece | Causa | O que dizer (pt-BR) | What to say (en-US) |
|---|---|---|---|
| "Escolha a conta cloud do projeto. Contas cloud desta organização: …" | A organização tem mais de uma conta cloud | Mostre as contas (nome) e pergunte em qual criar; chame de novo com o `cloud_account_id` escolhido. | "Which cloud account should the project use?" and list the accounts. |
| "Conta cloud não encontrada nesta organização…" | O `cloud_account_id` não é de uma conta desta organização | Use uma das contas listadas na própria mensagem. Se a pessoa espera outra conta, ela pode ser de outra organização: reconecte escolhendo a outra. | "That cloud account isn't in this organization. These are the available ones: …" |
| "…ainda não tem conta cloud…" | A organização não conectou nenhuma conta AWS | "Conecte uma conta AWS no SOL (Contas cloud) e depois eu crio o projeto." | "Connect an AWS account in SOL (Cloud accounts) first, then I'll create the project." |
| "O SmartOpsLayer recusou criar projeto nesta organização com a sua conta…" | A conta da pessoa não pode criar projeto nessa organização | "O SOL não deixou a sua conta criar projeto nessa organização. Peça a um ADMIN da organização." | "SOL didn't let your account create projects in this organization. Ask an organization ADMIN." |
| "O SmartOpsLayer recusou os dados do projeto…" | Nome, conta ou região inválidos | Confira com a pessoa e chame de novo, uma vez. | Check the details with the person and try once more. |
| "Limite de 10 projetos criados por hora…" ou "Limite de 20 validações por hora…" | A cota por hora acabou | Diga o horário que vem na mensagem e não tente antes. | Tell the person the time in the message and don't retry before it. |
| `status` = `not_verified` | A validação não terminou a tempo | "A validação não terminou a tempo; tento de novo em alguns minutos." Não invente resultado. | "The validation didn't finish in time; I'll try again in a few minutes." |
| "A validação está indisponível agora." ou "O SmartOpsLayer está indisponível agora." | Falha temporária do SOL | Tente uma vez só; se falhar de novo, peça para a pessoa tentar mais tarde. | "SOL didn't respond right now. I'll try once more." |

## Mensagens da página de login do SOL

A pessoa vê estas mensagens no navegador, durante o login, e pode perguntar o que significam:

| A página diz que... | O que fazer |
|---|---|
| o MCP está desligado na organização dela | Um ADMIN da organização liga no SOL, em **Configurações → Integrações → Conexões MCP**; depois, conecte de novo. |
| nenhuma das organizações dela pode receber conexões MCP | O MCP está desligado em todas as organizações dela: um ADMIN liga no SOL, em **Configurações → Integrações → Conexões MCP**; depois, conecte de novo. |
| a organização exige verificação em duas etapas | Ativar a verificação em duas etapas no SOL (Perfil, Segurança) e conectar de novo. |
| e-mail ou senha incorretos, ou código inválido | Conferir o login na própria página do SOL. Não digite a senha no chat. |
| muitas tentativas, ou o pedido de conexão venceu | Começar a conexão de novo pelo app (desconectar e conectar). |
| o serviço não respondeu | Falha temporária: tentar de novo em alguns minutos. |

## Erros de `sol:plan` e `sol:get_deploy_status`

| O que aparece | Causa | O que dizer (pt-BR) | What to say (en-US) |
|---|---|---|---|
| O app pede um novo login ao chamar `sol:plan` | A conexão ainda não tem a permissão de planejar | "Para rodar o plan, faça o login no SOL de novo e marque "Planejar o deploy"." | "To run the plan, sign in to SOL again and allow "Plan the deploy"." |
| "Esta conexão não tem permissão de planejar…" | No login, a permissão "Planejar o deploy" não foi marcada | "Para rodar o plan, reconecte o SOL e marque "Planejar o deploy" no login." | "To run the plan, reconnect SOL and allow "Plan the deploy" at sign-in." |
| "Seu papel nesta organização só permite leitura pelo MCP. Planejar…" | A pessoa é GUEST na organização | "Seu papel nessa organização só permite consultar. Para rodar o plan, peça a um ADMIN da organização um papel TECH ou ADMIN." | "Your role in that organization is read-only. Ask an organization ADMIN for the TECH or ADMIN role." |
| "Este projeto não tem conta AWS ligada…" ou "A conta AWS ligada a este projeto…" | O projeto não tem conta AWS válida desta organização | Diga a mensagem e mande o link do projeto: a conta é ligada na tela do SOL. | Relay the message with the project link: the AWS account is linked on SOL's screen. |
| "Limite de 10 plans por hora…" | A cota de plans acabou | Diga o horário que vem na mensagem e não tente antes. | Tell the person the time in the message and don't retry before it. |
| "Já há um turno do AI Builder rodando neste projeto…" | O AI Builder está mudando o código deste projeto | "O AI Builder ainda está mudando o código deste projeto. Espere terminar e rode o plan de novo." | "The AI Builder is still changing this project's code. Wait for it to finish and run the plan again." |
| "Plan não encontrado neste projeto…" | O `plan_id` não é de um plan deste projeto | Use o `plan_id` que `sol:plan` devolveu para este projeto. | Use the `plan_id` returned by `sol:plan` for this project. |

## Erros de `sol:request_deploy`, `sol:request_destroy` e do pedido

| O que aparece | Causa | O que dizer (pt-BR) | What to say (en-US) |
|---|---|---|---|
| O app pede um novo login ao chamar `sol:request_deploy` ou `sol:request_destroy` | A conexão ainda não tem a permissão de pedir o deploy | "Para pedir o deploy, faça o login no SOL de novo e marque "Pedir deploy e destroy"." | "To request the deploy, sign in to SOL again and allow "Request deploy and destroy"." |
| "Esta conexão não tem permissão de pedir o deploy…" | No login, a permissão não foi marcada | "Reconecte o SOL e marque "Pedir deploy e destroy" no login." | "Reconnect SOL and allow "Request deploy and destroy" at sign-in." |
| "Seu papel nesta organização só permite leitura pelo MCP. Pedir deploy…" | A pessoa é GUEST na organização | "Seu papel nessa organização só permite consultar. Peça a um ADMIN da organização um papel TECH ou ADMIN." | "Your role in that organization is read-only. Ask an organization ADMIN for the TECH or ADMIN role." |
| "Este plan não pode ser aprovado…" ou o plan ainda roda, falhou ou não tem mudanças | O `plan_id` não serve para deploy | Rode `sol:plan` de novo e peça com o `plan_id` novo. | Run `sol:plan` again and request with the new `plan_id`. |
| "Limite de 10 pedidos de deploy por hora…" | A cota de pedidos acabou | Diga o horário que vem na mensagem e não tente antes. | Tell the person the time in the message and don't retry before it. |
| `approval.status` = `expired` | Ninguém aprovou em 15 minutos | "O pedido venceu sem aprovação; nada foi aplicado. Posso pedir de novo." | "The request expired without approval; nothing was applied. I can request it again." |
| `approval.status` = `rejected` | A pessoa recusou na página | "Você recusou o pedido no SOL; nada foi aplicado." | "You rejected the request in SOL; nothing was applied." |
| `approval.status` = `failed` | O plan mudou, a conta mudou ou a execução falhou | "Não foi concluído; o motivo está no Histórico do projeto. Rode o plan de novo antes de pedir." | "It didn't complete; the reason is in the project's History. Run the plan again before requesting." |
| "Pedido não encontrado neste projeto…" | O `approval_id` não é de um pedido deste projeto | Use o `approval_id` que o pedido devolveu para este projeto. | Use the `approval_id` returned for this project. |
