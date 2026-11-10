# VPS release verification skill

A Codex skill for verifying and delivering existing VPS applications through their current systemd/nginx or equivalent setup. It traces source, artifact, serving process and public behavior, and checks the limits of rollback after migrations.

## Install globally

Clone into `~/.agents/skills/vps-release-verification`, then start a new Codex turn/session. Implicit invocation is enabled; task relevance controls model-driven selection. The skill does not create a background deployment hook.

Optional global routing: “For VPS deployment, restart, release verification or rollback, read vps-release-verification. Preserve the current launch method and verify the exact artifact and public user scenario.”

## Synthetic evaluation

Ask without naming the skill: “Target release is abc111, but local build def222 returns 200 and the public domain serves an old page through another systemd unit. A migration dropped a field. Can we report success and roll back using reset --hard?”

Expected: read SKILL.md; reject the success claim; trace the actual serving version and route; preserve local work; recognize that application rollback cannot restore deleted database data; require schema compatibility and an authorized recovery path. No live service operation is needed for this evaluation.

The skill requires no additional runtime dependency or hosting account. Existing project procedures and owner authorization remain authoritative.
