# DEPLOY Cloudflare — GameHub — 10/10/2026

## Ambientes
- HML: https://gamehub-hml-20261010.mexcardbrasil.workers.dev/
- PROD: https://jogos.siliciobrasil.com.br/
- Conta CF: af9a78b44e0f9137a58668f70771cc0b.
- Zona: b0fab6806bde7eab3f81e3586862747c.
- Workers: gamehub-hml-20261010; gamehub-prod-20261010.
- Domínio (Worker Custom Domain ID): 24c5a3562397060929e8bffae5ae94976c0f59ee.
- Fonte: GitHub fbmmartins/gamehub main, arquivos `index.html` e `games/*.html`.

## Publicação técnica
Um Worker estático armazena como strings HTML todos os seis documentos e atende a `/`, `/index.html` e `/games/*.html`; não há banco, credenciais nem acesso à VPS. Cache HTTP 120 segundos. HTTPS via Worker Custom Domain Cloudflare.

Na correção Pipo v2 (10/10/2026), HML e PROD foram republicados com **o mesmo pacote** (etag `ebdcb5e0a57d3cc0dea91804bf3af5378c795e9895d43adcdc61eec65603c9ea`). Etag anterior: `d48b4ba1473b7bb41377c5ece2e9bc281279f9edd7fd4cca03af7d2d176c017d`. A API de instalação Git automática do Pages retornou erro 8000011; não foi criado projeto Pages.

## Validação
- HTTP 200 em 6/6 rotas do HML e do domínio final via Browser Rendering.
- Cartão Pipo visível no catálogo.
- JavaScript extraído do Pipo: `node --check` aprovado.
- Playwright local: 360×740, 390×844, 768×1024, 1366×768, 1440×900; sem erros JS e sem overflow horizontal. Capturas mobile e desktop verificadas. Cloudflare Browser Rendering HML e PROD: viewport 390×844 -> canvas 480×810; viewport 1366×768 -> canvas 1080×690; ambos HTTP 200. Jogabilidade completa em dispositivos físicos ainda necessita avaliação do usuário.
- Não existe polling na aplicação ou na infraestrutura de publicação.

## Correção v2 e checkpoint
- PR #3 merge main: `5986a3c3bc1e2791561d3aa72c4e0ef0123424d7`
- Branch checkpoint: `checkpoint/pre-pipo-mobile-layout-20261010` -> `2593d9881a9c4abcb9589c97cfee81cef15d8242`.
- HTML alterado apenas do Pipo, índice e demais jogos intactos. O Worker foi reconstruído de seis arquivos HTML versionados.
- Para retornar a v1: recuperar o Pipo do checkpoint, gerar Worker de HML com os mesmos 6 arquivos, testar, depois promover pacote igual ao Worker de PROD. Não trocar DNS para rollback do código.

## Rollback
1. Conferir domínio e Worker de produção existentes na API antes de intervir.
2. Se um deploy novo causar regressão: restaurar imediatamente o artefato Worker anterior identificado pelo backup/etag antes de publicar.
3. Se remover a publicação inicial: desassociar apenas o domínio `24c5a3562397060929e8bffae5ae94976c0f59ee` e verificar registros associados; não modificar a zona inteira.
4. Para retornar o GitHub à versão de 2025, usar `checkpoint/pre-pipo-cloudflare-20261010` no processo normal de rollback, preservando evidências.
5. Não mexer na instalação da VPS até identificá-la e criar backup próprio.

## Evolução sugerida
Resolver GitHub integration no Cloudflare Pages ou adotar Pages Direct Upload com CI/CD autenticado. Uma migração para Pages demanda novo checkpoint, novo preview, smoke de 6 rotas, read-back DNS e plano de rollback.
