# Tag Notes Skill

You are tagging Obsidian notes in a given folder. Your job is to read every `.md` file, determine appropriate tags from the file path and content, then update the frontmatter.

## Instructions

1. If the user specified a folder path, use it. Otherwise ask which folder to process.
2. Run: `find "<folder>" -name "*.md" | sort` to get the full file list.
3. For each file:
   - Read its content
   - Decide on 2–6 tags based on folder path + content
   - If tags need updating, edit only the `tags:` block in the frontmatter using the Edit tool
4. Report a summary of what changed when done.

## Tag rules

- Use **core concept tags** only — no one-off or overly specific tags
- Common tags to draw from (not exhaustive):
  - **Kubernetes**: `Kubernetes`, `pods`, `deployment`, `services`, `namespaces`, `scheduling`, `daemonset`, `replicaset`, `statefulset`, `HPA`, `ingress`, `configmap`, `secrets`, `RBAC`, `networking`, `CNI`, `CSI`, `CRD`, `operators`, `etcd`, `TLS`, `storage`, `volumes`, `cronjob`, `jobs`, `monitoring`, `security`, `Kubestronaut`, `KCNA`, `CKA`
  - **Infrastructure**: `Docker`, `containers`, `Terraform`, `IaC`, `Helm`, `Azure`, `AWS`, `cloud`, `Linux`, `DevOps`, `CI/CD`, `git`
  - **General**: `networking`, `security`, `authentication`, `authorization`, `logging`, `YAML`, `identity`
- Keep existing tags that are already good — only replace generic ones like `KB`
- Each file should have 2–6 tags
- Valid frontmatter format:
```yaml
---
tags:
  - Tag1
  - Tag2
---
```
- If a file has no frontmatter, add it at the top
- If a file already has fully appropriate specific tags, skip it

## Example invocations

```
/tag-notes
/tag-notes 01 - Knowledge Base/02 - AI
/tag-notes /Users/joelplourde/Documents/Obsidian/Vaults/Jojo/02 - Projects
```

When given a relative path, resolve it relative to the vault root:
`/Users/joelplourde/Documents/Obsidian/Vaults/Jojo/`
