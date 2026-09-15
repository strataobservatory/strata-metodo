# Observation method · Strata Observatory · version 7

**What this document is.** The complete description of how we observe, written for someone who **does not trust us**. It is sealed alongside every observation it produces, so that ten years from now one can know not only what we measured but **how we measured it back then**.

**What it is not.** It does not argue that what we measure matters. It recommends nothing and scores nobody. And it does not describe how the archive is dated: that is in the verification procedure, which is published separately and works without access to our data.

**Scope of this version.** It covers **Layer 0 (the census)** and **Layer 1 (claims)**. Behavioural probes —Layer 2— **are not implemented and are not described here**: promising a method that is not executed would be exactly what this project does not do.

**Who maintains it.** Strata Observatory, maintained by Luis Calvo Ruiz. Its up-to-date contact details are at https://github.com/strataobservatory. This text names who and points to where to look, but writes down no email address or identifier: those details change, and this text, once sealed, does not.

---

## 1. The observed universe

Three classes of object, which are the same ecosystem seen at three levels:

1. **Registries and directories.** The sites that list the others.
2. **Services listed in them.** The bulk of the population.
3. **Services and agents with a record of their own on their domain**, found by probing standard paths on already known domains.

**Scope: global.** There is no geographic axis —these objects have no nationality— and no language filter. Claims are archived in a single language, keeping the reference and a minimal quotation of the original in its own language.

### The inclusion rule

An object enters the census if it appears in any of these sources:

- **Enumerable lists** — the five named below, and only those.
- **Dependency trail**, up to **two levels** from an already censused object. At the second level only what belongs to the classes above enters, not every transitive dependency.
- **Frontier**: probing of standard paths on known domains, and monitoring **filtered by name pattern** of the public certificate registries.

**That filter is part of the frontier of the universe**, not an implementation detail: whatever falls outside the pattern is recorded as outside the inclusion rule, **not as non-existent**.

### The five enumerable lists, named

Version 1 said «public registries and directories» without naming any, and that vagueness had a measurable consequence: two sources were implemented, and the other three **were not excluded: they were absent** — not appearing even among the discards, so that nobody could notice they were missing. A universe that is not named cannot be audited.

They are traversed in this order:

| Order | Source | Identifier in the code |
|---|---|---|
| 1 | The protocol's official registry | `registro-oficial-mcp` |
| 2 | The Smithery directory | `directorio-smithery` |
| 3 | The Glama directory | `directorio-glama` |
| 4 | The PulseMCP directory | `directorio-pulsemcp` |
| 5 | Package repositories, for anything that declares itself a service without being listed | `repositorio-npm` |

**The identifier column is not decorative.** It is what makes it possible to check by machine that the method and the instrument say the same thing: if this table names a source the census does not attempt, or the census attempts one this table does not name, verification fails. The defect that motivated this version is thus turned into a barrier.

Adding or removing a source from this table is **changing the observed universe**, and therefore a modification of the method with its entry in the history — never a configuration change.

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

**The agent always identifies itself**, with a link to this document. A record built by hiding attests to nothing.

**Public surface only, in the strict sense**: reachable without anyone else's credentials, without circumventing any control and without accepting terms that forbid it.

**A site's exclusion signals are respected as an absolute rule.** Whatever cannot be observed that way is recorded as **not observable by policy** and remains in the census with its reason.

**And declared USE signals are respected too.** Some sites declare in their `robots.txt`, next to the exclusions, how they allow their content to be consumed —search, input to models, training, and with what scope—. **Our use is reference and archival: we keep what an object declares about itself so that we can later say what it said and when. Nothing is trained on it, and third-party content is not redistributed.** Each site's particular signal is not copied here: it is recorded **on every pass**, with its date, because it is a declaration *by the observed* and can change any day — and a third party's sentence frozen inside our doctrine would stop being theirs. Not declaring one is neither permission nor prohibition, and that is recorded too.

**Zero load on the observed.** We ask whether something has changed before downloading it: the hash is kept on every pass and the content **only when the hash changes**.

**If an object blocks access, the block is recorded and we stop. It is not worked around.** The block is a datum in itself.

**If anyone asks to stop being observed, we stop observing** and the request is recorded with its date. The series is closed with a documented reason, never with a gap.

**Never observed**: nothing behind someone else's credentials, nothing concerning persons, and nothing originating from clients of whoever maintains the observatory.

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

Continuity is established by a **ladder of evidence**:

1. **Declared** — the new object declares the previous one, or the old address redirects to the new one.
2. **Structural** — same repository, same package identity, same maintainer, same key.
3. **Circumstantial** — one disappears and another similar one appears, with a similar declared purpose, within a short window.

**Levels 1 and 2 are the same object.** The alias is recorded with its date and the type of evidence.
**Level 3 is not**: a death and a birth are recorded, with a **note of suspected link** that leaves a record of the possible relation and of the evidence suggesting it.

> **Splitting is recoverable; merging is not.** Joining on weak evidence stops counting deaths and makes survival come out optimistic. Splitting too much somewhat overstates mortality, and the link note allows them to be reunited later. **That pessimistic bias is assumed deliberately, and it is stated.**

Particular cases: in a **fork** the original keeps its identity and the fork is a new object with a declared derivation link · a **name released by a death** is always a new object · an object **listed in four directories** is one identity with four sightings, because lists are sources and not identities.

Every identity decision is recorded with its evidence. Revising one means adding an entry, never rewriting.

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

What this rule measures is not the mortality **of servers**: it is the mortality **of listed entries**. The ladder in section 5 only joins the observations of two directories on declared or structural evidence, and today it joins them in no case —no object in the census has sightings in more than one list—, so the same service listed in two directories is two objects. If it disappears from one and remains in the other, it counts as a death in the first, and **it is right that it counts**: its entry there ceased to be. That is why the sentence that gets published has to say what is measured:

> *"Of the N entries listed in the protocol's official registry on 2 September 2026, X % no longer appeared thirty days later."*

Less reach than "servers" would suggest, and the precision that other sentence would not have. **And a consequence for the third gate:** as long as each object is listed by a single list, missing from *all* its lists means missing from its own. The gate stays written as it is, and the day the ladder joins two directories, it will act on its own.

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

## 6. The claims

**What turns a declaration into a monitored claim:**

> A monitorable claim is a declaration that the object makes **about itself**, machine-readable, **whose breach produces no visible error**.

That is the boundary with the census. «It responds or it does not respond» is census: whoever calls it sees that. «Declares it exposes this tool» is a claim: if it disappears nothing goes off until someone calls it, and by then nobody knows any more when it stopped being there.

Claims **are derived from observing the census and are only written when they fall.**

### The six families

| Family | Statement | Falls when |
|---|---|---|
| **Declared capabilities** | «Declares it exposes this capability, under this exact name» — one per capability | It disappears, or **changes name while keeping everything else**, which is worse because it looks as if it were still there |
| **Declared version** | «Declares this version» · and, separately, «its version is consistent with its content» | The version goes backwards · or **the content changes and the version does not**: an unannounced change |
| **Declared licence** | «Declares this licence» | It changes or disappears |
| **Access and authentication** | «Declares it is served here, with this authentication scheme» | Either of the two changes |
| **Declared provenance** | «Declares it originates here» | The origin ceases to exist or to be reachable |
| **Declared/listed discrepancy** | «What it says about itself and what whoever lists it says about it agree on this field» | They diverge |

For records of their own on a domain there is a seventh: **«declares conformity with this standard»**, checkable against its schema.

**In a discrepancy we do not say who is lying.** The disagreement is recorded with its two sources and its two dates. Behaviour is described, never character.

### What is stored when a claim falls

The statement · the date on which it last held · the date on which the fall was detected · **the date of the change as declared by the object**, if it declares it · the minimal fragment of evidence · and the method version. Never a dump of someone else's content.

The distance between the two dates —the declared one and ours— is our **real resolution**, and it is published as such.

### What is never a claim

Whatever fails visibly · prose descriptions, which are not falsifiable · any judgement of quality · the declared admission policies of directories · and anything concerning persons.

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

*This method is public. The archive it produces is not. The reason is that the method is replicable and the historical record is not: publishing it gives nothing away, and in exchange it allows someone to distrust us and still be able to accept the datum.*

---

## 9. Version history of this method

| Version | What changed | Why |
|---|---|---|
| 7 | **section 3**: a day that was not observed is sealed without source rows and says so in its header (`no_se_corrio` or `corrio_sin_observar`), and a lost day is sealed by the next pass. **Section 8**: a systematic error is retracted entry by entry, sealed on the day it is decided, and the database moves after the seal. **Section 7**: "walked in full yesterday" means with the same reading, and on the day of a declared discontinuity over a source its new entries are not births; **section 8**: the table of those discontinuities. **Section 10**: what is measured is the mortality of listed entries, not of servers, the quarantine of derived magnitudes comes in, and the other doors of a source are asked and sealed. And **section 9**: the version 4 row, which had been lost, returns, and the table recovers its order. And the preamble says who maintains the method and where its up-to-date contact details are | a lost day blocked every day after it, and the only recovery sealed that day in a way the verifier rejected. On 2026-09-08 11,652 false absences were sealed: the method did not say how an error like that is retracted, and nothing stopped 11,710 absences against a series of zeros from being treated as real. And the sentence for the rate had to be written down before there is a rate |
| 6 | **Section 2**: use signals are declared —that we respect them, and what ours is—. **Section 1**: the source table is corrected; it carried a row from the version history inside it. And a **discontinuity**: PulseMCP is now read as the set its sitemap declares, instead of by walking its pagination | reading by position is unstable by definition: if the list moves while it is being walked, an object that moves back is read twice and one that moves forward is never read. Measured, that produced **247 of the archive's 270 absences**, 242 of them lasting a single day. A set has no position |
| 5 | **new section 10**: the absence and death rule, with its three gates, the separation between absence and death, the back-dating of a death to the first day of absence, and `N` explicitly unfixed. **Section 3**: an object missing from a list walked in full counts as `observed` with a reason, and not in a sixth state | the method spoke of mortality and survival in five sections and the instrument **did not have the rule**: 49,720 objects, 0 with a death date, and the only possible death was that of an identity split in two. Birth was built and its mirror was left undone, and survival needs both. It is written **before there is any death to count**, so that the rule is not written by the data |
| 4 | **section 3**: the state of each source on each day becomes part of the sealed archive, and the verifier requires every day to carry a row for every source that day's method names | that datum is what the birth rule of section 7 depends on, and it lived only in a local database: it was not sealed, no verifier looked at it, and it did not travel in the backup copy. The whole product rested on the one part of the census nobody could check |
| 3 | **section 7**: it is now stated that the first day's population is left-censored and cannot enter any birth cohort, and that birth is asserted from our own coverage rather than from the date the object declares | the previous version said nothing about this, and the instrument was classifying as «born under observation» whoever **declared** it: 474 objects from the first sweep, not one of them seen to appear. Letting a declaration —which cannot be validated— decide a classification of ours is what section 4 forbids |
| 2 | **section 1**: the five enumerable lists are now **named**, with their traversal order, and a rule is added that each is recorded as *enumerated*, *excluded* or *unreadable*, never omitted in silence | version 1 said «public registries and directories» without naming them. The instrument implemented two out of five and the other three were left **absent**, not excluded: they appeared neither in the results nor in the discards. A universe that is not named cannot be audited |
| 1 | — | first version |

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
