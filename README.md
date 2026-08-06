# Hacktivity Skills

34 offensive security skill packs built from 4,831 publicly disclosed HackerOne reports.

Each pack covers one vulnerability class: how people find it, how they exploit it, common bypasses, and real payloads pulled from the writeups. Every example links back to the original disclosure.

Authorized testing and education only. Do not run these against anything you do not own or have written permission to test.

## What's in each pack

| File | Contents |
| --- | --- |
| `SKILL.md` | Playbook plus a handful of example PoCs |
| `payloads.md` | Full set of scored payloads mined from the writeups |
| `reference.md` | All disclosed reports for that class, ranked by severity and bounty |

There are a bit over 3,500 PoC snippets across the `payloads.md` files.

## Install

Clone the repo, then copy the skill folders into wherever your coding agent loads `SKILL.md` packs from:

```bash
git clone https://github.com/sahar042/hacktivity-skills.git
cd hacktivity-skills

# example: project-local skills directory
mkdir -p .agents/skills
for d in */; do
  name="${d%/}"
  case "$name" in
    .*) continue ;;
  esac
  cp -R "$name" .agents/skills/
done
```

Or symlink them into your personal skills directory if you want them available everywhere.

Once installed you can call a pack by name (`xss`, `ssrf`, `sql-injection`, and so on) or just ask about that vuln class and let the agent pick it up from the description.

If you install all 34 at once and some stop showing up in autocomplete, trim the set or mark rarely used ones as name-only in your agent settings. The big `payloads.md` files are only read when something actually opens them.

## Index

| Skill | Reports | Severity mix |
| --- | --- | --- |
| [xss](xss/SKILL.md) | 778 | 18 critical, 149 high, 429 medium, 182 low |
| [access-control-idor](access-control-idor/SKILL.md) | 688 | 67 critical, 141 high, 306 medium, 174 low |
| [info-disclosure](info-disclosure/SKILL.md) | 434 | 32 critical, 53 high, 192 medium, 157 low |
| [dos-resource-consumption](dos-resource-consumption/SKILL.md) | 272 | 11 critical, 56 high, 129 medium, 76 low |
| [memory-corruption](memory-corruption/SKILL.md) | 265 | 28 critical, 71 high, 90 medium, 76 low |
| [business-logic](business-logic/SKILL.md) | 223 | 12 critical, 43 high, 89 medium, 79 low |
| [misc-other](misc-other/SKILL.md) | 199 | 33 critical, 28 high, 76 medium, 62 low |
| [authentication-bypass](authentication-bypass/SKILL.md) | 178 | 31 critical, 42 high, 74 medium, 31 low |
| [code-injection-rce](code-injection-rce/SKILL.md) | 169 | 52 critical, 55 high, 35 medium, 27 low |
| [privilege-escalation](privilege-escalation/SKILL.md) | 157 | 26 critical, 46 high, 55 medium, 30 low |
| [ssrf](ssrf/SKILL.md) | 149 | 28 critical, 39 high, 52 medium, 30 low |
| [path-traversal-file](path-traversal-file/SKILL.md) | 137 | 20 critical, 66 high, 38 medium, 13 low |
| [csrf](csrf/SKILL.md) | 128 | 4 critical, 25 high, 69 medium, 30 low |
| [secure-design](secure-design/SKILL.md) | 116 | 5 critical, 9 high, 35 medium, 67 low |
| [sensitive-data-exposure](sensitive-data-exposure/SKILL.md) | 109 | 13 critical, 18 high, 42 medium, 36 low |
| [open-redirect](open-redirect/SKILL.md) | 108 | 7 high, 39 medium, 62 low |
| [command-injection](command-injection/SKILL.md) | 102 | 55 critical, 25 high, 19 medium, 3 low |
| [request-smuggling-desync](request-smuggling-desync/SKILL.md) | 86 | 9 critical, 18 high, 43 medium, 16 low |
| [sql-injection](sql-injection/SKILL.md) | 81 | 39 critical, 25 high, 13 medium, 4 low |
| [rate-limit-bruteforce](rate-limit-bruteforce/SKILL.md) | 74 | 6 critical, 10 high, 29 medium, 29 low |
| [crypto-weakness](crypto-weakness/SKILL.md) | 49 | 12 high, 25 medium, 12 low |
| [tls-certificate-mitm](tls-certificate-mitm/SKILL.md) | 40 | 2 critical, 6 high, 19 medium, 13 low |
| [misconfiguration](misconfiguration/SKILL.md) | 40 | 4 critical, 8 high, 13 medium, 15 low |
| [input-validation](input-validation/SKILL.md) | 40 | 2 critical, 8 high, 15 medium, 15 low |
| [ssti-injection-misc](ssti-injection-misc/SKILL.md) | 34 | 3 critical, 3 high, 12 medium, 16 low |
| [privacy-violation](privacy-violation/SKILL.md) | 32 | 4 high, 19 medium, 9 low |
| [race-condition](race-condition/SKILL.md) | 30 | 2 critical, 2 high, 8 medium, 18 low |
| [session-management](session-management/SKILL.md) | 29 | 1 critical, 1 high, 13 medium, 14 low |
| [logging-monitoring](logging-monitoring/SKILL.md) | 25 | 24 medium, 1 low |
| [clickjacking-ui-spoofing](clickjacking-ui-spoofing/SKILL.md) | 23 | 6 high, 5 medium, 12 low |
| [phishing-social](phishing-social/SKILL.md) | 14 | 2 high, 1 medium, 11 low |
| [xxe](xxe/SKILL.md) | 12 | 7 critical, 2 high, 2 medium, 1 low |
| [file-upload](file-upload/SKILL.md) | 9 | 2 critical, 1 high, 4 medium, 2 low |
| [prompt-injection-llm](prompt-injection-llm/SKILL.md) | 1 | 1 medium |

## Notes

Source material is public HackerOne disclosures only. Hosts in the PoCs are often redacted or program-specific, and some issues are old, so treat every snippet as a starting point rather than a paste-and-go exploit.

You are responsible for staying inside the law and the target program's rules.

## License

See [LICENSE](LICENSE).

## Author

[Sahar Shlichove](https://github.com/sahar042)
