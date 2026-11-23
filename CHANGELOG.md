# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and commit messages follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).
This repo is a lab template and has no versions or tags.

## [Unreleased]

### Added

- Backstage `catalog-info.yaml` with technology tags (2026-11-18).
- The P2.2 lab template: the vitrine app, the docker track's Dockerfile and the P2.1 solution workflow
  (`publicar`), which publishes the image of every `main` commit to GHCR tagged with the commit SHA. The
  student extends it so a version tag publishes the version and a pull request builds without
  publishing (2026-11-03).
