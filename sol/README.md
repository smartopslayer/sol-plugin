# SmartOpsLayer (SOL)

Converse com o SmartOpsLayer pelo Claude, sem precisar entender MCP. O plugin junta o conector do SOL (`https://mcp.smartopslayer.com/mcp`) e o skill `sol`, que ensina o Claude a usar o SOL: o que pedir, em que ordem e o que nunca prometer.

## Uso

Instale o plugin, conecte o conector `sol` e faça o login na página do SOL, uma vez. Depois peça, por exemplo:

- "liste meus projetos no SOL";
- "qual a situação do projeto X?";
- "o deploy do projeto Y falhou?";
- "me mostre o main.tf do projeto Z".

Nesta versão o conector lista os projetos da organização escolhida no login, mostra o status e os últimos estados de cada um e lê o código Terraform (sem o estado do Terraform, as variáveis `tfvars` e os logs), com o link para a tela do projeto. Quem é ADMIN ou TECH e marca "Conversar com o AI Builder" no login também cria projeto, pede mudanças de código ao AI Builder do projeto, grava um arquivo `.tf` direto, envia e traz código do repositório do GitHub ligado ao projeto, valida o código (terraform validate e checkov, sem tocar na conta AWS) e estima o custo mensal, com boas práticas e segurança, como o painel de Inteligência da tela. Com a permissão "Planejar o deploy" (pedida num novo login na primeira vez), roda o terraform plan na conta AWS do projeto (só leitura), diz que aprovação o deploy vai exigir e explica o plan com a IA (resumo, riscos e recomendação, a mesma análise da tela). Com a permissão "Pedir deploy e destroy" (outro novo login), pede o deploy de um plan ou o destroy do projeto: a própria pessoa aprova na página do SOL, pelo link que a resposta traz. Também mostra o diagrama do código (grafo de dependências em Mermaid, com o que um plan muda). O desenho por camadas e a aprovação continuam na tela do SOL. O passo a passo de cada app (Claude, Claude Code e Cursor), as permissões, a aprovação e os custos estão no guia: https://app.smartopslayer.com/guides/mcp.

## Dados

O login é feito na página do SOL; o Claude recebe um token de acesso do SOL, preso à organização escolhida, e nunca a sua senha. As chamadas mandam ao SOL só o que você pede (parte do nome do projeto, o limite da lista, o projeto e o arquivo a ler). O plugin não guarda nada.

---

Connect Claude to SmartOpsLayer (SOL) without learning MCP: the plugin bundles the SOL connector and the `sol` skill. Sign in once on the SOL page, then ask "list my SOL projects". It lists projects, shows their status and diagram, reads and writes Terraform code, talks to the project's AI Builder, syncs with GitHub, validates, estimates cost and runs the plan. It can request a deploy or a destroy, but nothing changes in AWS until you approve it on the SOL page. Guide: https://app.smartopslayer.com/guides/mcp.
