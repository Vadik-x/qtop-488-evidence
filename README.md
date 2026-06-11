# qtop Challenge #9 evidence (qtop/qtop#488)

Evidence artifacts for the focused-slice submission from @Vadik-x, kept
outside the main qtop repo per CONTRIBUTING.md (artifact-light policy).
All scans ran 2026-06-11 against qtop develop @ 0ebb451 plus the #488
changes (fork branches: 20260611-488-ci-realign-pvgis,
20260611-488-gitlab-linkage-pilot).

| Directory | Contents |
|---|---|
| repo-sanity/ | Full-tree text-trust audit (report + JSON) and the planted-payload selftest proof: 0 critical, 0 warning on the real tree |
| bandit/ | Bandit SAST: 54 findings (51 low, 3 medium) |
| semgrep/ | Semgrep p/python + p/security-audit: 4 ERROR findings |
| secrets/ | gitleaks (clean) and detect-secrets (3 false positives) |
| deps/ | pip-audit on pinned CI deps: pip 24.0 (5 advisories), pytest 8.2.2 (1) |
| license/ | pip-licenses report of the pinned CI dependency set |
| code-quality/ | ruff GitLab Code Quality JSON (clean tree) |
| coverage/ | Cobertura XML, 45% baseline (139 tests) |
| metrics/ | radon complexity/maintainability and vulture dead-code reports |
| scorecard/ | OpenSSF Scorecard public-API snapshot: score 7.1 (2026-06-08) |
| py36/ | Python 3.6.15 conformance: transcript (10/10 sample gates), qtop SGE render SVG, composite evidence page |

Live CI evidence: https://github.com/Vadik-x/qtop/actions (35-lane nightly
matrix, coverage, scorecard, pytest workflows running on the
20260611-488-gitlab-linkage-pilot branch).

## Live CI runs (fork: Vadik-x/qtop, branch 20260611-488-gitlab-linkage-pilot)

| Workflow | Result | Run |
|---|---|---|
| pytest-qtop (project's own) | green | https://github.com/Vadik-x/qtop/actions/runs/27360321859 |
| coverage-qtop | green | https://github.com/Vadik-x/qtop/actions/runs/27360318838 |
| scorecard-qtop | green | https://github.com/Vadik-x/qtop/actions/runs/27360320428 |
| nightly-matrix-qtop, run 1 | 22/35 green; surfaced 3 real findings | https://github.com/Vadik-x/qtop/actions/runs/27360317465 |
| nightly-matrix-qtop, run 2 (post-fix) | 34+/35 green incl. all PyPy + 3.15-rc | https://github.com/Vadik-x/qtop/actions/runs/27360742733 |

Run-1 findings (fixed in commit 271b381 on the branch): hardcoded
/usr/bin/which in qtop scheduler autodetection breaks minimal images;
pinned CI deps require Python >= 3.9 (importlib-metadata==8.7.1); openSUSE
images lack tar for checkout's tarball fallback.
