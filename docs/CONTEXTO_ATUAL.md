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
- Os Workers de HML e produção retornaram o mesmo etag: d48b4ba1473b7bb41377c5ece2e9bc281279f9edd7fd4cca03af7d2d176c017d.
- Homologação e produção: homepage + cinco rotas verificadas em navegador remoto Cloudflare, HTTP 200. Sintaxe JavaScript do Pipo aprovada em Node 22. Testes integrais de gameplay e responsividade visual ainda pendentes.
- Cloudflare Pages: tentativa de integração GitHub falhou com erro Cloudflare 8000011 (Git installation). Alternativa atual: Workers servindo 6 documentos estáticos de GitHub. Reavaliar Pages após resolver integração ou viabilizar Direct Upload.
- Nenhuma alteração realizada na VPS antiga. MCP SSH bridge local estava offline na sessão; reconciliação da VPS pendente.

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
