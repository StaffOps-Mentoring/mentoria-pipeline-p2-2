# AGENTS.md

Template repo for lab **P2.2** ("version by tag, pull request that builds without publishing") of the StaffOps
mentoring pipelines track: the vitrine app, its Dockerfile and a starting `publicar` workflow that students
extend in their fork. The lab statement and verify script live in the private
`StaffOps-Mentoring/mentoria-roadmap` (`labs/pipelines/P2.2-versao-e-pull-request/`).

## Branches

| Branch | Use |
|---|---|
| `main` | The only branch, and the template students fork. Changes go through a pull request |

## Commands

Go and Docker run in containers, never on the host.

```bash
docker run --rm -v "$PWD:/src" -w /src golang:1.26-alpine sh -c 'go vet ./... && go build -o /tmp/app .'
docker build --build-arg VERSAO=dev -t vitrine:dev .
docker run --rm -p 8080:8080 -e LOJA_NOME=demo vitrine:dev
```

Workflow: [`.github/workflows/publicar.yml`](.github/workflows/publicar.yml), push to `main` only. GitHub
Actions is **disabled on this repo**, so it never publishes from here; it runs in student forks.

## Rules

- New documentation, commit messages and PR text are in English. The README is student-facing Portuguese
  lab content: change it only together with the lab in `mentoria-roadmap`.
- Conventional Commits (`fix(vitrine): ...`, `docs: ...`).
- Update `CHANGELOG.md` `[Unreleased]` and the affected doc in the same commit as the change.
- Never commit secrets. `chamado.txt` holds a placeholder line; students write their own token in their fork.

## Pitfalls

| Pitfall | What to do |
|---|---|
| "Improving" `publicar.yml` with tag or pull request triggers | Don't: adding them is the lab. It must stay the P2.1 solution |
| `go.mod` declares `module github.com/StaffOps-Mentoring/mentoria-pipeline-p2-1` | Inherited from the P2.1 template; whether that is intended is not recorded, so ask the lab owner before renaming it |
| The app is a copy of `mentoria-apps/apps/vitrine` | A fix there does not reach this repo by itself; copy it deliberately |

## Docs map

| Need | Read |
|---|---|
| What the student does | [README.md](README.md) and the lab statement in the mentoring portal |
| The app's env vars and routes | [mentoria-apps README](https://github.com/StaffOps-Mentoring/mentoria-apps#vitrine) |
| Current state | [docs/handoff.md](docs/handoff.md) |
| History | [CHANGELOG.md](CHANGELOG.md) |
