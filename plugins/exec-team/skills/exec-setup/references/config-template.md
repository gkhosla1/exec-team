# <Project name>: executive team config

_Owner: <name>. Created <date> with /exec-setup. Edit freely; the team reads this every time._

## Project
- **What it is:** <one or two sentences>
- **Stage:** <idea / building / launched / revenue>
- **Docs:** company brief `<path>` · decisions log `<path>` · action items `<path>` · brief log `<path>` · other key docs `<paths>`

## Roster
<For each role: the full role card copied from the role library, edited for this project. Include a project-specific "Watches" checklist.>

### Chief of Staff (chair)
- **Owns:** ...
- **Optimizes for:** ...
- **Always asks:** ...
- **Default skepticism:** ...
- **Watches:** ...

### <Role>
...

## Customer panel
1. **<Persona name>:** <who they are, what they want, what makes them skeptical>
2. ...

## Brief
- **Schedule:** <days> at <time> <IANA time zone> (scheduled task: "<task name>")
- **Deliver to:** one of: <email address> by ~~email · <channel> by ~~chat · notification only. Subject "<Project> brief · <Day> <Date>"
- **Max action items:** 3 · **Length:** under ~200 words plus numbers
- **Include a request for numbers the team can't see:** <e.g. social follower counts on Mondays, or none>

## Sources the team may read
- **~~email:** only messages with the label/folder **"<label>"**. Never read outside it.
  - **Digest:** emails with subject starting "<subject prefix>" from <sender>. If a line `--- machine-readable ---` appears, the JSON after it holds exact numbers.
  - **Partners and services:** <list of senders/programs to watch>
  - **Feedback inbox:** <address forwarded into the label, if any>
- **Web watch:** <topics for 1–3 light searches: competitors, regulation, partner terms>
- **Other connectors:** <e.g. analytics, project tracker; "none">
- **Missing on purpose:** <sources the team can't see yet, so it doesn't pretend>

## Alerts (go to the top of the brief)
_Each alert must be checkable from the sources above._
- <e.g. "no digest in 4 days", "error rate above X", "quota under Y", "partner deadline within 3 days">

---

# brief-log.md format (separate doc, written by exec-briefing)

```
# <Project> brief log
## <YYYY-MM-DD> · delivered by <email|chat|notification> · <n> action items
- Numbers: <name> <value>; <name> <value>; ...
- Web items reported: <short title + URL>; ...
- Missing sources: <none | list>
```
Newest entry first; keep the last ~10.
