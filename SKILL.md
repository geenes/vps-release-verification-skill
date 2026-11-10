---
name: vps-release-verification
description: Use when deploying, restarting, verifying or rolling back an existing application on a VPS with systemd, nginx or comparable process and reverse-proxy tools, especially when the served version may differ from the intended release.
---

# VPS release verification

Read the existing deployment instructions, scripts, service configuration and relevant changes first. Preserve the current repository, stack, host, working directory and launch method. Discover actual unit names, ports and proxy routes; never infer them from an example. Use only the host and access already authorized by the user.

## Define the release evidence

Before mutation, establish the intended commit and any intentional local diff, build inputs, artifact identifier/checksum, serving process, public route, and success criteria. Uncommitted changes are not part of a commit hash: identify which inputs actually produced the artifact. Check the working tree without exposing secrets or overwriting others' work. Reuse the existing release procedure rather than creating another platform or service.

Check environment/configuration requirements without printing credentials. For migrations and asset changes, establish old/new application compatibility, data-loss risks and the supported recovery path. Application rollback does not undo a database migration or restore deleted data. Do not create profile/database backups automatically; if unique data needs protection beyond existing recovery, explain the specific risk and obtain the needed owner decision before that operation.

## Execute within scope

When deployment is authorized, build and switch only the intended artifact and service using existing scripts. Inspect the exact process working directory/executable/environment source and loaded unit configuration as permitted. Validate a changed nginx configuration before an authorized reload. Avoid broad restarts, reset --hard, deletion of release directories or changes to unrelated units. Authorization to inspect or verify is not authorization to deploy or roll back.

## Verify the served result

Trace intended source -> built artifact -> serving process -> proxy route -> public response. Inspect available release metadata, checksums or asset identities rather than trusting a 200 status. Where identity cannot be established, mark it unverified. Compare the backend and public path, including cache/CDN/service-worker effects where relevant; use the existing cache procedure within scope.

Run the requested user scenario against the target public address and check relevant health/log evidence with secret-safe output. A healthy local endpoint can belong to another process or version. Record the observed version, route and behavior; distinguish build success, service health, artifact identity and functional success.

## Recovery and report

Use explicit failure criteria and the existing recovery mechanism. Before rolling back, check authorization, previous artifact availability and schema compatibility. Stop and report uncertainty when rollback would lose data or cannot restore compatibility; propose the smallest viable recovery or forward fix. Never claim rollback restored data without verifying it.

Report the intended and observed version, checks performed at the actual target, failures and remaining checks. Do not report a release as successful based on a build, process start, another commit's local response or an executor's statement.
