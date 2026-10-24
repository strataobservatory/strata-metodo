# Observation method · Strata Observatory · version 11.1

**What this document is.** The complete description of how we observe, written for someone who **does not trust us**. It is sealed alongside every observation it produces, so that ten years from now one can know not only what we measured but **how we measured it back then**.

**What it is not.** It does not argue that what we measure matters. It recommends nothing and scores nobody. And it does not describe how the archive is dated: that is in the verification procedure, which is published separately and works without access to our data.

**Scope of this version.** It covers **Layer 0 (the census)**, and only what is executed. Claims —Layer 1— and behavioural probes —Layer 2— **are not implemented and are not described here**: promising a method that is not executed would be exactly what this project does not do. Their design is in a separate document, which is not sealed, does not travel in the copies and is not this method.

**Who maintains it.** Strata Observatory, maintained by Luis Calvo Ruiz. Its up-to-date contact details are at https://github.com/strataobservatory. This text names who and points to where to look, but writes down no email address or identifier: those details change, and this text, once sealed, does not.

---

## 1. The observed universe

Three classes of object, which are the same ecosystem seen at three levels:

1. **Registries and directories.** The sites that list the others.
2. **Services listed in them.** The bulk of the population.
3. **Services and agents with a record of their own on their domain**, found by probing standard paths on already known domains.

**Scope: global.** There is no geographic axis —these objects have no nationality— and no language filter.

### The inclusion rule

An object enters the census if it appears in any of these sources:

- **Enumerable lists** — the four named below, and only those. A fifth is recorded as declared and not yet incorporated, with no coverage state.
- **Dependency trail**, up to **two levels** from an already censused object. At the second level only what belongs to the classes above enters, not every transitive dependency. **It does not run**: it was attempted once, on 2026-09-02, and yielded no object, because its source is the package repository, which is not read.
- **Frontier**: probing of standard paths on known domains, and monitoring **filtered by name pattern** of the public certificate registries. **The daily pass does not run it.** The probing was done only once, on 2026-09-02, and found 34 services with their own card on 23 domains. The monitoring of the certificate registries **has never been done**: their exclusion signal has forbidden it to us since the first day.

**That filter is part of the frontier of the universe**, not an implementation detail: whatever falls outside the pattern is recorded as outside the inclusion rule, **not as non-existent**.

**What runs every day.** Of the three mechanisms above, **only the enumerable lists are walked in every pass**. The services the frontier found and that its rule admits (below) are looked at every day at their own address, one request each, but **no further domain has been probed**. So since 2026-09-02 **the universe grows only through the lists**, and whatever the frontier would have found afterwards is not there. Until version 7 this was not said, and the executed inclusion rule kept in the archive still described that day's sweep. From version 8, the pass rewrites it every day with what was done that day. Running the frontier again, and how often, would change what is observed: a new version, with its discontinuity.

### The enumerable lists, named

Version 1 said «public registries and directories» without naming any, and that vagueness had a measurable consequence: two sources were implemented, and the other three **were not excluded: they were absent** — not appearing even among the discards, so that nobody could notice they were missing. A universe that is not named cannot be audited.

They are traversed in this order:

| Order | Source | Identifier in the code |
|---|---|---|
| 1 | The protocol's official registry | `registro-oficial-mcp` |
| 2 | The Smithery directory | `directorio-smithery` |
| 3 | The Glama directory | `directorio-glama` |
| 4 | The PulseMCP directory | `directorio-pulsemcp` |

**The identifier column is not decorative.** It is what makes it possible to check by machine that the method and the instrument say the same thing: if this table names a source the census does not attempt, or the census attempts one this table does not name, verification fails. The defect that motivated version 2 is thus turned into a barrier.

Adding or removing a source from this table is **changing the observed universe**, and therefore a modification of the method with its entry in the history — never a configuration change.

### A declared source not yet incorporated

There is a fifth source the project decided to observe and does not read yet. **It is not in the table above and carries no coverage state**: a source's three states describe an attempt, and with this one nothing is attempted. Nor is it kept quiet: it is recorded here, with the day from which it is recorded this way and why, and it is shown in the history and in the dashboard.

| Source | Since | Why it is not incorporated yet |
|---|---|---|
| `repositorio-npm` | 2026-09-17 | we know what it permits —its terms allow replicating the public registry through its interfaces—, but there is no deterministic walk yet: its search returns at most 5,000 results, in an order that moves, and the keyword query declares 72,182. Reading it that way would be reading by position, the defect that already retired two readings. Until version 7 it was recorded every day as `ilegible`, and it was not: what it permits was known |

Incorporating it will be, like any change to the table above, a new version of the method, and the day it enters will be a declared discontinuity over that source.

### A directory that asks to leave

**A directory can ask us to stop reading it, and the request is honoured.** Ceasing to read a source is a change in **our** reading, so it enters a version of this method as a declared discontinuity, and that version **names the source**, below and with the day: without naming it nobody could know why the census changed, and a directory is a public service, not a person. The source leaves the table of enumerated lists and from that day it is not read and carries no coverage state. **Its objects that were known only through it leave by exclusion of their source**: an exit sealed with that reason, with no removal and outside every rate, just like the exit by change of rule (section 10); that day they are recorded one last time, not observable by policy, and their sealed history stays. **Those that another source also brings stay**, and from that day they are looked at through it; those looked at in their own address stay as they were. Exclusion is by address (section 2), and the source's address does not cover its objects' addresses.

| Source | How | Since |
|---|---|---|

Today no source has asked to leave.

### Glama, by its sitemap and in tranches

Up to version 8.4 Glama was recorded **excluded** every day: its programming interface was attempted, and its `robots.txt` closes it to our agent. But the same site publishes **a sitemap with one entry per server**, which it does not close, just like PulseMCP. From version 9 on Glama is read **by the set that sitemap declares**, and its interface is no longer attempted. Only the server sub-sitemaps are read; those of remote connectors are another class of object and are not read. Of each entry only its identifier is kept: it is the only unambiguous thing on a page meant for people.

**It does not enter all at once, because it does not fit.** Measured on a copy of the census on 2026-10-05, requesting nothing but the sitemap: 96,340 servers in ten sub-sitemaps, none of them the same object as one already censused, 8 entries per object that enters. All in one day would take more than three quarters of the day's capacity. So it enters **in tranches**, and the partition is the source's own —its sub-sitemaps, in the order of its index—, never "the first N" of a list:

- **Tranche 1**: sub-sitemaps 1 to 3. **Tranche 2**: 4 to 6. **Tranche 3**: from 7 to the last one its index declares that day.
- **Never on consecutive days**: between one tranche and the next, at least one whole ordinary day, sealed and measured.
- **Each tranche is a declared discontinuity** over the source, with its day, in the table of section 8: on that day, its new entries are not births.
- **A guard in the same run that seals, which rejects instead of warning.** On a tranche day, before registering anything, the run adds the entries of the **last sealed ordinary day** —counted in the archive— and **what the tranche adds on top of that day**, counted with the entries it brings: each entry not in the census counts as a whole new registration, each entry of the tranche already there as one coverage, and each equivalent name in another directory as one link. **The coverage of what entered in earlier tranches is not added**: it is already inside the ordinary day, which covered it too, and counting it again would count the same day twice. If the sum exceeds **half the day's capacity** (2²⁰ entries; half, because the margin must also cover the echo of the following day), **the tranche does not enter that day**, and both figures are written in that day's state of the source, inside the seal. A rejected tranche does not enter on another date without a new version of the method.

**While not everything its index declares is read, Glama is recorded with the cut stated**: which sub-sitemaps are read and which have not yet entered. On those days Glama supports no absence and no birth, because what appears in or goes missing from a read sub-sitemap may come from one not yet read: measured, the partition shifts a few entries a week at the borders between sub-sitemaps. From the day of the last tranche it is read in full, and sub-sitemaps the index adds later are read as part of it.

**Glama is not read again on the same day if it goes down**: its list moves, and another reading would be another sample.

### Every source is recorded with its outcome, and there are three of them

On every pass, every source in the table is recorded in one of these states. **None may be omitted in silence.**

| State | What it means |
|---|---|
| **Enumerated** | It was traversed in full, or it is stated where it was cut short |
| **Excluded** | Its exclusion signals forbid the enumerable surface. It is recorded and we stop |
| **Unreadable** | It could not be known what it permits. Not knowing whether it is permitted is not permission |

**«It was not attempted» and «we were not allowed» are different things and cannot produce the same report.** The first speaks about us; the second, about the site. Confusing them would turn an omission of ours into a refusal by someone else, which is a false statement about a third party.

**A source that goes down is not given up on at the first try, and when it was read is stated.** Each page that fails in transport is requested up to three more times, with growing waits of 20, 60 and 180 seconds; a refusal is never requested again. If the enumeration is still cut short, the source is read in full again **once the other lists are done**, and if it is still down, **a third time about two hours later**; meanwhile the day is not sealed. The third is only attempted if it fits within the same UTC day: a list read the next day would be the next day's list. If that fails too, the day is sealed with its gap, as before. **This only applies to sources whose list does not move from one day to the next** —today, the official registry—: on a list that moves, another reading would be another sample, and keeping the one that comes out clean would be choosing by the result. **For every source, every day, when it was read and in which round is sealed** —the first, the second or the third—: the lists of a single day may be read hours apart, and whoever compares them has to be able to see it. The time is our own clock's, and it is declared as such. It is sealed from 2026-10-03: earlier days do not have it.

### The frontier's inclusion rule, path by path

From version 10 on, the frontier's rule **names every path that is probed**, and what each one decides:

| Path | Decision | Agent protocol |
|---|---|---|
| `/.well-known/mcp.json` | in | `mcp` |
| `/.well-known/agent-card.json` | in | `a2a` |
| `/.well-known/agent.json` | in | `a2a` |
| `/.well-known/ai-plugin.json` | in | `openai-plugin` |
| `/.well-known/oauth-protected-resource` | **out** | — |

- The last one is out because it is **infrastructure metadata**: it does not declare itself a service for agents, and it shows up because the probe passed that way. **What only shows up because our probe passed that way is not part of the universe**: a by-product of the observation method is never an observed object, and admitting it would not broaden the census, it would change what it is a census of.
- **Also out, the domain that serves the same content, byte for byte, on paths of different protocols**: demonstrably it is not a declaration. The same content in `agent.json` and in `agent-card.json` does not count: that is the migration of a protocol, and both paths belong to the same one.
- **A path this table does not name stops the pass** before anything is requested, instead of guessing whether it is in: admitting by mistake is sealed forever, and stopping costs a day.

**The services the frontier found are judged by this rule only once**, on the first day version 10 ran. Those the rule leaves out **leave the census by change of rule** (section 10), never as removals; the others stay and receive their two attributes (section 4). That evaluation is preceded by **the same capacity guard as Glama's tranches**: if the last sealed ordinary day plus what the evaluation is going to seal exceeds half the day's capacity, nothing of it is written, and it is tried again the next day with that day's figure.

Probing new domains is still not done: version 10 changed **what counts** of what was already found, not what is searched for.

### Smithery: the total of each page, and where each duplicate falls

Smithery is read by pages, with the day's seed and **a hundred at a time** (`pageSize=100`). A hundred is the most it accepts: with 150, 200, 250 and 500 it answers with an error (measured on 2026-10-10 and 2026-10-12). That size is in the versioned code since 2026-09-04; for the two days before, no code remains that says it. Like the seed, it is part of how the source is read, and whoever wants to repeat a day's reading needs it: changing it is a new version of this method. About one day in six, **one row arrives duplicated and another is missing**, and that day the reading is recorded with its cut: not walkable. Two causes give that same final count —a new entry that falls in the part already read, or a server that changes position while it is being read—, and what tells them apart is **the total each page declares** and **on which page and at which position each duplicate falls**. Up to version 9 only the last page's total was kept, and of the duplicates only how many: the evidence arrived every day and was thrown away.

From version 10 on, in Smithery's state of each day, **the series of totals of all its pages** is sealed and, for each duplicated row, **its page, its position and where it was seen the first time**. **It is an observation and governs nothing**: a reading with duplicates is still recorded not walkable, as before. And if a sealed row says there were duplicates, that day's state has to declare its cut: otherwise the archive would contradict itself.

**This census does not aim to be complete. It aims to be deep and consistent.** One cannot enumerate what one does not know exists, and saying otherwise would be the archive's first lie.

---

## 2. How observation is done

**The agent always identifies itself**, in the header of every request, with its name —`strata-observatory`—, the address of the project page, which links in one step to where every version of this document is published, and its contact email. A record built by hiding attests to nothing.

**Public surface only, in the strict sense**: reachable without anyone else's credentials, without circumventing any control and without accepting terms that forbid it.

**A site's exclusion signals are respected as an absolute rule.** Whatever cannot be observed that way is recorded as **not observable by policy** and remains in the census with its reason.

**Following a redirect to another host is making a new request to another site**, and it is governed by everything that governs a request. Before following it, **the exclusion list** is checked for the destination (below); then **its `robots.txt`**, requested once per pass and per host like anyone else's; and **the courtesy of one request per second per destination host** is respected, shared among all the origins that lead to it. If any of the three prevents it, it is not followed, and the origin is recorded **not observable by policy** with the reason «destino de la redirección» (destination of the redirect): it is not "could not be looked at" nor a failure of the observed, because we decided it. Another host is another host name: from `http` to `https` with the same name it is not, and from `a.ai` to `www.a.ai` it is. A redirect within the same host is followed as before, checking the list. And a `robots.txt` that redirects to another host whose policy is not known yet is not followed: no reading is opened inside another one, and not knowing what is allowed is no permission. Up to version 11 a redirect to another host was followed without asking the destination anything, while this section already said that exclusions are an absolute rule: it was a false statement.

**And declared USE signals are respected too.** Some sites declare in their `robots.txt`, next to the exclusions, how they allow their content to be consumed —search, input to models, training, and with what scope—. **Our use is reference and archival: we keep what an object declares about itself so that we can later say what it said and when. Nothing is trained on it, and third-party content is not redistributed.** Each site's particular signal is not copied here: it is recorded **on every pass**, with its date, because it is a declaration *by the observed* and can change any day — and a third party's sentence frozen inside our doctrine would stop being theirs. Not declaring one is neither permission nor prohibition, and that is recorded too.

**Zero load on the observed.** We ask whether something has changed before downloading it: the hash is kept on every pass and the content **only when the hash changes**.

**If an object blocks access, the block is recorded and we stop. It is not worked around.** The block is a datum in itself.

**Whoever does not want to be observed can ask us to stop, and what we promise is by address.** We stop the addresses we are given; a card of theirs published at another address is another address, and to stop it they have to name it to us. Since objects are not linked by their owner (below), we cannot know that a card in another directory belongs to the same project. Up to version 11 this paragraph said that whoever did not want to be observed could stop us, which promised more.

**The automatic way is their own `robots.txt`.** If it names our agent, it is respected like any exclusion in the next pass, without anyone on our side having to read anything. The name is recognised as it would be written by someone who has seen it in their access log: with or without a version, with the whole header pasted, with different capitals or separators.

**For whoever cannot touch their `robots.txt`, the alternative is a written request**, to the project's email or by opening an issue on its page. **It is fulfilled at most five days after it arrives**, and that is the deadline met in the worst month, not in a normal one. Whoever maintains the observatory looks at the email and the issues at least every three days, and every time they look the day is written down, even if there was nothing. Every pending request is written down too, with the day it arrived. **The watchdog raises an alert**, as it does for a missing day: if more than three days pass without looking, if a request passes the deadline, or if an issue stays open longer than it. Fulfilling it means adding the address —a domain, or a path inside a site, such as an account on a hosting site— to a **declared list** that travels with the instrument's code, and answering whoever made it. The list holds the address, the day the request arrived and how it arrived; **never who made it**.

**The list is read at the start of every pass, before any source**, and if it cannot be read, the pass does not start: not knowing whom not to look at is no licence to look at everyone. What it covers **receives no request** —not even the one for its `robots.txt`, nor one arriving through a redirect— **and nothing about it is recorded**: no registrations, no facts, no absences.

**The series of an object the list covers is closed with a single entry.** On the first day the list covers it, the object is recorded one last time as **not observable by policy**, with its identifier, the day and the reason «a petición» (on request): not the address, not the channel the request came through, not when. Never with a gap, because a gap without a reason cannot be told apart from a failure of ours. **From the next day on it is only counted**: it is no longer in the day's coverage, and the list's trace (section 11) seals how many series close that day and how many were already closed, without names. **And every day the number of addresses excluded on request is sealed, in the day's coverage and without names**: without those numbers, a day's coverage could be narrower than the previous one's without anyone seeing why. What was sealed before the closing stays, including what links its identifier to its name, because no day is resealed. Up to version 11 the excluded object's coverage was sealed every day with its identifier and the day the request arrived, and every extra day named it once more.

**Whoever verifies the archive with the list in hand checks that no request of the day falls under it** once its deadline has passed: not the address of an object that was asked for something, not where the request led, not any address in what was recorded that day. It is a stronger check than one row per object with a label, and it needs to name nobody.

**A directory can also ask to leave** (section 1). That is something other than an address on this list: it is ceasing to read a source, and so it goes in a version of the method, which names it.

**Nothing behind someone else's credentials is ever observed.** The instrument does not know how to send them, and a refusal is a block (above).

**What is kept of each object is what the object itself or the source listing it publish about it**: its name in that source, the public address where it is published —as the sources publish it—, the attributes it declares and the hash of its declaration. That address is sometimes that of a repository under a person's account, because that is how hosting sites name things: the object is the repository, not the account. **Objects are not linked by their owner**: nothing is grouped, counted or derived by account, author, maintainer or organisation. And whoever owns one of those addresses has what is said above: they can ask to leave.

**Nothing enters the census through any door other than the sources named in section 1.** The pass refuses to register anything from any other, and the verifier checks on every sealed day that each registration comes from one of them. That is why nothing arrives through the relationship of whoever maintains the observatory with their clients, nor by any other way.

---

## 3. The coverage states

Every object, every day, is recorded in one of these states. **Coverage is a first-class datum**: a recorded gap is information, and a silent gap would be a lie that would contaminate the entire archive.

| State | What it means |
|---|---|
| **Observed** | It was looked at and a response was obtained |
| **Not observed** | It was not looked at. The reason is recorded |
| **Failure of the observed** | It was looked at and the object did not respond correctly |
| **Blocked** | The object refused access |
| **Not observable by policy** | It could technically be looked at, but doing so would breach section 2 |

A period without a coverage record does not exist: if it is not recorded, the archive is incomplete and verification says so.
**A missing object counts as `observed`, with its reason**, and not in a sixth state: we looked and it was not there, which is not the same as not having looked at it. This holds for what is missing from a list walked in full and for what is looked at in its own address and is missing from it. What is done with that absence is in section 10.
**And the state of each SOURCE on each day is part of the sealed archive.** This is not the same as the above: that speaks of an object, this of an entire list, and it is recorded as *enumerated*, *excluded* or *unreadable*, never silently omitted (section 1). It goes inside the seal **because it is the evidence on which every claim of birth depends**: an object is recorded as born under observation because the source that carries it was walked in full the day before, and anyone who cannot check that row cannot check the birth. An archive that asserts the second without sealing the first is asserting something it does not support.
**A day that was not observed carries no source rows. None.** If a day's pass does not happen, that day is not measured afterwards —that would record today's state as if it were then—: it is sealed as not observed, with every object *not observed* and its reason, and **without any source row**. The three answers a source can give describe an attempt, and on that day there was none; what happened, happened to the day, not to the sources. And the day's header **says so**: `no_se_corrio` (not run) if the pass did not happen, and then there is no row at all; `corrio_sin_observar` (run without observing) if it was attempted and nothing could be observed, and then every source carries its row and none is *enumerated*. The distinction lives in a stated value, not in a gap. It is not a fourth source state: the closed vocabulary is the source's, and this one is the day's. **A lost day costs one day**: the next pass seals it before its own, because the chain admits no gaps.

---

## 4. What is recorded about each object

**An identifier of our own**, assigned the first time and **never reused**. External names are aliases with their date.

**Its attributes**, which live on the object and are not repeated in every observation: class, provider or responsible organisation, declared type or functional domain, protocol and technical surface, hosting, licence, provenance, the source that discovered it, parent object if it came in by dependency, and whether it **was born under observation** or already existed when we arrived.

Attributes **are sparse series, not fields that get overwritten**: almost none of them ever change, and when one does, an entry is added with its validity date. Without that one could not ask how the objects of a given type behaved in 2027, because one would need to know what type they were *back then*.

**What the object declares and what we classify are stored separately and marked.** The first is a measurement; the second, an interpretation — and our classification carries its own method version.

**How we reach an object and what it declares itself to be are two axes, and they are not mixed.** The first —through which list or mechanism, with what birth resolution— is already in the irreversible attributes of the new entry, and decides what can be computed with it. The second decides which population it belongs to, and **it is an attribute, not a class**: that way rates by protocol are given without inventing classes, and a new protocol comes in as one more value. For every service with its own card that the frontier's rule admits (section 1), two are classified, with this method's version and **with the date of the day they are recorded, not that of the new entry** —that we know it from today does not mean it was so since we arrived—:

- **`protocolo_de_agentes`**: the agent protocol it declares to speak —`mcp`, `a2a` or `openai-plugin`—, according to the path where it publishes its card. It is not the technical surface (`protocolo`, which is `https`): they are two axes with two names.
- **`cumple_minimo_de_formato`**: `si` or `no`, against the minimum of its format. **Conformity is an attribute, not a frontier**: what fails a strict check is, proportionally, careless and half-finished manifests, which are the ones that die most, and requiring it to enter would bias mortality downwards, which is the figure this archive exists to publish. With the datum per object any rate can be computed both ways, and the difference is in turn a measure. It is judged again every time the declaration changes, and the entry is added with its date. While an object lacks it, its card is requested in full, without the conditional request of section 2: the body is not kept, and a "not modified" response brings nothing to judge. **What is not a JSON shaped as an object is not judged**: it is not a badly made declaration, it is that there is no declaration there any more, and that is a missing day (section 10). The conformity it had stays as it was.

The minimums, with their source:

| Format | Minimum | Where it comes from |
|---|---|---|
| `ai-plugin.json` | `schema_version`, `name_for_model` and the `api` object | its author's official example manifest |
| A2A (`agent-card.json`, `agent.json`) | `name`, `skills` as a list, and `url` or `supportedInterfaces` | what its versions have in common: the current one requires eight fields, and requiring them would leave most out |
| `mcp.json` | a name (`name`, `title` or `serverInfo`) and some connection field (`url`, `endpoint`, `endpoints`, `transport`, `transports`, `remotes`, `server`, `servers`) or capabilities field (`capabilities`, `tools`, `resources`, `prompts`) | **ours**: there is no ratified standard, and it is stated. It only describes; it does not decide who enters |

What is not a JSON shaped as an object meets no minimum. The objects from the lists, and the four directories, do not carry a protocol yet: recording it for them will be another version.

**The hash of the complete declaration**, every day. The content, only when the hash changes.

**The address the request ended up at, when it is not the one requested.** If the object's address redirects to another, where it ended up is kept, that day and alongside its observation. It is the evidence that an old address leads to a new one —what tells an object that moved from one that died—, and it arrived with every request and was thrown away. **It is kept and not used**: it plays no part in identity (section 5), in absence (section 10), or in any other rule until what it means has been measured; using it will be another version of this method, and a discontinuity. It is kept from 2026-09-27: earlier days do not have it, and that does not mean there were no redirects.

---

## 5. When two observations are of the same object

It matters more than it seems: if a name change is recorded as a death and a birth, the mortality we publish would be false.

**Today an object is recognised by its name in the source, and none is merged.** The same name, whichever list it comes from, is the same object, and each list that brings it adds a sighting. But each directory names things in its own namespace —the official registry `io.github.x/y`, Smithery `x/y`, PulseMCP `x-y`—, so in practice no object has sightings in more than one list: **a service listed in four directories is four objects** (section 10).

**The only thing recorded across lists is a note of suspected link.** When an object is registered, if another one from another list has the same name once each directory's prefix is removed, the possible relation is noted with that evidence. The note merges nothing: it allows them to be reunited later.

> **Splitting is recoverable; merging is not.** Joining on weak evidence stops counting deaths and makes survival come out optimistic. Splitting too much somewhat overstates mortality, and the link note allows them to be reunited later. **That pessimistic bias is assumed deliberately, and it is stated.**

**An object that changes its name** is recorded as an entry that stops being there and another that appears, with a note only if their names match as above. That overstates the mortality of entries, and it is assumed.

**Nothing is ever joined by owner** (section 2): the account, the author or the maintainer are not evidence of identity, and they are not used for anything.

Every identity decision is recorded with its evidence. Revising one means adding an entry, never rewriting.

**A ladder that merges on declared or structural evidence is designed and not connected.** Its design is in the separate document named in the scope. Connecting it would change what is counted, so it will be another version, and a discontinuity.

The other half of this —when an object stops being there, and why that is not the same as a death— is in **section 10**.

---

## 10. Absence and death

**Why this section is numbered 10 and sits here.** Because section numbers **are not shifted**. The archive's closing documents and the instrument's comments cite "section 5" or "section 8", and those citations have to keep meaning the same thing ten years from now. It is the same rule that governs the census's own identifiers —the counter only goes up, not even after a death— and the same one that forbids relabelling a sealed observation. It is placed after section 5 because it is its natural continuation: that one decides when two observations are of the same object, this one when an object stops being there.

This section is **the mirror of the birth rule**, and until version 4 it did not exist. The method spoke of mortality and survival in five places and the instrument only marked a death when an identity was split in two: an object that stopped appearing in a list walked in full was recorded nowhere.

### The three gates

An object **is missing** on a day if all three hold:

1. the source that listed it was walked **in full and without a cut** that day —enumerated, and with no declared cut—;
2. the object does not appear in that walk;
3. and that holds for **every** source that listed it.

The third is the one birth does not need and this one does: an object can be in four directories and disappear from one. **If any of its sources was not walked in full, it is not missing** — we did not get to look, which is different from looking and not finding. A cut source cannot kill anybody.

### The absence of what is looked at in its own address

The three gates above are lists walked in full, and something that is looked at in its own address cannot be missing from a list that does not list it. From version 11 on **the services with their own card that the frontier's rule admits** (section 1) have their own rule, judged every day on what their path answered:

| Reason | What was seen that day |
|---|---|
| `ruta_404_o_410` | missing: the path was requested and answered 404 or 410 |
| `respuesta_200_sin_objeto` | missing: the path answered 200 with something that is not a JSON shaped as an object |
| `dominio_en_b_prima` | missing: the path gave a declaration, and its domain serves that day the same body, byte for byte, on paths of different protocols |

**Only what the table names is missing, and only an admitted declaration reappears.** Anything else is not a missing day, and there are two cases that are not confused:

- **It is not missing, because it could not be looked at**, if it was a failure of the observed, a block or a path its `robots.txt` forbids. That day neither confirms the absence nor denies it: it is a calendar day, not a confirmed day.
- **Any other observed answer is not judged**:

| The rest | What was seen that day |
|---|---|
| `no_juzgado` | neither missing nor reappearing: the path answered something other than one of the three missing reasons or an admitted declaration —a 204, a 304 of something not recorded as a declaration—, and it is sealed with its code |

A day not judged does not confirm the absence or close it either: it counts as a calendar day, not as a confirmed day. **It is sealed with its code** in the object's coverage that day, which is still recorded `observed` —we looked and it answered—, and **the days not judged are counted in the trace** (section 11), because if that figure grows it is a suspicion about how we look before it is a fact about the world. A redirect is followed; one that cannot be followed is recorded as a failure of the observed, and one that our exclusions do not let us follow —the list, the destination's `robots.txt` or its courtesy, section 2— is recorded not observable by policy, with the reason «destino de la redirección». In both cases it could not be looked at.

- **Each missing day carries its reason, that day's**, because the three cases are told apart on the day they are looked at and not afterwards. If two fit, the path's own one rules: B′ is judged only among the paths that gave a declaration that day.
- **B′ is judged every day**, over the domain's paths requested that day, and when it falls the whole domain is missing. The two objects that show it are sealed, and whoever verifies recounts it with the hashes sealed that day.
- **It reappears** when the path gives an admitted declaration again. As long as the last thing it gave is not recorded as a declaration —a 404, a 200 without an object, or a day before version 11—, its path is requested in full, without the conditional request: a "not modified" of something that was not a declaration cannot say it is still there.
- What the frontier's rule has not admitted yet, or what left by change of rule, is not judged here.

**The A2A migration is not a death.** For each missing day on one of the two A2A paths, the other A2A path of the same domain is asked, that same day, as another door (below). Relating the two paths of a domain is not linking by owner: the domain is part of the name the object itself declares. **Nothing is aggregated or published by domain.**

**Its magnitudes are its own.** The absences that enter and the reappearances of the frontier (`ausencias_entran_frontera`, `reapariciones_frontera`) are not added to those of the lists, neither in the series nor in the quarantine. **They have no floor, and nothing of them is held back**: as long as they have no `N` there is no consequence to hold back. Their floor will be derived from the same window with which their curve is measured, and fixed at the same time as their `N`. Until then they are published apart, saying they have no floor.

### Absence and death are two different things

| | when | what it is |
|---|---|---|
| **Absent** | from the **first** day it is missing | a **reversible** fact, recorded and undoable |
| **Reappeared** | if it comes back | **a datum, not an erasure**: it measures how noisy the source is |
| **Death** | after **N** days absent | and **dated on the first day of absence**, not the Nth |

That death is **back-dated to the first day of absence** is what makes everything else work: the archive is an instrument of dates, and the date on which something stopped being there is the day it stopped being there, not the day we became convinced of it.

**Two spans are counted, not one.** A day on which the source could not be walked in full neither confirms the absence nor denies it: it does not close the episode —it is not a reappearance— but neither does it count. That is why each episode carries its **calendar days** and its **confirmed days**, and they are different.

### N is not fixed, and that is stated

**`N` has no value in this version, and no death is declared from absence.** A number chosen by judgement is measured before it is accepted, and `N` cannot be measured without knowing how many absences revert. The first measurement, over the archive's first five days, says why it cannot be 1: **270 episodes, of which 156 have already closed and all 156 reappeared the next day.** *That measurement was made on the archive as it was then and cannot be recounted from today's sealed record: it stands as the reason for not fixing N = 1, not as a checkable figure.*

And there is no need to hurry. **Because death is back-dated, nothing is lost by waiting**: if `N` is fixed three weeks from now, the deaths still come out with their correct date. The only thing that cannot be recovered is not having started to record.

### What is measured: listed entries, not servers

What this rule measures is not the mortality **of servers**: it is the mortality **of listed entries**. Section 5 does not join the observations of two directories —no object in the census has sightings in more than one list—, so the same service listed in two directories is two objects. If it disappears from one and remains in the other, it counts as a death in the first, and **it is right that it counts**: its entry there ceased to be. That is why the sentence that gets published has to say what is measured:

> *"Of the N entries listed in the protocol's official registry on 2 September 2026, X % no longer appeared thirty days later."*

Less reach than "servers" would suggest, and the precision that other sentence would not have. **And a consequence for the third gate:** as long as each object is listed by a single list, missing from *all* its lists means missing from its own. The gate stays written as it is, and the day a ladder that joins two directories is connected, it will act on its own.

**What the frontier's absence measures is not listed entries: it is declarations published on their own domain, at a path.** Its sentence states the path or the protocol, the universe it runs over and conformity both ways, for example: *"Of the N A2A declarations published on their own domain on day D, X % no longer answered with an admitted declaration thirty days later (Y % among those that met the minimum of their format)."* A listed service that also has its own card is two objects: **they are never added up in the same rate**.

### Other doors of a source

A source can have **more than one door**, and they need not say the same thing. On 2026-09-10, 33 absences from the Smithery directory came out that were not due to our reading —its listing, walked in full twice, no longer enumerated them— and that still existed: its search found them. Missing from the listing while remaining in the search **is not the same as missing from everywhere**, and it has a state of its own.

That is why each confirmed absence from a source with other doors is asked, that same day, at each of them, and **each answer is sealed as a separate observation**: *present*, *absent* or *could not be asked*, which is a result and not a gap.

| Source | Other door | What it governs |
|---|---|---|
| `directorio-smithery` | the entry page, by exact name | death: it is deterministic |
| `directorio-smithery` | the search, by exact name | nothing: it is sealed as an observation |
| `frontera-rutas-estandar` | the other A2A path of the same domain | death: it will require silence on both |

**The entry page rules.** The listing still measures absence; the entry page, which answers the same every time it is asked, governs death; the search ranks by relevance —*absent* there only means it did not appear among the first results for its exact name— and speaks of a reranker, not of the object. It is kept because it is a fact, and it decides nothing. A death, when there is one, **will require silence at the entry page**.

**On the frontier, the other door is the other A2A path of the same domain.** It is asked with the answer it already gave that day if it is an object of the census, and if it is not, with one request, in full and with the same exclusions as any other. **It registers nothing**: what it finds is sealed as another door and nothing more.

### The quarantine of what has no precedent

**The consequence is held back, never the recording.** What is observed is always sealed. What is held back is what is **derived** from it —the absences that enter on a day, the reappearances of a day— when it has no precedent: if the day's value exceeds **both** a declared multiple of the largest earlier value already consumed for that magnitude **and** an absolute floor declared for it, everything of that magnitude on that day is sealed **in quarantine**. It stays in the archive, with the figure that triggered it and the bar it was measured against; but **it is not consumed**: it does not enter the series, does not count as open, and does not bring anything closer to a death.

| Parameter | Value |
|---|---|
| Multiple of the quarantine threshold | `3` |
| Absolute floor of `ausencias_entran` | `42` |
| Absolute floor of `reapariciones` | `4` |
| Series the floor comes from | from `2026-09-10` to `2026-09-14` |
| Quarantine term | `14` days |

The threshold has **two terms, and both must be exceeded**. The multiple is **relative to the series itself**, so that it need not be readjusted as the population grows; what is held back does not count towards that maximum: if it did, the first absurdity would make the second one invisible. The floor is **absolute**, so that a series still short, or made of zeros, does not hold back the ordinary movement of a day: against zeros, the multiple alone would be triggered by any figure.

**How the floor is derived, sealed together with it so that it can be redone.** The floor of each magnitude is the largest daily value of that magnitude in the clean series: the days of the comparable series —from 2026-09-10, the first on which the sources that can be read were read in full with today's reading— up to 2026-09-14, the last one sealed before it was fixed, counting what exists: without what was annulled by a retraction and without what was held back. Day by day, the absences that entered were 42, 14, 11, 13 and 9, and the reappearances 0, 2, 4, 0 and 0. So the floor sits above the largest ordinary daily movement of the clean series and far below the incident of 2026-09-08 (11,710). Whoever verifies the archive from outside recounts that series from what is sealed and checks that it gives these floors. Changing a floor, or the series it comes from, is a new version of the method.

**It leaves quarantine in two ways, and both are sealed**, one entry per object: **lifted**, when a person decides the figure belongs to the world and not to the instrument; or **expired**, when the term passes without a decision —and then it counts, marked as never resolved, and the day it expires is flagged as the day it opened was—. If what is decided is that the figure was false, it is not lifted: it is retracted, entry by entry (section 8). How long a quarantine took to resolve is in turn a fact about the instrument.

**Deaths** are also a derived magnitude, and will enter here when they exist; today there are none, because `N` is not fixed.

### Leaving by change of rule is not dying

An object can stop counting in the census without anything having happened to it: because **we** narrowed the inclusion rule. That is not a death —it is still alive; what changed was the rule— and sealing it as a removal would put false deaths into the only series that is the product. That is why it has **its own disposition, "exit by change of rule"**, dated and stated as ours, with the rule that changed and its evidence. And the test to recognise it on the spot: if the question *"what happened to the object?"* is answered *"nothing"*, what happened was ours, and it cannot be written with the vocabulary of the world.

- **It is sealed on the day it is decided, and that day it still counts**; from the next one it is no longer part of the population and is not looked at. Like a retraction, first it is sealed and then the database moves.
- **Nothing is deleted**: the object, its attributes and its sealed days stay as they were.
- **It enters no rate, neither before nor after the change**: it is not a removal and does not open an absence, and whoever computes a rate over earlier days has to remove it from those days too, because under today's rule it would not have been there.
- An object leaves this way only once, and cannot be recorded as a removal at the same time.

The first ones are the `oauth-protected-resource` services the frontier found (section 1).

**The exit by exclusion of its source is of the same kind** (section 1): that of the objects that only a directory that asked to leave brought. It is ours —we stop reading that source because it asked us to—, it carries its own reason, it is sealed on the day it is decided, it is not a removal and it enters no rate.

An exit by change of rule only happens when **our** rule changes: when a version of the method enters, once, over what was admitted before. If an object of the frontier stops meeting the rule because **the world** changed —its path stops giving a JSON shaped as an object, or starts giving the same body as another path of another protocol—, that is not a change of rule: it goes through its absence (above).

### Which way this rule fails

**Towards "it has not died".** An undeclared birth impoverishes a cohort of ours; a false death is **a false claim about a third party**: saying that something ceased to exist when it exists. It is the same family as "it was not attempted" versus "we were not allowed", and in that family this method always picks the same side.

Declared consequence, like the overcount in section 7: **any mortality we publish will be a lower bound.** It is stated, not disguised.

**The frontier's mortality does not see the death of the domain.** A domain that stops resolving, or does not accept connections, is never missing: it is recorded as a failure of the observed, or as not observable by policy if what did not answer was its `robots.txt`, and that could not be looked at. It is probably the most common end of a self-hosted service. So its lower bound is a different one from that of the lists, where a withdrawal is seen, and **the two bounds are not added or compared without saying so**. To be able to measure it, for each transport failure on the frontier its class is sealed:

| Class | What happened |
|---|---|
| `no_resuelve` | failure of the observed: the domain name did not resolve |
| `no_conecta` | failure of the observed: the name resolved and the connection did not open, or was cut |
| `se_agota_el_tiempo` | failure of the observed: it did not answer, or did not finish answering, in time |

It is a datum, not a coverage state: the five states of section 3 do not change. **It is kept and governs nothing** until what it means has been measured.

### What is sealed, and which coverage state applies

**Every confirmed day of absence goes inside the seal**, tied to the day its episode began, and so does the reappearance that closes it. It goes in for the same reason the state of each source entered in version 4: it is the evidence on which every claim of mortality will depend, and anyone who cannot recount it cannot check the claim. **All** confirmed days are sealed and not just the first, because what must be recountable is how many days the absence was confirmed, not how many days went by.

**An absent object still counts as `observed`**, with its reason written. There is no sixth coverage state: the five in section 3 answer *"did we manage to look at it?"*, and here we did look —the list was walked in full, or its path was requested and answered—. *"Was it there?"* is another question, with another shape —an interval, not the state of one day—, and that is why it is recorded separately. Putting them in the same column would repeat the very error section 1 expressly forbids: confusing "we were not allowed to look" with "we looked and it was not there".

---

## 11. The mechanisms this method declares, and their trace

**A document is not proof of a behaviour.** This method describes what the archive does, and that description does not check itself: for four sealed versions it declared three mechanisms —the frontier, the dependency trail and the monitoring of the certificate registries— of which one had run only once and another never, and they were discovered one by one and by chance. That is why, from version 10 on, **every mechanism the method declares is named in the table below, with its cadence, and every sealed day carries the trace of each one**.

The trace goes **inside the seal**, in the day's coverage, and says of each mechanism **which day it speaks of**, **whether it ran** and **what it looked at**, with its zeros: a mechanism whose only proof of having run is a zero cannot be told apart from one that did not run, so what was looked at is stated and not only what was found. If it could not be known whether it ran, the trace says so, and says why.

**A declared mechanism without a trace is a failure, not a footnote.** The pass does not seal a day that lacks the trace of one, nor one that brings a trace of something the table does not declare; and whoever verifies the archive from outside checks, with the table of the method sealed that day, that the set of declared mechanisms is exactly the set of those that bring a trace. That a trace says "it did not run" is not a failure of the archive: it is a datum about that day, and it stays as such.

Three cadences:

- **`cada-pasada`**: it runs inside the pass that seals the day, and its trace speaks of that same day.
- **`del-dia-anterior`**: it runs after the seal —the attestation, the copy, the watchman, the look at the mail, the backup watchman—, so its trace is sealed by the next day's pass, and speaks of the previous one. A day that was not run seals no trace of anything, and what ran after it is not traced: it is said here so that it is not read as not having run.
- **`no-se-ejecuta`**: the method declares it and says it does not run. It cannot have a trace.

| Mechanism | Cadence | What it does |
|---|---|---|
| `lista-de-exclusiones` | cada-pasada | reads the list of what stops being observed on request, before any source, and counts without names the series that close that day, those already closed and what leaves by exclusion of its source (sections 1 and 2) |
| `listas-enumerables` | cada-pasada | walks the sources in the table of section 1 and records the state of each one |
| `otra-vuelta-a-una-fuente-caida` | cada-pasada | reads again a source whose list does not move if it went down in transport (section 1) |
| `tramos-de-glama` | cada-pasada | decides whether a Glama tranche enters that day, with its guard (section 1) |
| `paginacion-de-smithery` | cada-pasada | seals the total each Smithery page declares and where each duplicate falls (section 1) |
| `control-semanal-de-pulsemcp` | cada-pasada | once a week, also walks PulseMCP's pagination and notes it down; it records and does not decide (section 8) |
| `fichas-propias-a-diario` | cada-pasada | looks every day, at their address, at the services with their own card the frontier found (section 1) |
| `regla-de-la-frontera` | cada-pasada | applies the frontier's inclusion rule to what is already in the census, with its guard (section 1) |
| `redirecciones` | cada-pasada | keeps where the request led when it is not the one requested (section 4), and counts those that went to another host as a new request and those that could not be followed (section 2) |
| `ausencias` | cada-pasada | applies the three gates of absence from the lists, and the absence of what is looked at in its own address, with its magnitudes apart (section 10) |
| `otras-puertas` | cada-pasada | asks the other doors of a source about its absences (section 10) |
| `cuarentena` | cada-pasada | holds back what has no precedent (section 10) |
| `retractacion` | cada-pasada | seals the retractions decided before the database moves (section 8) |
| `atestacion` | del-dia-anterior | deposits the day's summary in the layers that attest it (verification procedure) |
| `confirmar-anclas` | del-dia-anterior | confirms the pending anchors and fetches the public record of each deposit (verification procedure) |
| `verificar-capas` | del-dia-anterior | checks the archive's attestation layers (verification procedure) |
| `copia-diaria` | del-dia-anterior | copies the archive off this machine and checks the copy |
| `vigia` | del-dia-anterior | checks that the pass happened and warns of whatever does not add up, including the deadline of requests (section 2) |
| `mirada-al-correo` | del-dia-anterior | looks at the mail and the project's issues and writes the day down (section 2) |
| `vigia-suplente` | del-dia-anterior | from outside this machine, checks twice a day that the archive has sealed |
| `frontera-sondeo-de-rutas` | no-se-ejecuta | probing standard paths on known domains (section 1): it was done once, on 2026-09-02 |
| `frontera-registros-de-certificados` | no-se-ejecuta | monitoring the public certificate registries (section 1): it has never been done |
| `rastro-de-dependencia` | no-se-ejecuta | following dependencies from a censused object (section 1): it was attempted once, on 2026-09-02 |

**The backup watchman lives on the witness repository's host, and the only record of it expired there.** Its run history is kept by the provider —ninety days, according to its own documentation, which is a third party's claim about itself—. That is why the pass asks it every day, through its public interface and without credentials, what runs it had the previous day, **seals it in the trace** and **publishes it in the witness repository**, one line per run, in an append-only file (`vigia-suplente.txt`). The first time it dumps everything the provider still kept, from 2026-09-05. It is the same provider that hosts the backup watchman, and that is why what it answers is not believed: it is sealed with its date, which is what can be done with a third party's testimony about itself.

**The absence of what is looked at in its own address is not a separate mechanism**: it leaves its count inside the trace of `ausencias` —the objects it judged, how many enter, continue and reappear, by reason, how many could not be looked at, how many days not judged and with which code, what the other A2A path said, the open ones and that its magnitudes have no floor—, and the question to the other A2A path is counted by `otras-puertas`, like all its questions.

Adding a mechanism to this table, removing one or changing its cadence is changing what the method declares: a new version, with its entry in the history.

---

## 7. What is not measured

Stated in full, because it is what makes the rest citable.

- **Real behaviour is not measured in this version.** Everything above compares what is declared against what was declared before. That a service does what it says **is not checked**: that is Layer 2 and it does not exist.
- **The census is not complete.** It only reaches what the sources in section 1 expose, within the declared filter.
- **An object may change and change back** between two daily observations without our seeing it. The resolution is the cadence.
- **Of the first day's population it is not known when it was born, and it never will be.** That an object was born under observation is asserted by comparing today's list against yesterday's, not by believing the date the object declares —that one cannot be validated—. On the first day there is no yesterday to compare against, so **everything censused that day is recorded as already existing** and stays out of any birth cohort for good. Only what appears from the second day onwards has a whole measurable life. And **"walked in full yesterday" means walked in full yesterday with the same reading**: on the day of a declared discontinuity over a source, none of the new entries that source brings is a birth —its reason is the discontinuity—, because what appears that day may be only what we have started to see. The fraction of the population in each case is published with the series.
- **We do not know why anything changed.** We record that it changed and when.
- **What is not observable by policy may be changing** all the time, and it is recorded that we did not look at it.
- **Our classification is an interpretation of ours**, not a fact about the object, and it is marked as such. And the format minimum of `mcp.json` (section 4) is ours: there is no standard to check it against.
- **Services with their own card can be missing from version 11 on** (section 10), but their mortality does not see the death of their domain, and their bound is not compared with that of the lists without saying so. **The directories**, which are also looked at in their own address, **still cannot be recorded as absent**: this version does not define their absence.
- **That a mechanism left a trace does not prove it did its job well**: it proves that it ran and what it looked at (section 11). And what runs after the seal of a day that was not run is not traced.

---

## 8. Versioning of this method

**Every observation records the version of the procedure that produced it, and the text of the procedure is sealed alongside the data.** A version number without the text it described proves nothing.

The test that separates the two classes of change:

> **If measuring yesterday's again could give a different result, it is a discontinuity. If not, it is a compatible version.**

In a discontinuity both procedures are overlapped for as long as possible, so as to leave a calibration bridge; when the object has changed in such a way that the old procedure can no longer be executed, the break is declared and recorded. Skipping the overlap is admissible **with a written excuse**, never in silence.

A discontinuity may be declared **over a series** and not only over a procedure, for the case in which nobody touches the method but the object changes in such a way that the same thing comes to measure something different.

**The discontinuities declared over a source**, with their day. This is the table the birth rule reads —on that day, the new entries of that source are not births— and the one checked by whoever verifies the archive from outside:

| Day | Source | What changed in its reading |
|---|---|---|
| 2026-09-08 | `directorio-pulsemcp` | it is read by the set its sitemap declares, not by walking its pagination |
| 2026-09-08 | `directorio-smithery` | it is read with a seed that fixes the order, not by an order that moves |
| 2026-10-09 | `directorio-glama` | tranche 1 of 3: sub-sitemaps 1–3 of its sitemap enter, and its interface is no longer attempted |
| 2026-10-11 | `directorio-glama` | tranche 2 of 3: sub-sitemaps 4–6 of its sitemap enter |
| 2026-10-13 | `directorio-glama` | tranche 3 of 3: sub-sitemaps 7 and following of its sitemap enter; from that day it is read in full |

**Never backwards**: a new method is not re-executed over old data passing it off as original, nor are already sealed observations relabelled. An error is corrected by **adding** a correction entry with its date, and the original remains intact.

**A systematic error is retracted entry by entry.** When a defect in the instrument produces many false statements at once, each one gets its own correction, with the day and the identifier of the entry it retracts: they are statements about named third parties, and each of them deserves its retraction by name. A collective correction does not exist in the format, and it is not invented under the pressure of an error. **It is sealed on the day it is decided**, not on the day the defect would close by itself. And **the order is mandatory: first the correction is sealed, and only then does the census database move**; the other way round there would be a stretch of time in which the database denies what the seal asserts, and if the sealing failed, that stretch would last forever. What is retracted is **annulled**, which is not the same as **reappeared**: an episode opened by a defect of ours says nothing about the world, and enters no measure of a source's noise. This is how 11,652 false absences of 2026-09-08 were retracted, in the seal of 2026-09-09.

---

*This method is public since 2026-09-15, with all its versions. The archive it produces is not. The reason is that the method is replicable and the historical record is not: publishing it gives nothing away, and in exchange it allows someone to distrust us and still be able to accept the datum.*

---

## 9. Version history of this method

| Version | What changed | Why |
|---|---|---|
| 11.1 | **section 2**: a redirect to another host is a new request —the exclusion list, the `robots.txt` and the courtesy of the destination—, and if anything prevents it the origin is recorded not observable by policy with the reason «destino de la redirección»; the promise to stop observing is by address, and it says so; the series of whoever asked to leave closes with a single entry carrying its identifier, the day and «a petición», and afterwards it is only counted; and whoever verifies with the list in hand checks that no request of the day falls under it. **Section 1**: a directory can ask to leave; the version that honours it names it, and its objects without another source leave by exclusion of their source. **Section 10**: the redirect our exclusions do not let us follow, and the exit by exclusion of its source, which is not a removal. **Section 11**: what `lista-de-exclusiones` and `redirecciones` count | section 2 said that exclusion signals are respected as an absolute rule and that what the list covers receives no request, and every redirect to another host was followed without requesting the destination's `robots.txt`, without checking the list for it and skipping the per-host courtesy: it was a false statement of the method. And exclusion promised more than it can keep —without linking objects by owner we cannot know that a card elsewhere belongs to the same project—, and sealed every day the excluded object's identifier, which earlier days link to its name (C16) |
| 11 | **section 10**: the absence of what is looked at in its own address, for the services with their own card that the frontier's rule admits —missing for three sealed reasons, that day's; what could not be looked at does not count; what answered something else is a day not judged, sealed with its code and counted in the trace; only an admitted declaration reappears; for each A2A missing day the other A2A path of the domain is asked as another door, which registers nothing; and its magnitudes are its own, with no floor and nothing held back—; the frontier's mortality does not see the death of the domain, and for each transport failure its class is sealed, which governs nothing; what its sentence measures; and the exit by change of rule is not that of what stops meeting the rule because the world changed. **Section 3**: what is missing counts as `observed` also when it is looked at in its own address. **Section 4**: what is not a JSON shaped as an object is not judged. **Section 7**: services with their own card can be missing; directories, not yet. **Section 11**: the `ausencias` row, and that the frontier's absence is not a separate mechanism. **And the sentences of the body that said "this version" for 2, 9 or 10 now name their number** | with version 10 what is looked at in its own address could not be missing: the absence rule was written for what a list enumerates and did not reach the frontier, so the malformed ones —which are the ones that die most— would have entered a series whose mortality is not recorded, and a rate by protocol would have come out clean by construction. And what is looked at in its own address cannot be missing the way something is missing from a list: what could not be looked at and what cannot be read have to be stated each by its name, or the first one hides the second. The sentences of the body, because copied into this version they would say that what version 10 brought starts today |
| 10 | **section 1**: the frontier's inclusion rule, as a table that names every path —`oauth-protected-resource` is out, being infrastructure metadata—; also out, the domain that serves the same content on paths of different protocols; an undecided path stops the pass; what the frontier found is judged by it once, with the capacity guard of Glama's tranches; and of Smithery the total each page declares and where each duplicate falls are sealed, without governing anything. **Section 4**: `protocolo_de_agentes` and `cumple_minimo_de_formato`, two classified attributes with the date of the day they are recorded, and the minimum of each format with its source. **Section 10**: exit by change of rule, which is not a removal and enters no rate. **Section 11, new**: the table of the mechanisms the method declares, and the sealed trace of each one on every day; the backup watchman, sealed and published in the witness repository | what an object declares itself to be and how we reach it were being confused, and the frontier had admitted metadata documents that declare themselves to be nothing —sixteen of thirty-four—: taking them out as removals would have put sixteen false deaths into the series. Smithery comes out not walkable one day in six, and the evidence that says why arrived and was thrown away. And three mechanisms were declared over four sealed versions without running, and were discovered one by one: what the method declares was not checking itself, and the only trace of the backup watchman lived where it expires |
| 9 | **section 1**: Glama is no longer attempted through its interface, which excludes us, and is read by the set its sitemap declares, only its servers; it enters **in three tranches of sub-sitemaps**, never on consecutive days, with a guard in the same run that rejects the tranche if the last sealed ordinary day plus its share exceeds half the day's capacity. **Section 8**: each tranche, a declared discontinuity over the source | it was recorded excluded every day, and what excludes us is a surface, not the source: the same site publishes for enumeration a map with one entry per server —96,340 on 2026-10-05—, a whole directory the census did not see. And it is the largest entry the archive has had: what is irreversible is not executed with an estimated size, so it was measured on a copy and enters in parts with its guard |
| 8.4 | **section 1**: a source whose list does not move, if it goes down in transport, is requested again with growing waits, read in full again once the others are done and, if still down, about two hours later within the same day; **for every source, when it was read and in which round is sealed** | on 2026-09-30 an outage of a few minutes of the official registry left 37,281 of 77,390 objects unobserved —48 %—, the third outage in 29 days. It is not a discontinuity: a list read in full reads the same at any hour, and what changes is how many days it is achieved; that is why the time is sealed |
| 8.3 | **section 4**: the address a request ended up at is kept when it is not the one requested, **with no rule using it** | the evidence that an object moved arrived with every request and was thrown away, and what is not kept on the day it arrives is never recovered |
| 8.2 | **corrections**: the day comes to be dated by a timestamp from two independent authorities instead of by the witness's host, which stays on to prove what was published and in what order; with the dated obligation to seal again before their chains expire (2037 and 2040) | the layer that dated shared a provider with the witness repository and with the watchman —three layers that are only worth having if they fail separately cannot depend on the same place— and besides, **only we could check it**: a testimony the reader cannot verify on their own is indistinguishable from an invented one |
| 8.1 | **corrections**: the discontinuity of the institutional layer is declared —until 2026-09-20 on the test bench, with identifiers that are not permanent; since 2026-09-21 on the permanent registry— | the receipts from before and after 2026-09-21 point to different services, and anyone comparing them without this would not know why. A `10.5072` identifier is not citable: saying so is part of not promising more than we have |
| 8 | **section 1**: the package repository leaves the table of sources with a coverage state and is recorded as a **declared source not yet incorporated**, with the day and the reason; and it is said which mechanisms of the inclusion rule run every day and which ran only once. **Scope**: only Layer 0, and **section 6 (claims) is removed**, its design moving to a document that is not sealed. **Section 2**: whoever asks stops being observed, through their `robots.txt` or by email, with a declared list that the pass reads before any source, a published five-day deadline with trace and alert, and the daily count, without names, of what is excluded; it is said what is kept of each object and that nothing is linked by owner, and that nothing enters through any door other than the named sources. **Section 5**: what identity really does —name per source, suspected-link note, no merging—. **Footer**: since when it is public | it was recorded every day as `ilegible`, which was not true: what it permits is known. What is missing is a deterministic walk, and that is not a state of the source but a decision of ours. And the inclusion rule described three mechanisms when the daily pass runs one: the other two only ran on 2026-09-02. And going through everything the method declared, five more sentences described something that did not happen: Layer 1, stopping observing whoever asks, the link to this document, the method being public and the identity ladder. And whoever asked not to be observed had no way to, while the project page offered it. And the only way that did stop the agent, a `robots.txt` naming it, only stopped it with the name written exactly so: with a version or other capitalisation it did not, and whoever tried it never found out |
| 7 | **section 3**: a day that was not observed is sealed without source rows and says so in its header (`no_se_corrio` or `corrio_sin_observar`), and a lost day is sealed by the next pass. **Section 8**: a systematic error is retracted entry by entry, sealed on the day it is decided, and the database moves after the seal. **Section 7**: "walked in full yesterday" means with the same reading, and on the day of a declared discontinuity over a source its new entries are not births; **section 8**: the table of those discontinuities. **Section 10**: what is measured is the mortality of listed entries, not of servers, the quarantine of derived magnitudes comes in, and the other doors of a source are asked and sealed. And **section 9**: the version 4 row, which had been lost, returns, and the table recovers its order. And the preamble says who maintains the method and where its up-to-date contact details are | a lost day blocked every day after it, and the only recovery sealed that day in a way the verifier rejected. On 2026-09-08 11,652 false absences were sealed: the method did not say how an error like that is retracted, and nothing stopped 11,710 absences against a series of zeros from being treated as real. And the sentence for the rate had to be written down before there is a rate |
| 6 | **Section 2**: use signals are declared —that we respect them, and what ours is—. **Section 1**: the source table is corrected; it carried a row from the version history inside it. And a **discontinuity**: PulseMCP is now read as the set its sitemap declares, instead of by walking its pagination | reading by position is unstable by definition: if the list moves while it is being walked, an object that moves back is read twice and one that moves forward is never read. Measured, that produced **247 of the archive's 270 absences**, 242 of them lasting a single day. A set has no position |
| 5 | **new section 10**: the absence and death rule, with its three gates, the separation between absence and death, the back-dating of a death to the first day of absence, and `N` explicitly unfixed. **Section 3**: an object missing from a list walked in full counts as `observed` with a reason, and not in a sixth state | the method spoke of mortality and survival in five sections and the instrument **did not have the rule**: 49,720 objects, 0 with a death date, and the only possible death was that of an identity split in two. Birth was built and its mirror was left undone, and survival needs both. It is written **before there is any death to count**, so that the rule is not written by the data |
| 4 | **section 3**: the state of each source on each day becomes part of the sealed archive, and the verifier requires every day to carry a row for every source that day's method names | that datum is what the birth rule of section 7 depends on, and it lived only in a local database: it was not sealed, no verifier looked at it, and it did not travel in the backup copy. The whole product rested on the one part of the census nobody could check |
| 3 | **section 7**: it is now stated that the first day's population is left-censored and cannot enter any birth cohort, and that birth is asserted from our own coverage rather than from the date the object declares | the previous version said nothing about this, and the instrument was classifying as «born under observation» whoever **declared** it: 474 objects from the first sweep, not one of them seen to appear. Letting a declaration —which cannot be validated— decide a classification of ours is what section 4 forbids |
| 2 | **section 1**: the five enumerable lists are now **named**, with their traversal order, and a rule is added that each is recorded as *enumerated*, *excluded* or *unreadable*, never omitted in silence | version 1 said «public registries and directories» without naming them. The instrument implemented two out of five and the other three were left **absent**, not excluded: they appeared neither in the results nor in the discards. A universe that is not named cannot be audited |
| 1 | — | first version |

**Version 11.1 IS a declared discontinuity, over the coverage of what redirects to another host and only over it.** By the criterion of section 8: measuring an earlier day again with this rule could give not observable by policy where the archive sealed `observed`, if the destination's `robots.txt` forbids it. **It cannot overlap**, and that is the written excuse: also measuring the earlier way would mean continuing to make the request that section 2 forbids. Closing the series of whoever asked to leave changes no measurement —only when its identifier stops appearing—, and a directory's exit will be its own discontinuity, in the version that names it.

**What the entry produces, stated before it happens** (measured on the census of 2026-10-18). In the daily pass, **no origin changes state**: since 2026-09-27, which is since where each request led has been kept, no object looked at in its own address has ended at another one —there are 22 on 2026-10-18—, neither on another host nor on the same one. Where it will change is in the frontier's round, which is not part of this version: on 2026-10-16, in a full round, 201 requested hosts ended at 198 destinations on another host, and 3 of those destinations are reached from two origins; how many of them their `robots.txt` forbids is not measured. The exclusion list is empty: no series closes that day, and no directory has asked to leave.

**Version 11 IS a declared discontinuity, over the series of absences and only over what is looked at in its own address.** By the criterion of section 8: measuring an earlier day again with this rule would give absences where the archive has none. Before the day it enters, a service with its own card could not be missing, so **its mortality cohort starts that day**, and those already there enter it left-censored from 2026-09-02, like the first day's population in the birth cohort. It also changes how its card is sealed when it no longer gives a declaration: a 404 stops sealing the previous day's hash, and a 200 without an object stops being recorded as conformity `no`. It does not go in the table of section 8, for the same reason as version 10: that table is the one of the enumerable sources. **It cannot be overlapped**, for the reason version 5 already gave: the previous procedure produced no measure of this absence to calibrate against; that is the written excuse. What is measured from the four lists does not change, nor do their magnitudes and their quarantine: those of the frontier go apart. **The class of the transport failure is not a discontinuity**: it is sealed alongside the usual and changes no measure.

**What the entry produces, stated before it happens.** It judges the 18 services with their own card that remain after version 10 —7 `mcp`, 8 `a2a` and 3 `openai-plugin`—, and no other: nothing new is probed. On the first day each one is requested in full, without the conditional request, because no earlier day says whether what it gave was a declaration; from the next one, what gave a declaration goes back to zero load. Each one that answers 404 or 410 that day, a 200 without an object or a declaration on a domain in B′ opens an episode with its reason —at most 18—, and each missing day on an A2A path asks the other path of its domain —at most 8 questions, and one more request for each one that is not an object of the census—. No death: the frontier has no `N`. A few dozen more entries that day, at most. **How many of the 18 will be missing is not measured**: it will be said on the day it enters, with what is sealed.

**Version 10 IS a declared discontinuity, over the frontier and only over it.** By the criterion of section 8: measuring an earlier day again with this rule would give a census with sixteen fewer objects. It does not go in the table of section 8, because that table is the one of the enumerable sources —the one the birth rule reads— and the frontier is not one of them: none of its new entries is from today, so there is no birth to protect. What is measured from the four lists does not change. **It cannot be overlapped**: the previous procedure —admitting any path— cannot run at the same time without counting again as objects what this version says are not; that is the written excuse for skipping the overlap. The days sealed up to the day of the exit keep the sixteen as they were. **The Smithery series and the trace of the mechanisms are not discontinuities**: they change no measure, they are sealed alongside them.

**What the entry produces, stated before it happens** (measured on the census of 2026-10-10): of the 34 services with their own card from 2026-09-02, 16 publish at `oauth-protected-resource` and leave by change of rule; none of the other 18 falls into the case of repeated content, because on no domain do two paths of different protocols give the same body; the 18 receive `protocolo_de_agentes` —7 `mcp`, 8 `a2a` and 3 `openai-plugin`— and, as soon as their full card arrives, `cumple_minimo_de_formato`. About 52 entries that day, and the guard decides with that day's figure, not with this one.

**Version 9 IS a declared discontinuity, over Glama and only over it, and on three days.** By the criterion of section 8: measuring an earlier day again with this reading would give a different result —that day Glama was recorded excluded and with zero objects, and with this reading it would bring tens of thousands—. Each tranche is its own row in the table, because each changes what is read from the source that day. What is measured from the other three sources does not change. And on the day a tranche enters, **none of its new entries is a birth**: what appears is what we begin to see.

**What the entry produces, stated before it happens** (measured on a copy of the census of 2026-10-05): none of Glama's entries is the same object as one already censused; tranche 1 brings 30,000 new objects and 243,320 Glama entries —3,320 of them suspected links to another directory, which do not merge—; tranche 2, 30,000 new and 272,223 entries; tranche 3, with that day's ten sub-sitemaps, 36,340 new and 356,257 entries; and each ordinary day afterwards, one entry per Glama object already in. The census would go from about 80,500 objects to about 177,000. The figures that decide each tranche are not these: the guard takes them on the day, with the last sealed ordinary day.

**Version 8 is not a discontinuity**, by the criterion of section 8: the source that leaves the table did not contribute a single object on any day —it was recorded `ilegible`, with zero—, so measuring any earlier day again without it would give the same result. What changes is what is stated about it, not what is measured.

**Retraction, decided on 2026-09-15 and sealed with this version, of what section 1 stated since version 4.** From 2026-09-02 to 2026-09-15 —fourteen sealed days, under versions 4, 5, 6 and 7— section 1 said that an object enters the census, besides through the lists, through the "dependency trail, up to two levels from an already censused object" and through the "frontier: probing of standard paths on known domains, and monitoring filtered by name pattern of the public certificate registries". In a text that describes how we observe, that states those mechanisms work. **It was false.** The dependency trail was attempted once, on 2026-09-02, and yielded nothing. The probing of standard paths was done only once, that same day. And the monitoring of the certificate registries has never been done. Those texts are not edited: they remain sealed as they were, each on its days. They are retracted here, by adding and with a date, as the 11,652 false absences of 2026-09-08 were retracted. What is stated from this version on is what section 1 now says.

**Retraction, decided on 2026-09-15 and sealed with this version, of five further statements of versions 4 to 7.** The frontier was not the only one. Going through everything the method declared, and looking for each mechanism in the code and in the fourteen sealed days —from 2026-09-02 to 2026-09-15—, there were five more sentences describing something that did not happen:

- "It covers Layer 0 (the census) and Layer 1 (claims)", and in section 6, "claims are derived from observing the census and are only written when they fall". **It was false.** No pass has ever derived a claim, or detected one falling: there is no code that does it, and in the fourteen sealed days there is not a single entry of that kind.
- "If anyone asks to stop being observed, we stop observing and the request is recorded with its date". **The procedure did not exist**: neither a register of requests nor anything in the pass that fulfils them. No request arrived, so nobody was observed against their will; but the text described a mechanism that was not there.
- "The agent always identifies itself, with a link to this document". It always identified itself. **The link, no**: until 2026-09-14 it pointed to an address under a reserved domain, which can never resolve, and on 2026-09-15 to the project page, which does not link to this document.
- "This method is public". **It was not**, on any of the fourteen days: its public address was opened on 2026-09-15 at 08:32, Madrid time, after that day's sealing.
- In section 5, "continuity is established by a ladder of evidence", with structural evidence of "same repository, same package identity, same maintainer, same key", and "an object listed in four directories is one identity with four sightings". **It was not so.** No merging rung was connected: no source supplies declared evidence, and the search by package identity exists in the code but is never called. The repository was discarded on purpose —a single one holds 127 servers, and it would have merged them into one— and the maintainer has never been used. What ran was something else: a suspected-link note by name, at registration. And a service in four directories is four objects, as section 10 already acknowledged since version 7.

Those texts are not edited: they remain sealed as they were. They are retracted here, by adding and with a date, like the frontier. What is stated from this version on is what the scope, sections 2 and 5 and the footer now say.

**Section 6 is removed, and the others are not renumbered.** It described Layer 1, which has never been executed. Marking it "not implemented" still put into the document of record what is not done, and that is how these sentences piled up. Its design moves, with that of the identity ladder, to a separate document that is not sealed, does not travel in the copies and is not called method. The other sections keep their number, as section 10 kept its own: the closures and the instrument cite them.

**Version 7 is not a discontinuity**, by the criterion of section 8: measuring yesterday again would not give a different result. The quarantine changes no measurement: it changes what is consumed of what is derived. And the rest of what it adds describes how a day that was **not** measured is sealed —and so far none has been lost—, how an error is retracted —and the retraction of 2026-09-09 was already done that way, under version 6— and what the rate that will one day be published means. No measurement changes.

**Correction of what the institutional layer did, declared here because the method travels inside every package.** On 2026-09-02 and 2026-09-03 the quarterly layer deposited two packages labelled as the quarter `2026-T3`, when the quarter had just begun: they were **mid-term snapshots**, not the quarter's deposit, and they contain the anchor of an open month that was later rewritten. Their content is not false —it was a true picture of those days—; what was wrong was the label. They are left as they are. **The deposit of the closed quarter is pending**: it will be made once, after 30 September, and its own date will say it was made afterwards. No check found this —the receipts said "deposited, T3, correct"—; it was found by asking what was inside the package.

**Discontinuity of the institutional layer, declared with this version.** Until 2026-09-20 that layer's deposits were made against `sandbox.zenodo.org`, the test bench: their identifiers begin with `10.5072` and are **not permanent** —the service removes them whenever it wants, and anyone citing one may find nothing there—. The two that exist are from 2026-09-02 and 2026-09-03, they are recorded in `testigo/recibos-A.jsonl` with their base, and they are the same ones the paragraph above retracts for their label. **Since 2026-09-21 deposits are made against `zenodo.org`**, the permanent registry, and the first real one will be that of the closed quarter, after 30 September. It is declared here, and not in the table in section 8, because that table is about how a source is read —the birth rule uses it— and this changes no measurement: it changes where the evidence is deposited. Anyone comparing the receipts before 21-09 with the later ones will see two different services, and this is why.

**Discontinuity of method in the layer that dates the day, declared with this version.** Until 2026-09-25 the day was dated by the **repository host** where the witness is published: the summary was pushed to it and the time it claimed to have received it was kept. That had two defects that no amount of careful writing fixes —it shared a provider with the repository and with the watchman, and **only we could check it**, so anyone reading the archive had to take our receipt on trust—. **Since 2026-09-26 the day is dated by two independent RFC 3161 timestamping authorities**, in two countries and with two roots that share no failure path; each seal travels whole inside its receipt and **anyone verifies it without talking to us or to the authority**. Each day records **how many of the two sealed it**. The host **stays**, with the role it really supports: proving **what** was published and **in what order**, never when. **Days before 2026-09-26 are not touched**: their layer C is the one they had, it is judged by the rule of that time, and whoever reads the archive will see two different stretches because that is what happened; what exists for them is the anteriority seal of 2026-09-16 over the root of their chain, which proves they existed no later than that day. **And the obligation this brings, with a date and not as an aspiration:** a seal can only be validated while its authority's chain is still alive —2040 for one, 2037 for the other—, so **before the first expires, what is already sealed must be sealed again** with a valid authority, chaining the new seal over the old one. An expired seal does not count as a layer, and the verifier warns before that happens. The mechanism's detail is in the sealing specification, which travels inside every deposit.

**The Smithery discontinuity of 2026-09-08 was not declared at the time**, and it is declared now in the table of section 8. That day Smithery started being read with a seed that fixes the order; measuring the previous day again with that reading gave a different result —from 271 objects to 11,814—, so by the criterion of that same section it was a discontinuity. No birth changed: the previous day Smithery had been read cut, so none of its new entries of 09-08 could be one.

**Correction of an error in the text, declared and not concealed.** When the history row stuck inside the table of section 1 was taken out (version 6), that row —the one for version 4— **was not put back where it belonged**, and the history of version 6 lost the version 4 entry; already in version 5 the table was out of order. It is restored with its original text and the table is put in order. Days sealed under version 6 keep the text with the error, because nothing is resealed.

**Version 6 declares a discontinuity over one source, and only over it.** PulseMCP was read by walking some 535 pages of its website; it is now read as the **set** the site itself declares in its sitemap, in a single request. The test in section 8 is met beyond doubt: re-measuring the same day by the two routes gives different results —on 2026-09-07, 21,957 by the set against 21,912 by the walk—, and that difference **is not noise: it is what the pagination was dropping**.

**It can be overlapped, and it is.** Unlike version 5, here there are two live procedures: the walk still exists and is run as a **periodic control**, so that the difference between the two routes is measured rather than assumed. That control **records and decides nothing**: until there are weeks of that measurement, no number taken from it governs anything.

**What the discontinuity produces on its first day, said before it happens:** **18 absences at once**, the objects the site no longer lists and the pagination kept bringing. Of those, **14 have two independent witnesses** —they stopped coming out of the pagination *and* the site removed them from its set—. They are correct, and they are that source's first deaths with backing.

**And a consequence that is not about measurement but about method:** from 535 requests to 1. That is section 2 —the load placed on the observed— improving by two orders of magnitude, and it is why this change would be made even if it fixed nothing else.

**The instrument stops halting on other people's counts.** Until version 5, the package enumeration stopped when the total the source itself declared said it was done. A third party's count cannot be checked, and if it came up short the reading was left half-done **without declaring a cut**. Now it stops on a fact the source delivers —it stops giving rows— and the declared count is kept **to be contrasted**: if it does not match what was brought, that is a cut with both numbers inside. It is the third time the same class of defect appears —Smithery in version 2, PulseMCP in 6— and the five sources now treat that dependency alike.

**Correction of an error in the text, declared and not disguised.** Since version 4, the table in section 1 carried **a row from the version history pasted inside it**, between Smithery and Glama. It changed no measurement —the verifier reads the five sources by their backticked identifier, and all five came out right— but the document that defines the observed universe spent six days sealed with a paragraph that was not its own. It is corrected here. **Days already sealed keep the text with the error, because nothing is re-sealed**: anyone comparing the versions will see the difference, which is exactly what section 8 asks for.

**Version 5 IS a declared discontinuity**, and it is the first. The test in section 8 says so unambiguously: *if re-measuring yesterday could give a different result, it is a discontinuity*. Here it does come out different — not because it is measured worse, but because **this was not measured before**: until 2026-09-06 an object that disappeared from a list walked in full left no trace anywhere, and from 2026-09-07 it leaves an episode with its date. Re-measuring 3 September with this method would give absences where the archive has none.

**And it cannot be overlapped, because there are not two procedures to overlap: there is one and none.** Section 8 allows skipping the overlap with a written excuse, and this is the excuse: the previous procedure produced no absence measurement to calibrate against. The consequence is declared instead of disguised — **the archive's first five days (2026-09-02 to 2026-09-06) have no absence series and never will**, because sealing backwards is forbidden. Every mortality cohort begins on 2026-09-07, and the earlier population enters it cut off on the left, just as the first day's population does in the birth cohort.

**`N` is left explicitly unfixed in this version, and no death is declared from absence.** The day it is fixed will be another version bump, with its measurement in front of it.

**The archive format goes up too: `strata-sello/4` → `strata-sello/5`.** It adds no new top-level entry type —an absence has an object, so it enters as one more form inside `observacion`, unlike source coverage, which had none—. It goes up because without the number a day with no absence entries would be ambiguous between *"nobody was missing"* and *"the instrument was not recording absences yet"*, which is exactly the ambiguity a format number exists to remove.

**Version 4 is not a discontinuity either**, by the same test in section 8: re-measuring yesterday would not give a different result, because **nothing new is measured**. The state of each source was already computed and already decided who counted as born; all that changes is that it is now sealed, so that it can be checked from outside. It is declared all the same because it changes the archive format —`strata-sello/3` → `strata-sello/4`— and a format change is announced even when it moves no measurement.

**This version bump is not a discontinuity**, and that can be asserted with the test in section 8: measuring yesterday's again would not give a different result, **because there is no yesterday** — there was not a single real observation sealed when the change was made. It is the only window in which widening the universe is free.

After the archive's first day, adding a source **would** be a declared discontinuity: it would change what the population means, and moreover every object from the new source would enter as «already existed when we arrived», impoverishing the born-under-observation cohort for good.
