# CONTEXTO ATUAL — GameHub

Atualizado em: 2026-10-10

## Estado encontrado
- Repositório: fbmmartins/gamehub (público, legado de 2025).
- Branch principal: main @ 1408f6ca943d00f0dff91d644c00256970ac63bc.
- Site existente em index.html, com quatro jogos HTML5 preservados em games/.
- A VPS antiga ainda não foi reconciliada: SSH bridge indisponível; nenhum deploy ou remoção efetuado na VPS.
- DNS jogos.siliciobrasil.com.br não foi encontrado na zona Silício Brasil na consulta de 10/10/2026.

## Escopo desta mudança
- Incluir como quinto jogo o Pipo — Patrulha dos Brinquedos.
- Acrescentar card no catálogo com contagem atualizada de 4 para 5.
- Preparar publicação **isolada**, inicialmente em Cloudflare Pages sem modificar produção antiga.
- Não alterar os quatro jogos existentes, recursos da VPS, sistemas ou DNS de outros projetos.

## Rollback / checkpoint
- Branch: checkpoint/pre-pipo-cloudflare-20261010 @ 1408f6ca943d00f0dff91d644c00256970ac63bc
- Recuperação do código: retornar a main/checkpoint no GitHub ou reverter somente os arquivos desta branch.
- Cloudflare: criar projeto Pages isolado sem domínio principal; caso falhe, desligar/remover somente a configuração nova após registrar seu estado.
- Cutover do domínio apenas após validação e promoção.

## Próximo passo
Validar diffs e smoke de cinco rotas em Preview do Cloudflare Pages, revisar mobile/desktop; só depois configurar jogos.siliciobrasil.com.br.
