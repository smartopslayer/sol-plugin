# Status do projeto

O campo `status` de `sol:list_projects` é o último estado do projeto no ciclo do Terraform (plan, apply, destroy). Os nomes abaixo são os mesmos da tela do SOL. Use a coluna do idioma da pessoa.

| `status` | pt-BR | en-US |
|---|---|---|
| `CREATED` | **Novo**: projeto ainda sem plan. | **New**: the project has no plan yet. |
| `PLAN_STARTED` | **Planejando...**: o terraform plan está rodando. | **Planning...**: the terraform plan is running. |
| `PLANNED_WITH_CHANGES` | **Planejado**: o plan tem mudanças pendentes, esperando aplicar ou descartar na tela do SOL. | **Planned**: the plan has pending changes, waiting to be applied or discarded in SOL. |
| `PLANNED_NO_CHANGES` | **Sem alterações**: o plan não encontrou mudanças; nada pendente. | **No changes**: the plan found no changes; nothing pending. |
| `APPLY_STARTED` | **Aplicando...**: o terraform apply está rodando. | **Applying...**: the terraform apply is running. |
| `APPLIED` | **Aplicado**: o último apply terminou com sucesso. | **Applied**: the last apply finished successfully. |
| `PLAN_ERROR` | **Erro no plan**: o último plan falhou; o erro está no Histórico do projeto. | **Plan error**: the last plan failed; the error is in the project's History. |
| `APPLY_ERROR` | **Erro no apply**: o último apply falhou; o erro está no Histórico do projeto. | **Apply error**: the last apply failed; the error is in the project's History. |
| `DESTROY_STARTED` | **Destruindo...**: o terraform destroy está rodando. | **Destroying...**: the terraform destroy is running. |
| `DESTROY_PLANNED_NO_CHANGES` | **Destroy planejado, sem recursos**: o plan de destroy não encontrou recursos para remover. | **Destroy planned, no resources**: the destroy plan found no resources to remove. |
| `DESTROY_PLANNED_WITH_CHANGES` | **Destroy planejado**: há recursos a remover, esperando confirmar ou descartar na tela do SOL. | **Destroy planned**: there are resources to remove, waiting to be confirmed or discarded in SOL. |
| `DESTROY_PLAN_ERROR` | **Erro no destroy plan**: o plan de destroy falhou; o erro está no Histórico do projeto. | **Destroy plan error**: the destroy plan failed; the error is in the project's History. |
| `DESTROY_ERROR` | **Erro no destroy**: o último destroy falhou; o erro está no Histórico do projeto. | **Destroy error**: the last destroy failed; the error is in the project's History. |
| `DISCARDED` | **Descartado**: as mudanças foram descartadas; nada foi aplicado. | **Discarded**: the changes were discarded; nothing was applied. |
| vazio ou outro valor | **Status não informado**. | **Status not reported**. |

Regras:
- `*_STARTED` quer dizer que algo está rodando agora. Diga que ainda não terminou e mande o link para acompanhar.
- Em status de erro, não tente adivinhar a causa: o conector não traz o log. Mande o link do projeto, onde fica o Histórico.
- `PLANNED_WITH_CHANGES` e `DESTROY_PLANNED_WITH_CHANGES` esperam uma decisão de uma pessoa na tela do SOL. Não diga que vai aplicar, confirmar ou descartar.
