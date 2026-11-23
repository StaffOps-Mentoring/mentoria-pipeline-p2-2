# Handoff

Last updated: 2026-11-23 by Backstage docs-standard rollout · branch `main`

## State

**Lab template repo** (not a student's solution): state = what the P2.2 lab currently hands to students.
`main` holds the vitrine Go app (identical to `mentoria-apps/apps/vitrine` today but without its tests),
the docker track's multi-stage Dockerfile, `chamado.txt` with a placeholder for the student's token, and
`.github/workflows/publicar.yml`, the P2.1 solution: on push to `main` it builds amd64 plus arm64 and pushes
`ghcr.io/<repo>:<sha>`. The student extends it so a version tag publishes the version and a pull request
builds without publishing. The catalog marks it `type: template`, `lifecycle: production`. GitHub Actions
is disabled on this repo and it has no runs, tags or releases. The lab's own status is not consistent across
the private `StaffOps-Mentoring/mentoria-roadmap`: its README lists P2.2 as ready, while its `HANDOFF.md`
and `docs/handoff/pipelines.md` (last P2.2 entry 2026-11-05) record the verify battery as half done. That
pipelines handoff is the working log; this repo has nothing in flight.

## Done

- Backstage catalog and technology tags ([`297cf61`](https://github.com/StaffOps-Mentoring/mentoria-pipeline-p2-2/commit/297cf61), [`9171a8d`](https://github.com/StaffOps-Mentoring/mentoria-pipeline-p2-2/commit/9171a8d))
- The P2.2 template: vitrine, Dockerfile and the P2.1 solution workflow ([`c172fc7`](https://github.com/StaffOps-Mentoring/mentoria-pipeline-p2-2/commit/c172fc7))

## In progress

- No open pull requests and no open issues here. Check with `gh pr list -R StaffOps-Mentoring/mentoria-pipeline-p2-2`.
- The lab's verify battery (in `mentoria-roadmap`, not here): per its pipelines handoff, nine scenarios and
  the variants mark remain, blocked until image version `505c2d76…` is deleted from the measurement fork's
  package `lab-p22-medida`.

## Next steps

1. Finish the P2.2 battery in `mentoria-roadmap` once the blocking package version is deleted (from that
   repo's pipelines handoff).
2. Align the lab status between the mentoring README and its handoff (suggested, inferred).

## Decisions

No ADRs here. Lab decisions (the starting workflow is the P2.1 solution; a PR build must never publish) are
recorded in `mentoria-roadmap`.

## Risks and open questions

- `go.mod` declares `module github.com/StaffOps-Mentoring/mentoria-pipeline-p2-1`; whether that is intended
  is not recorded (open question).
- The workflow pins actions by major tag (`@v5`, `@v3`, `@v6`), not by SHA.
- The app is a copy of `mentoria-apps/apps/vitrine`; a fix there needs a deliberate copy here.

## How to verify

```bash
gh api repos/StaffOps-Mentoring/mentoria-pipeline-p2-2/actions/permissions --jq .enabled   # false
grep -n -A3 '^on:' .github/workflows/publicar.yml                        # push to main only
docker run --rm -v "$PWD:/src" -w /src golang:1.26-alpine sh -c 'go vet ./... && go build -o /tmp/app .'
docker build --build-arg VERSAO=dev -t vitrine:dev .
```
