# CONTEXTO ATUAL — GameHub

Atualizado: 10/10/2026. Fonte de verdade: GitHub + Cloudflare.

## Situação em produção — validada
- URL: https://jogos.siliciobrasil.com.br/
- Repositório: fbmmartins/gamehub, branch main.
- PR #1 (merge commit 9a0de0ec3dda86f4aeb20611adfcf622416a9dcf) adicionou Pipo ao catálogo; cinco jogos existentes em games/.
- Cloudflare conta af9a78b44e0f9137a58668f70771cc0b, zona siliciobrasil.com.br ID b0fab6806bde7eab3f81e3586862747c.
- Worker produção: gamehub-prod-20261010.
- Worker homologação: gamehub-hml-20261010 (workers.dev habilitado).
- Domínio customizado do Worker: ID 24c5a3562397060929e8bffae5ae94976c0f59ee; serviço gamehub-prod-20261010, enabled=true.
- DNS criado pela Cloudflare: jogos.siliciobrasil.com.br AAAA 100::, proxy ativo. **Não remover 100::**, é registro gerenciado da custom domain do Worker.
- Os Workers de HML e produção usam o mesmo artefato **Pipo v2** (etag `ebdcb5e0a57d3cc0dea91804bf3af5378c795e9895d43adcdc61eec65603c9ea`).
- Homologação e produção: homepage + cinco rotas verificadas em navegador remoto Cloudflare, HTTP 200. Sintaxe JavaScript do Pipo aprovada em Node 22. Validação da v2: Playwright local em 360×740, 390×844, 768×1024, 1366×768 e 1440×900; sem erros JavaScript e sem scroll horizontal. Inspeção visual local em mobile e desktop. Cloudflare Browser Rendering HML e PROD confirmou canvas vertical 480×810 no viewport 390×844 e horizontal 1080×690 no viewport 1366×768, ambos HTTP 200. Jogabilidade completa por usuário ainda pendente.
- Cloudflare Pages: tentativa de integração GitHub falhou com erro Cloudflare 8000011 (Git installation). Alternativa atual: Workers servindo 6 documentos estáticos de GitHub. Reavaliar Pages após resolver integração ou viabilizar Direct Upload.
- Nenhuma alteração realizada na VPS antiga. MCP SSH bridge local estava offline na sessão; reconciliação da VPS pendente.

## Correção mobile Pipo v2 (10/10/2026)
- PR #3, merge commit `5986a3c3bc1e2791561d3aa72c4e0ef0123424d7`.
- Corrigido somente `games/pipo-patrulha-dos-brinquedos.html`: cachorro central inferior, progresso no topo, última curva afastada, viewport móvel com tabuleiro vertical (480×810), controles de toque e recálculo da pista na rotação.
- Checkpoint específico: `checkpoint/pre-pipo-mobile-layout-20261010` @ `2593d9881a9c4abcb9589c97cfee81cef15d8242`.
- Worker PROD anterior à atualização: etag `d48b4ba1473b7bb41377c5ece2e9bc281279f9edd7fd4cca03af7d2d176c017d`; a branch checkpoint mantém o HTML anterior para remontagem, preservando também os cinco outros documentos.
- DNS e VPS não modificados nesta correção.

## Retorno e escopo
- Checkpoint original do código: `checkpoint/pre-pipo-cloudflare-20261010` @ `1408f6ca943d00f0dff91d644c00256970ac63bc`.
- Branch de trabalho anterior: `feature/pipo-cloudflare-20261010` @ `01342df3ce39342ccddce2a4eee9e53a6f6c22f6`.
- Os quatro HTML anteriores não sofreram alteração.
- Rollback de domínio **somente com autorização ou conforme incidente/roteiro aprovado**: antes, registrar o ID atual do domínio; remover especificamente a Worker custom domain 24c5... e seu DNS apenas se for seguro e autorizado; não alterar registros de outros serviços. Se necessário restaurar código, usar branch de checkpoint.
- Modificar HML/produção separadamente e replicar **o mesmo artefato testado**. Não alterar o DNS principal sem nova validação.

## Próximos passos
1. Abrir portal no celular e computador e validar visual e jogabilidade do Pipo.
2. Quando MCP VPS funcionar, identificar o antigo portal na VPS sem excluir nada.
3. Avaliar custo/uso e migração para Cloudflare Pages via Direct Upload; registrar plano/rollback antes.

## Nova versão v3 — publicada e verificada (11/10/2026)
- Branch de tarefa: `feature/pipo-fases-20261011`; checkpoint anterior: `checkpoint/pre-pipo-fases-20261011` @ `2d22a8621aa947ef0f6c80f6103dc9152ed1a20b`.
- 12 fases em 3 ambientes originais, 4 pistas por mundo, dificuldade gradual, progresso desbloqueado em localStorage.
- Mascote Pipo redesenhado em arte própria embutida como WebP transparente; não alterar outros jogos.
- Mobile retrato dimensiona a **altura lógica** da pista pelo espaço disponível em `visualViewport`, preservando toda a interface sem rolagem vertical.
- Testes locais headless em 320×568, 360×640, 390×667, 390×844, 412×915, 768×1024, 1366×768, 1440×900: nenhum erro de JavaScript, nenhuma rolagem horizontal ou vertical no mobile; testes de desbloqueio fases 1→2→3, seleção e retorno passaram.
- **Publicação concluída:** PR #5, commit merge `4cb64df04aae3636c49e9e82f8c678a953a5eef0`; HML Worker `gamehub-hml-20261010` e PROD `gamehub-prod-20261010` com **etag idêntico** `a17b3455932996b1291b1bd59746e818a3d3b35f443c6b2ae105dc13ffddc921`.
- Cloudflare Browser Rendering (11/10/2026): rota principal e os cinco jogos HTTP 200. No Pipo: viewport 320×568 → canvas 480×627; 390×844 → 480×810; 1366×768 → 1080×690. Progressão e layout também testados localmente com Playwright.
- Sem alterações no DNS ou na VPS; quatro jogos anteriores preservados. Próximo passo: teste manual das fases em aparelho físico e ajuste fino de jogabilidade conforme feedback.
