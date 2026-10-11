# CENÁRIOS ORIGINAIS DO PIPO — 12 FASES

Atualizado em 11/10/2026.

## Implementação
As 12 fases mantêm mecânicas, caminhos e progressão da versão 3; cada fase agora tem paleta de fundo, cores do caminho, ornamentos vetoriais e acento visual da interface próprios. Essas escolhas são autorais; não reproduzem cenários de Zuma.

| Fase | Título técnico de ambiente | Motivos e identidade |
|---|---|---|
| 1 | Prado Florido | Verde-musgo, flores amarelas |
| 2 | Lago Azul | Ciano, reflexos e ondas |
| 3 | Jardim Lilás | Lilás, flores rosadas |
| 4 | Floresta de Outono | Verde-oliva e cobre, folhas |
| 5 | Mar de Turquesa | Turquesa, água e conchas |
| 6 | Dunas de Mel | Areia dourada, dunas |
| 7 | Ilha Esmeralda | Verde-esmeralda, pequenas palmeiras |
| 8 | Pôr do Sol | Coral e violeta, faróis e luz quente |
| 9 | Vagalumes Mágicos | Índigo, vagalumes luminosos |
| 10 | Lua de Prata | Azul-noturno, lua e estrelas |
| 11 | Céu dos Cometas | Violeta, cometas |
| 12 | Festival das Estrelas | Roxo, confetes festivos |

## Testes de pré-publicação
- Node `--check` no JavaScript: aprovado.
- Playwright Chromium: 12 fases em cada viewport 320×568, 390×844 e 1366×768 (36 verificações).
- Todas as 12 fases produziram capturas distintas em cada viewport; nenhum erro JS e nenhum overflow horizontal ou vertical no celular.
- Seleção de fases por interface com progresso simulado de teste; não altera o progresso dos usuários.
- Capturas internas: `/mnt/data/pipo_v4_montagem_390.jpg` e `/mnt/data/pipo_v4_montagem_1366.jpg` (apenas ambiente de teste, não commitadas).

## Escopo e retorno
- GitHub: fbmmartins/gamehub.
- Checkpoint anterior: `checkpoint/pre-pipo-cenarios-20261011` @ `61aadaab458bba969c3e9ff6609d2b3d63791680`.
- Alterar somente HTML do Pipo + documentação desta etapa. Outros jogos, DNS e VPS protegidos.
- Homologação: Worker `gamehub-hml-20261010`; produção somente após teste e mesmo pacote validado.
