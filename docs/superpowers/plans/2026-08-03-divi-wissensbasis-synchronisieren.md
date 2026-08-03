# Divi-Wissensbasis Synchronisieren Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Die öffentlich sichtbare Skill-Dokumentation, Wiki, NAS-Wissen und die GitHub-/Gitea-Repository-Kopie erhalten einen nachvollziehbar gleichen Reifegrad.

**Architecture:** Das GitHub-Repository bleibt die veröffentlichte Skill-Quelle; die GitHub-Wiki vermittelt die Themen als lesbare Einstiegsseiten. Das NAS bleibt die ausführliche interne Wissensbasis. Eine gemeinsame Synchronisationsseite beschreibt Abdeckung, Quellenhierarchie und Pflegeweg.

**Tech Stack:** Git, GitHub, Gitea, Markdown, WordPress 7, Divi 5.

---

### Task 1: Reifegrad transparent machen

**Files:**
- Modify: `README.md`
- Create: `docs/WISSENSSTAND.md`
- Create: `/Volumes/AI-Workspace/AI_Knowledge/08 AI WISSEN/11 - WordPress/00 - Orientierung/Wissensstand Divi und WordPress.md`

- [x] Beschreibe die verbindlichen Quellen und ordne Skill, Wiki und NAS verständlich ein.
- [x] Kennzeichne vorhandene Themen als nutzbar; offene Themen nur dort, wo wirklich Inhalt fehlt.
- [x] Halte fest, dass keine Zugangsdaten, Backups oder Kundendaten veröffentlicht werden dürfen.

### Task 2: Wiki-Einstieg fertigstellen

**Files:**
- Modify: `MGD_Divi5-Dev_SKILL.wiki/Home.md`
- Create: `MGD_Divi5-Dev_SKILL.wiki/WordPress-7-Grundlagen-und-Betrieb.md`
- Create: `MGD_Divi5-Dev_SKILL.wiki/Plugin-Entwicklung-sicher.md`
- Create: `MGD_Divi5-Dev_SKILL.wiki/Divi-5-Visual-Builder-und-Designsystem.md`
- Create: `MGD_Divi5-Dev_SKILL.wiki/Divi-5-Module-und-Erweiterungen.md`
- Create: `MGD_Divi5-Dev_SKILL.wiki/KI-Agenten-Playbook-für-WordPress-und-Divi.md`

- [x] Ersetze die irreführenden „in Arbeit“-Links durch echte, verständliche Seiten.
- [x] Jede neue Wiki-Seite enthält einen Nutzerteil, einen Entwickler-/Agententeil, Sicherheitsgrenzen und Links zu den ausführlichen NAS-Themen.
- [x] Ergänze einen einheitlichen Stand und die Quellenhierarchie.

### Task 3: Repository und Remotes abgleichen

**Files:**
- Modify: `CHANGELOG.md`

- [x] Prüfe Markdown, sensible Daten und Git-Status.
- [x] Committe den Skill-Stand nachvollziehbar und pushe ihn nach GitHub.
- [x] Übernehme denselben Commit-Stand nach Gitea; ohne Zugangsdaten im Repository oder in der Dokumentation abzulegen.
