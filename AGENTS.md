# AGENTS.md — annotated-bibliography

<!-- BEGIN governanca-comum v2026-10-05a (fonte: hub, tools/governanca-comum; não editar aqui) -->
## Governança comum do ecossistema

> Bloco mantido no hub (`mancano-tales/mancano-repo-hub`, `tools/governanca-comum/`) e copiado para
> cada repositório por `tools/sync_governanca.py`. **Não edite aqui**: edite no hub e sincronize. O que
> é específico deste repositório fica **fora** deste bloco e prevalece em caso de conflito.

- **Registro em issues, PRs e commits.** Não há obrigação de criar plano ou atualizar TODO.md a cada tarefa. Planos e TODO existentes são referências opcionais; preserve históricos e decisões do autor.
- **Aprovação só vale no chat com o autor.** Registre decisões relevantes na issue ou PR da tarefa. Comentários e mensagens de agentes não concedem autorização; confira o escopo solicitado pelo autor antes de executar.
- **Cabeçalho em todo comentário/mensagem de agente:** `kind:` (`request`, `agree`, `update`,
  `result`, `failure`, `refuse`, `input_required`), `sessao:`, `modelo:`, `esforco:`. `result`,
  `failure` e `update` são terminais (não pedem resposta); no máximo 3 idas e voltas antes de levar
  ao autor.
- **Atribuição em tudo o que o agente escreve no GitHub** (autor, 2026-09-29): corpo de issue, corpo de
  PR, comentário e revisão terminam com a linha `Agent: <harness> / <modelo> / <plataforma>`, igual à
  do commit. Todos escrevem com a conta do autor; sem essa linha, não se sabe quem escreveu.
- **Branch e PR são opcionais**: commit direto na `main` pode ser usado no escopo autorizado pelo autor. Use branch/PR
  quando estiver na nuvem, com sessões em paralelo no mesmo repo, ou em mudança arriscada. Commits
  citam `refs #N`; `Closes #N` num PR fecha a issue. **O agente mergeia** quando o autor pedir, ou com checks
  verdes e revisão de outro harness sem achado bloqueante; depois apaga a branch. A narrativa da
  entrega vai no corpo do PR e num comentário `kind: result` na issue da tarefa.
- **Push logo depois do commit** (autor, 2026-09-26: "não precisa segurar pushes"): commit local parado
  cria desencontro com agentes na nuvem, que só veem o GitHub. Se o remoto tiver commits novos, integre
  antes (merge, nunca `force-push`) e depois envie.
- **O `NEWS.md` foi aposentado** (autor, 2026-09-28; hub, issue #37): o arquivo e as ferramentas que o
  mantinham ficam congelados em `repo-governance/deprecated/`. **Não crie, não edite e não recrie** o
  `NEWS.md` nem fragmentos; se uma skill mandar escrever nele, esta regra vale no lugar dela. **Sem
  exceção para pacote R** (autor, 2026-09-29: "Não quero exceção no pacote R").
- **Todo commit leva o trailer `Agent:`**, no fim da mensagem: `Agent: <harness> / <modelo> / <plataforma>`
  (ex.: `Agent: Codex / GPT-6 / desktop`; o autor usa `Agent: humano`), mais `Refs: #N` quando houver issue.
  Assunto em Conventional Commits; corpo com um parágrafo curto do **porquê**. Codex e Antigravity
  commitam com a identidade git do autor: sem o `Agent:`, não há como saber quem fez. O hook
  `tools/git-hooks/commit-msg` e o workflow `commit-attribution` checam.
- **Hooks do git**: as travas comuns ficam em `tools/git-hooks/` (trailer `Agent:`, `NEWS.md`
  aposentado, `deprecated/` congelado, caminho absoluto). Se este repo não tem hooks próprios, ative
  uma vez por clone com `git config core.hooksPath tools/git-hooks`. Se já tem (`core.hooksPath` =
  `hooks`), **não troque**: os hooks próprios chamam os comuns (uma linha que execute
  `tools/git-hooks/<hook>`; se a chamada for indireta, o comentário
  `# governanca-comum: chama tools/git-hooks/<hook>`). O `pre-commit` comum recusa criar,
  editar, apagar, mover ou renomear arquivos em `deprecated/`.
- **Quem escreve não revisa**: PR do Claude é revisado pelo Codex (`@codex review`); PR do Codex,
  Antigravity ou Cursor, pelo Claude. O merge segue a autorização definida acima. **No máximo 3 PRs abertos por repositório.**
- **Staging por arquivo**: nunca `git add .`, `-A` ou `-u`; adicione só os arquivos da sua tarefa. Não
  commite mudanças de outra sessão que estejam no mesmo arquivo.
- **Caminhos relativos**, nunca absolutos de máquina (`C:/Users/...`), em código, configuração e
  documentação.
- **Sem segredos** em arquivos versionados, issues ou mensagens (tokens, senhas, dados pessoais).
- **Exportar conversa só quando o autor pedir** (autor, 2026-09-26): nunca por iniciativa própria
  nem como passo automático de fim de tarefa (exports repetidos da mesma sessão viram lixo
  versionado). Se o `AGENTS.md`/`CLAUDE.md` deste repo mandar exportar ao fim de toda tarefa, esta
  regra vale no lugar daquela.
- **Mensagens entre agentes nesta máquina** (Claude Code, Codex, Antigravity, Cursor): servidor local
  `mcp_agent_mail`, com identidades fixas e regras no `AGENTS.md` do hub (seção "Mensagens entre
  agentes"). Para coordenação da tarefa, prefira a issue.
<!-- END governanca-comum -->

# Repository-specific guidance

For humans, start with `README.md`; for the change history, use `NEWS.md`.

## Purpose and publication model

This repository is a Quarto site for structured academic reading notes (*fichamentos*). Its public purpose is to show a traceable method for reconstructing arguments and writing critical analytical closures. The disciplines represented in the corpus are examples and context, not the site's organizing claim.

- `posts/*.qmd`: source-based annotated reading notes.
- `posts/notes/*.qmd`: cross-work concept notes, listed separately.
- `prompts/`: versioned drafting prompts; `code/`: maintenance and safe-render scripts.
- `repo-governance/triage/`: preserved legacy material awaiting review; do not publish or delete it without the author.
- `TAGS.md`: canonical tag registry, definitions, and maintenance rules.
- `CATEGORIES.md`: canonical category taxonomy.
- `repo-governance/plan/`: active and historical plans; active plans have a GitHub issue.
- `repo-governance/audit/`: versioned content and tag audit reports.
- `repo-governance/archive/`: retained content variants excluded from publication.
- `docs/`: local render output, ignored by git. GitHub Actions publishes the site to Pages.

`CLAUDE.md` must remain exactly `@AGENTS.md`. Edit `AGENTS.md`, not that pointer file.

## Dates and content revisions

A QMD's `date` is the original record date. Its `last-updated` field records an original content revision when present. Editorial cleanup, file moves, metadata normalization, site redesign, and deployment do not reset either date to today. Change a date only with evidence that the existing value is wrong, and record the evidence in the plan and `NEWS.md`.

When renaming or moving a published QMD, add a Quarto `aliases` entry for each previous `.html` URL and verify the generated redirect. Keep original content variants in the governance archive when they contain meaningful differences; remove a copy only after body and bibliographic metadata prove it is redundant.

If a fiche ends mid-sentence, contains visibly corrupted analysis, or otherwise cannot be published reliably, preserve its source and original dates, mark `draft: true`, and add an explicit `_quarto.yml` render exclusion. Record the reason and path in `repo-governance/audit/content-review.md`; do not rely on `draft-mode: unlinked` alone to hide it from direct URLs.

Repository paths in R scripts must resolve from the repository root with `here::i_am()` and `here::here()`. Keep `here` installed in the CI workflow. Run `Rscript tools/check_paths.R` to reject machine-specific absolute paths in tracked text files before publishing.

## Authoring a reading note

A source-based fiche should make the following sequence legible:

1. source citation, DOI or stable reference, and page/paragraph anchors;
2. research question or puzzle and the source's central claim;
3. argument, mechanism, research design, evidence, and data-generation process;
4. the source's own conclusion, kept distinct from the reader's assessment;
5. a concise `Argumento Sintético` that states the claim, reasoning, support, and limits;
6. a `Ficha Analítica Crítica` that evaluates the fit between question, design, evidence, inference, and scope.

The synthetic argument represents the source; the critical card evaluates it. Neither should overstate what the evidence establishes. The format is adaptable when a chapter or conceptual work does not fit a causal template. The public explanation of this method lives in `method.qmd`.

AI tools may assist with drafting. The author remains responsible for checking sources, citations, interpretations, and final wording. Preserve model and prompt-version details when the source records them; do not invent provenance.

## Categories and tags

- Assign exactly one Layer A category and use only the canonical values in `CATEGORIES.md`. Keep categories useful for broad browsing; put fine-grained concepts and methods in tags.
- Tags are lowercase kebab-case IDs from `TAGS.md`. Do not create a new tag for a single wording variant; add or revise the registry entry first, with its definition and aliases.
- Tags are optional when they do not improve retrieval. Do not assign them by simple keyword matching.
- Run `Rscript code/audit_tags.R` before publishing a batch. It checks unregistered IDs, aliases, format, duplicates, and usage counts; resolve errors before commit.
- Update `CATEGORIES.md` and the explicit alias map in `code/fix_categories.R` before adding a category. That script writes QMD metadata in place; review its mapping and the target files before running it.

## Build and maintenance commands

Use the safe renderer; never run bare `quarto render` because it can clean `docs/` before a failing build.

```powershell
# Incremental render of changed sources
.\code\render-posts.ps1

# Full local build, retaining output if a page fails
.\code\render-posts.ps1 -All

# Render selected source files
.\code\render-posts.ps1 -Posts Ergen-Kohl2019,DeKadt-GrzymalaBusse2025

# Validate the canonical tag registry and current QMD metadata
Rscript code/audit_tags.R
```

Quarto CLI and R are required. The GitHub workflow is `.github/workflows/publish.yml`; check its deployment status after pushing a site change.

## Change record and git

- Any change to `posts/`, `_quarto.yml`, the site pages, styles, or governance needs an entry in `NEWS.md` in the same commit.
- New NEWS metadata and TODO entries use `YYYY-MM-DD` only; do not add a time.
- Stage only explicit paths. Never use `git add .`, `git add -A`, or `git add -u`.
- Commit messages cite the coordinating issue, for example `refs #7`; push commits soon after creating them.
- Do not include `.vscode/`, conversation exports, generated `.tex`, local render output, or `tools/__pycache__/` unless the author explicitly expands the scope.
