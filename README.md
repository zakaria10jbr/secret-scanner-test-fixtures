# secret-scanner-test-fixtures

> ⚠️ **All credentials in this repository are fake.** Every API key, access
> key, token, and connection string here is a synthetic, non-functional
> placeholder generated for testing purposes. None of them have ever been
> valid, none are tied to a real account or service, and none pose any
> security risk. It is safe to scan, clone, fork, or index this repository.

## What this is

This repository is a collection of intentionally fake, non-functional test
credentials — AWS access keys, GitHub personal access tokens, Slack bot
tokens, Stripe API keys, database connection strings, private key blocks,
and similar patterns — used to validate the behavior of secret-scanning
tools. It exists so scanners can be tested against realistic-looking
secrets without any risk of exposing something real.

It extends [`atrull/fake-public-secrets`](https://github.com/atrull/fake-public-secrets),
the original fixture repository this project is based on, with additional
custom test cases: extra token formats and providers, config-file and
Terraform-variable placements, database connection strings, and edge cases
like a "mangled" non-standard file format.

As with the base repo, some fake secrets are embedded directly in this
README to test whether scanners pick up credentials in documentation
files, not just in code:

```
AWS_ACCESS_KEY_ID="AKIAJAA49FFSFRFN6AAA"
AWS_SECRET_ACCESS_KEY="u9N1o8s+u3q4uwt9s8dfsdf/afx/d/24449YiNHN"

AKIAJAA49FFSFRFN6BBB
```

## Attribution

The base set of fixtures (the fake AWS key pair, the `BARE-SECRETS` layout
idea, etc.) originates from
[atrull/fake-public-secrets](https://github.com/atrull/fake-public-secrets).
This repository builds on that foundation with additional fixtures and a
CI workflow; all credit for the original concept and initial fixtures goes
to that project.

## Continuous scanning workflow

This repository also hosts a GitHub Actions workflow
(`.github/workflows/secret-scan.yml`) that demonstrates continuous secret
scanning in CI: it runs on every push and on a daily schedule, scans full
commit history (not just the current tree), enforces a `--fail-on high`
gate, and files GitHub Issues for new findings via `--notify-github`
(deduplicated against a cached baseline across runs). Because this repo's
entire purpose is to contain known high-severity fake secrets, the scan
job is *expected* to report findings and fail on every run — that is
correct, intentional behavior here, not a bug in the workflow or the
scanning tool.

## License

MIT — see [LICENSE](LICENSE).
