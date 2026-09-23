# Observation method · Strata Observatory · version 8

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

**What runs every day.** Of the three mechanisms above, **only the enumerable lists are walked in every pass**. The 34 services the frontier found are looked at every day at their own address, one request each, but **no further domain has been probed**. So since 2026-09-02 **the universe grows only through the lists**, and whatever the frontier would have found afterwards is not there. Until version 7 this was not said, and the executed inclusion rule kept in the archive still described that day's sweep. From version 8, the pass rewrites it every day with what was done that day. Running the frontier again, and how often, would change what is observed: a new version, with its discontinuity.

### The enumerable lists, named

Version 1 said «public registries and directories» without naming any, and that vagueness had a measurable consequence: two sources were implemented, and the other three **were not excluded: they were absent** — not appearing even among the discards, so that nobody could notice they were missing. A universe that is not named cannot be audited.

They are traversed in this order:

| Order | Source | Identifier in the code |
|---|---|---|
| 1 | The protocol's official registry | `registro-oficial-mcp` |
| 2 | The Smithery directory | `directorio-smithery` |
| 3 | The Glama directory | `directorio-glama` |
| 4 | The PulseMCP directory | `directorio-pulsemcp` |

**The identifier column is not decorative.** It is what makes it possible to check by machine that the method and the instrument say the same thing: if this table names a source the census does not attempt, or the census attempts one this table does not name, verification fails. The defect that motivated this version is thus turned into a barrier.

Adding or removing a source from this table is **changing the observed universe**, and therefore a modification of the method with its entry in the history — never a configuration change.

### A declared source not yet incorporated

There is a fifth source the project decided to observe and does not read yet. **It is not in the table above and carries no coverage state**: a source's three states describe an attempt, and with this one nothing is attempted. Nor is it kept quiet: it is recorded here, with the day from which it is recorded this way and why, and it is shown in the history and in the dashboard.

| Source | Since | Why it is not incorporated yet |
|---|---|---|
| `repositorio-npm` | 2026-09-17 | we know what it permits —its terms allow replicating the public registry through its interfaces—, but there is no deterministic walk yet: its search returns at most 5,000 results, in an order that moves, and the keyword query declares 72,182. Reading it that way would be reading by position, the defect that already retired two readings. Until version 7 it was recorded every day as `ilegible`, and it was not: what it permits was known |

Incorporating it will be, like any change to the table above, a new version of the method, and the day it enters will be a declared discontinuity over that source.

### Every source is recorded with its outcome, and there are three of them

On every pass, every source in the table is recorded in one of these states. **None may be omitted in silence.**

| State | What it means |
|---|---|
| **Enumerated** | It was traversed in full, or it is stated where it was cut short |
| **Excluded** | Its exclusion signals forbid the enumerable surface. It is recorded and we stop |
| **Unreadable** | It could not be known what it permits. Not knowing whether it is permitted is not permission |

**«It was not attempted» and «we were not allowed» are different things and cannot produce the same report.** The first speaks about us; the second, about the site. Confusing them would turn an omission of ours into a refusal by someone else, which is a false statement about a third party.

**This census does not aim to be complete. It aims to be deep and consistent.** One cannot enumerate what one does not know exists, and saying otherwise would be the archive's first lie.

---

## 2. How observation is done

**The agent always identifies itself**, in the header of every request, with its name —`strata-observatory`—, the address of the project page, which links in one step to where every version of this document is published, and its contact email. A record built by hiding attests to nothing.

**Public surface only, in the strict sense**: reachable without anyone else's credentials, without circumventing any control and without accepting terms that forbid it.

**A site's exclusion signals are respected as an absolute rule.** Whatever cannot be observed that way is recorded as **not observable by policy** and remains in the census with its reason.

**And declared USE signals are respected too.** Some sites declare in their `robots.txt`, next to the exclusions, how they allow their content to be consumed —search, input to models, training, and with what scope—. **Our use is reference and archival: we keep what an object declares about itself so that we can later say what it said and when. Nothing is trained on it, and third-party content is not redistributed.** Each site's particular signal is not copied here: it is recorded **on every pass**, with its date, because it is a declaration *by the observed* and can change any day — and a third party's sentence frozen inside our doctrine would stop being theirs. Not declaring one is neither permission nor prohibition, and that is recorded too.

**Zero load on the observed.** We ask whether something has changed before downloading it: the hash is kept on every pass and the content **only when the hash changes**.

**If an object blocks access, the block is recorded and we stop. It is not worked around.** The block is a datum in itself.

**Whoever does not want to be observed can stop us, and the way is their own `robots.txt`.** If it names our agent, it is respected like any exclusion in the next pass, without anyone on our side having to read anything. The name is recognised as it would be written by someone who has seen it in their access log: with or without a version, with the whole header pasted, with different capitals or separators.

**For whoever cannot touch their `robots.txt`, the alternative is a written request**, to the project's email or by opening an issue on its page. **It is fulfilled at most five days after it arrives**, and that is the deadline met in the worst month, not in a normal one. Whoever maintains the observatory looks at the email and the issues at least every three days, and every time they look the day is written down, even if there was nothing. Every pending request is written down too, with the day it arrived. **The watchdog raises an alert**, as it does for a missing day: if more than three days pass without looking, if a request passes the deadline, or if an issue stays open longer than it. Fulfilling it means adding the address —a domain, or a path inside a site, such as an account on a hosting site— to a **declared list** that travels with the instrument's code, and answering whoever made it. The list holds the address, the day the request arrived and how it arrived; **never who made it**.

**The list is read at the start of every pass, before any source**, and if it cannot be read, the pass does not start: not knowing whom not to look at is no licence to look at everyone. What it covers **receives no request** —not even the one for its `robots.txt`— **and nothing about it is recorded**: no registrations, no facts, no absences. Every day it is recorded as **not observable by policy**, with the reason and the day the request arrived, without the address. The series is closed with that reason, never with a gap. **And every day the number of addresses excluded on request is sealed, in the day's coverage and without names**: without that number, a day's coverage could be narrower than the previous one's without anyone seeing why. What was sealed before is not deleted, because no day is resealed.

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
**An object missing from a list walked in full counts as `observed`, with its reason**, and not in a sixth state: we looked and it was not there, which is not the same as not having looked at it. What is done with that absence is in section 10.
**And the state of each SOURCE on each day is part of the sealed archive.** This is not the same as the above: that speaks of an object, this of an entire list, and it is recorded as *enumerated*, *excluded* or *unreadable*, never silently omitted (section 1). It goes inside the seal **because it is the evidence on which every claim of birth depends**: an object is recorded as born under observation because the source that carries it was walked in full the day before, and anyone who cannot check that row cannot check the birth. An archive that asserts the second without sealing the first is asserting something it does not support.
**A day that was not observed carries no source rows. None.** If a day's pass does not happen, that day is not measured afterwards —that would record today's state as if it were then—: it is sealed as not observed, with every object *not observed* and its reason, and **without any source row**. The three answers a source can give describe an attempt, and on that day there was none; what happened, happened to the day, not to the sources. And the day's header **says so**: `no_se_corrio` (not run) if the pass did not happen, and then there is no row at all; `corrio_sin_observar` (run without observing) if it was attempted and nothing could be observed, and then every source carries its row and none is *enumerated*. The distinction lives in a stated value, not in a gap. It is not a fourth source state: the closed vocabulary is the source's, and this one is the day's. **A lost day costs one day**: the next pass seals it before its own, because the chain admits no gaps.

---

## 4. What is recorded about each object

**An identifier of our own**, assigned the first time and **never reused**. External names are aliases with their date.

**Its attributes**, which live on the object and are not repeated in every observation: class, provider or responsible organisation, declared type or functional domain, protocol and technical surface, hosting, licence, provenance, the source that discovered it, parent object if it came in by dependency, and whether it **was born under observation** or already existed when we arrived.

Attributes **are sparse series, not fields that get overwritten**: almost none of them ever change, and when one does, an entry is added with its validity date. Without that one could not ask how the objects of a given type behaved in 2027, because one would need to know what type they were *back then*.

**What the object declares and what we classify are stored separately and marked.** The first is a measurement; the second, an interpretation — and our classification carries its own method version.

**The hash of the complete declaration**, every day. The content, only when the hash changes.

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

### Absence and death are two different things

| | when | what it is |
|---|---|---|
| **Absent** | from the **first** day it is missing | a **reversible** fact, recorded and undoable |
| **Reappeared** | if it comes back | **a datum, not an erasure**: it measures how noisy the source is |
| **Death** | after **N** days absent | and **dated on the first day of absence**, not the Nth |

That death is **back-dated to the first day of absence** is what makes everything else work: the archive is an instrument of dates, and the date on which something stopped being there is the day it stopped being there, not the day we became convinced of it.

**Two spans are counted, not one.** A day on which the source could not be walked in full neither confirms the absence nor denies it: it does not close the episode —it is not a reappearance— but neither does it count. That is why each episode carries its **calendar days** and its **confirmed days**, and they are different.

### N is not fixed, and that is stated

**`N` has no value in this version, and no death is declared from absence.** A number chosen by judgement is measured before it is accepted, and `N` cannot be measured without knowing how many absences revert. The first measurement, over the archive's first five days, says why it cannot be 1: **270 episodes, of which 156 have already closed and all 156 reappeared the next day.**

And there is no need to hurry. **Because death is back-dated, nothing is lost by waiting**: if `N` is fixed three weeks from now, the deaths still come out with their correct date. The only thing that cannot be recovered is not having started to record.

### What is measured: listed entries, not servers

What this rule measures is not the mortality **of servers**: it is the mortality **of listed entries**. Section 5 does not join the observations of two directories —no object in the census has sightings in more than one list—, so the same service listed in two directories is two objects. If it disappears from one and remains in the other, it counts as a death in the first, and **it is right that it counts**: its entry there ceased to be. That is why the sentence that gets published has to say what is measured:

> *"Of the N entries listed in the protocol's official registry on 2 September 2026, X % no longer appeared thirty days later."*

Less reach than "servers" would suggest, and the precision that other sentence would not have. **And a consequence for the third gate:** as long as each object is listed by a single list, missing from *all* its lists means missing from its own. The gate stays written as it is, and the day a ladder that joins two directories is connected, it will act on its own.

### Other doors of a source

A source can have **more than one door**, and they need not say the same thing. On 2026-09-10, 33 absences from the Smithery directory came out that were not due to our reading —its listing, walked in full twice, no longer enumerated them— and that still existed: its search found them. Missing from the listing while remaining in the search **is not the same as missing from everywhere**, and it has a state of its own.

That is why each confirmed absence from a source with other doors is asked, that same day, at each of them, and **each answer is sealed as a separate observation**: *present*, *absent* or *could not be asked*, which is a result and not a gap.

| Source | Other door | What it governs |
|---|---|---|
| `directorio-smithery` | the entry page, by exact name | death: it is deterministic |
| `directorio-smithery` | the search, by exact name | nothing: it is sealed as an observation |

**The entry page rules.** The listing still measures absence; the entry page, which answers the same every time it is asked, governs death; the search ranks by relevance —*absent* there only means it did not appear among the first results for its exact name— and speaks of a reranker, not of the object. It is kept because it is a fact, and it decides nothing. A death, when there is one, **will require silence at the entry page**.

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

### Which way this rule fails

**Towards "it has not died".** An undeclared birth impoverishes a cohort of ours; a false death is **a false claim about a third party**: saying that something ceased to exist when it exists. It is the same family as "it was not attempted" versus "we were not allowed", and in that family this method always picks the same side.

Declared consequence, like the overcount in section 7: **any mortality we publish will be a lower bound.** It is stated, not disguised.

### What is sealed, and which coverage state applies

**Every confirmed day of absence goes inside the seal**, tied to the day its episode began, and so does the reappearance that closes it. It goes in for the same reason the state of each source entered in version 4: it is the evidence on which every claim of mortality will depend, and anyone who cannot recount it cannot check the claim. **All** confirmed days are sealed and not just the first, because what must be recountable is how many days the absence was confirmed, not how many days went by.

**An absent object still counts as `observed`**, with its reason written. There is no sixth coverage state: the five in section 3 answer *"did we manage to look at it?"*, and here we did look —the list was walked in full—. *"Was it there?"* is another question, with another shape —an interval, not the state of one day—, and that is why it is recorded separately. Putting them in the same column would repeat the very error section 1 expressly forbids: confusing "we were not allowed to look" with "we looked and it was not there".

---

## 7. What is not measured

Stated in full, because it is what makes the rest citable.

- **Real behaviour is not measured in this version.** Everything above compares what is declared against what was declared before. That a service does what it says **is not checked**: that is Layer 2 and it does not exist.
- **The census is not complete.** It only reaches what the sources in section 1 expose, within the declared filter.
- **An object may change and change back** between two daily observations without our seeing it. The resolution is the cadence.
- **Of the first day's population it is not known when it was born, and it never will be.** That an object was born under observation is asserted by comparing today's list against yesterday's, not by believing the date the object declares —that one cannot be validated—. On the first day there is no yesterday to compare against, so **everything censused that day is recorded as already existing** and stays out of any birth cohort for good. Only what appears from the second day onwards has a whole measurable life. And **"walked in full yesterday" means walked in full yesterday with the same reading**: on the day of a declared discontinuity over a source, none of the new entries that source brings is a birth —its reason is the discontinuity—, because what appears that day may be only what we have started to see. The fraction of the population in each case is published with the series.
- **We do not know why anything changed.** We record that it changed and when.
- **What is not observable by policy may be changing** all the time, and it is recorded that we did not look at it.
- **Our classification is an interpretation of ours**, not a fact about the object, and it is marked as such.

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

**Never backwards**: a new method is not re-executed over old data passing it off as original, nor are already sealed observations relabelled. An error is corrected by **adding** a correction entry with its date, and the original remains intact.

**A systematic error is retracted entry by entry.** When a defect in the instrument produces many false statements at once, each one gets its own correction, with the day and the identifier of the entry it retracts: they are statements about named third parties, and each of them deserves its retraction by name. A collective correction does not exist in the format, and it is not invented under the pressure of an error. **It is sealed on the day it is decided**, not on the day the defect would close by itself. And **the order is mandatory: first the correction is sealed, and only then does the census database move**; the other way round there would be a stretch of time in which the database denies what the seal asserts, and if the sealing failed, that stretch would last forever. What is retracted is **annulled**, which is not the same as **reappeared**: an episode opened by a defect of ours says nothing about the world, and enters no measure of a source's noise. This is how 11,652 false absences of 2026-09-08 were retracted, in the seal of 2026-09-09.

---

*This method is public since 2026-09-15, with all its versions. The archive it produces is not. The reason is that the method is replicable and the historical record is not: publishing it gives nothing away, and in exchange it allows someone to distrust us and still be able to accept the datum.*

---

## 9. Version history of this method

| Version | What changed | Why |
|---|---|---|
| 8 | **section 1**: the package repository leaves the table of sources with a coverage state and is recorded as a **declared source not yet incorporated**, with the day and the reason; and it is said which mechanisms of the inclusion rule run every day and which ran only once. **Scope**: only Layer 0, and **section 6 (claims) is removed**, its design moving to a document that is not sealed. **Section 2**: whoever asks stops being observed, through their `robots.txt` or by email, with a declared list that the pass reads before any source, a published five-day deadline with trace and alert, and the daily count, without names, of what is excluded; it is said what is kept of each object and that nothing is linked by owner, and that nothing enters through any door other than the named sources. **Section 5**: what identity really does —name per source, suspected-link note, no merging—. **Footer**: since when it is public | it was recorded every day as `ilegible`, which was not true: what it permits is known. What is missing is a deterministic walk, and that is not a state of the source but a decision of ours. And the inclusion rule described three mechanisms when the daily pass runs one: the other two only ran on 2026-09-02. And going through everything the method declared, five more sentences described something that did not happen: Layer 1, stopping observing whoever asks, the link to this document, the method being public and the identity ladder. And whoever asked not to be observed had no way to, while the project page offered it. And the only way that did stop the agent, a `robots.txt` naming it, only stopped it with the name written exactly so: with a version or other capitalisation it did not, and whoever tried it never found out |
| 7 | **section 3**: a day that was not observed is sealed without source rows and says so in its header (`no_se_corrio` or `corrio_sin_observar`), and a lost day is sealed by the next pass. **Section 8**: a systematic error is retracted entry by entry, sealed on the day it is decided, and the database moves after the seal. **Section 7**: "walked in full yesterday" means with the same reading, and on the day of a declared discontinuity over a source its new entries are not births; **section 8**: the table of those discontinuities. **Section 10**: what is measured is the mortality of listed entries, not of servers, the quarantine of derived magnitudes comes in, and the other doors of a source are asked and sealed. And **section 9**: the version 4 row, which had been lost, returns, and the table recovers its order. And the preamble says who maintains the method and where its up-to-date contact details are | a lost day blocked every day after it, and the only recovery sealed that day in a way the verifier rejected. On 2026-09-08 11,652 false absences were sealed: the method did not say how an error like that is retracted, and nothing stopped 11,710 absences against a series of zeros from being treated as real. And the sentence for the rate had to be written down before there is a rate |
| 6 | **Section 2**: use signals are declared —that we respect them, and what ours is—. **Section 1**: the source table is corrected; it carried a row from the version history inside it. And a **discontinuity**: PulseMCP is now read as the set its sitemap declares, instead of by walking its pagination | reading by position is unstable by definition: if the list moves while it is being walked, an object that moves back is read twice and one that moves forward is never read. Measured, that produced **247 of the archive's 270 absences**, 242 of them lasting a single day. A set has no position |
| 5 | **new section 10**: the absence and death rule, with its three gates, the separation between absence and death, the back-dating of a death to the first day of absence, and `N` explicitly unfixed. **Section 3**: an object missing from a list walked in full counts as `observed` with a reason, and not in a sixth state | the method spoke of mortality and survival in five sections and the instrument **did not have the rule**: 49,720 objects, 0 with a death date, and the only possible death was that of an identity split in two. Birth was built and its mirror was left undone, and survival needs both. It is written **before there is any death to count**, so that the rule is not written by the data |
| 4 | **section 3**: the state of each source on each day becomes part of the sealed archive, and the verifier requires every day to carry a row for every source that day's method names | that datum is what the birth rule of section 7 depends on, and it lived only in a local database: it was not sealed, no verifier looked at it, and it did not travel in the backup copy. The whole product rested on the one part of the census nobody could check |
| 3 | **section 7**: it is now stated that the first day's population is left-censored and cannot enter any birth cohort, and that birth is asserted from our own coverage rather than from the date the object declares | the previous version said nothing about this, and the instrument was classifying as «born under observation» whoever **declared** it: 474 objects from the first sweep, not one of them seen to appear. Letting a declaration —which cannot be validated— decide a classification of ours is what section 4 forbids |
| 2 | **section 1**: the five enumerable lists are now **named**, with their traversal order, and a rule is added that each is recorded as *enumerated*, *excluded* or *unreadable*, never omitted in silence | version 1 said «public registries and directories» without naming them. The instrument implemented two out of five and the other three were left **absent**, not excluded: they appeared neither in the results nor in the discards. A universe that is not named cannot be audited |
| 1 | — | first version |

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
