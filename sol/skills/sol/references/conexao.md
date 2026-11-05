# Como conectar o SOL

O endereço do conector é `https://mcp.smartopslayer.com/mcp`. O login é sempre na página do SOL, uma vez por conexão: a pessoa entra com o e-mail e a senha do SOL (e o código de 2FA, se tiver) e escolhe a organização. Nunca peça nada disso no chat.

Explique só os passos do app que a pessoa está usando:

| App | Passos |
|---|---|
| claude.ai ou app desktop, com o plugin | **Customize > Plugins**, abra o plugin **SmartOpsLayer (SOL)**, aba **Connectors**, e clique em **Connect** no conector `sol`. Em Team e Enterprise, se o conector aparecer como não adicionado, um Owner adiciona em **Organization settings > Connectors** e cada pessoa conecta com a própria conta. |
| claude.ai sem o plugin | **Customize > Connectors > Add custom connector**, com a URL `https://mcp.smartopslayer.com/mcp`, e depois **Connect**. Em Team e Enterprise, um Owner adiciona em **Organization settings > Connectors**. |
| Claude Code | Digite `/mcp`, escolha o servidor `sol` (com o plugin aparece como `plugin:sol:sol`) e selecione **Authenticate**. Se a conexão venceu, **Re-authenticate**. |
| Cursor | **Settings > MCP**: o servidor `sol` precisa estar no `mcp.json` com a URL acima; o Cursor abre o login do SOL quando conecta. |

Para trocar de organização: desconecte (claude.ai: **Disconnect** no conector; Claude Code: `/mcp` > **Clear authentication**) e conecte de novo, escolhendo a outra organização na página do SOL.
