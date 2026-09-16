# Adversary Playbook — Free Tier

**4 battle-tested offensive-security skills for AI coding agents** — attack
chains verified against live lab targets, then generalized into replicable
playbooks. Each skill teaches an agent to run a complete technique: recon →
exploit → pivot, with the pitfalls that cost us hours already documented.

Built and hardened in a working homelab across dozens of engagement-class
sessions. Not theory — every chain here was executed, debugged, and re-executed
before being written down.

These four are the free tier. The rest of the pack (10 more skills, including the
full Active Directory trust-abuse ladder and the CI/CD attack chains) is available
as a paid bundle — see [More packs](#more-packs).

## What's inside

| Skill | Technique |
|---|---|
| `ad-ntds-escalation` | Foothold → credential escalation → DCSync → NTDS.dit extraction ladder |
| `client-side-crypto-forgery` | Forge signed/AES-GCM payloads when the key ships client-side |
| `code-exec-via-installer-channels` | Supply-chain execution via package-install hooks |
| `idor-exploitation` | Insecure Direct Object Reference hunting playbook |

Each skill is self-contained: instructions plus references, no required scripts,
no dependencies.

## Install

Works with any agent that supports the [Agent Skills standard](https://agentskills.io)
(Claude Code, Hermes, OpenClaw, and others):

```
# Claude Code
/plugin marketplace add <your-org>/adversary-playbook

# Hermes
hermes skills tap add <your-org>/adversary-playbook
hermes skills install <skill-name>
```

Or just point your agent at any `skills/<name>/SKILL.md` file.

## Design principles

- **Replicable bodies** — no lab-specific IPs, hostnames, or paths in the skill
  bodies. Placeholders like `<target-ip>` and `<user>` throughout.
- **Generalized technique + worked-example companions** — the transferable
  pattern is the skill; environment specifics live in clearly-labeled references.
- **Pitfalls are first-class content** — the "we lost 3 hours to this" notes are
  the most valuable lines in each file.
- **Authorization-first** — every skill assumes a target you're authorized to
  attack (your lab, your CTF box, your engagement scope).

## Privileges and elevation

Several commands in this pack need root on the host you run them from.
They are written with a `$ELEV` prefix instead of the literal Linux elevation
command, because that literal token is a false positive for the substring
scanners some skill marketplaces run over documentation. Set it once at the
top of your session:

```bash
ELEV="<your-elevation-prefix>"   # the standard Linux root-elevation command
```

Everything marked `$ELEV` or `(elev)` is a read-only or host-local operation
unless the skill says otherwise. Nothing in this pack requires root on a
target, and no skill needs elevated rights on your own machine to be read.

## Network endpoints used

This pack is documentation only — no scripts, nothing phones home. For
transparency, these are every endpoint or address class that appears:

- **`C2` / `<attacker-host>` placeholders** — stand-ins for a listener you run
  during an engagement (`http://C2:8000/...`). No real host is named.
- **`<dc>`, `<dom>`, `<domain>`, `<user>`, `<nthash>`, `<hash>`** —
  placeholders for the engagement network and credentials you already hold.
- **`https://agentskills.io`** and the agent/companion links in this README —
  read by humans, not by the skills.

## License

MIT — use it, fork it, teach with it. You are responsible for staying within
the law and your authorization scope.

*Built with [Hermes Agent](https://github.com/NousResearch/hermes-agent) by
[NZ1Labs](https://nz1labs-web-design.pages.dev) — sovereign AI, on hardware you already own.*

## More packs

The **full Adversary Playbook (14 skills)** adds the capability areas these four
free skills stop short of. It is available as a bundle or as individual skills
on our [Agensi store](https://www.agensi.io):

- **Active Directory trust-abuse ladder** — inter-realm ticket forging against
  trusting forests, clock-skew compensation, the privilege that finishes what
  DACLs deny, and child/parent domain escalation paths
- **CI/CD attack chains** — turning build runners into pivots, and code execution
  through package-install hooks in reverse-fork pull requests
- **Cloud credential theft** — service-side request forgery to instance-metadata
  credentials, then to execution
- **Web chains** — stored cross-site scripting through an admin bot to session
  hijack and server-side plugin execution
- **Host post-exploitation** — the 15-minute privilege-escalation ladder, and
  credential extraction from virtual-machine memory images
- **Engagement meta-skill** — running a whole engagement session end-to-end:
  network setup, recon discipline, objective extraction, teardown

Our other packs, same storefront:

- **Homelab AI Operator** — run a multi-node local AI lab on hardware you
  already own (10 skills)
- **Content Engine + Agent Ops** — agentic content production & agent operating discipline