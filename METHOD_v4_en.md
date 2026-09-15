# Observation method · Strata Observatory · version 4

**What this document is.** The complete description of how we observe, written for someone who **does not trust us**. It is sealed alongside every observation it produces, so that ten years from now one can know not only what we measured but **how we measured it back then**.

**What it is not.** It does not argue that what we measure matters. It recommends nothing and scores nobody. And it does not describe how the archive is dated: that is in the verification procedure, which is published separately and works without access to our data.

**Scope of this version.** It covers **Layer 0 (the census)** and **Layer 1 (claims)**. Behavioural probes —Layer 2— **are not implemented and are not described here**: promising a method that is not executed would be exactly what this project does not do.

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
| 4 | **section 3**: the state of each source on each day becomes part of the sealed archive, and the verifier requires every day to carry a row for every source that day's method names | that datum is what the birth rule of section 7 depends on, and it lived only in a local database: it was not sealed, no verifier looked at it, and it did not travel in the backup copy. The whole product rested on the one part of the census nobody could check |
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
**And the state of each SOURCE on each day is part of the sealed archive.** This is not the same as the above: that speaks of an object, this of an entire list, and it is recorded as *enumerated*, *excluded* or *unreadable*, never silently omitted (section 1). It goes inside the seal **because it is the evidence on which every claim of birth depends**: an object is recorded as born under observation because the source that carries it was walked in full the day before, and anyone who cannot check that row cannot check the birth. An archive that asserts the second without sealing the first is asserting something it does not support.

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
- **Of the first day's population it is not known when it was born, and it never will be.** That an object was born under observation is asserted by comparing today's list against yesterday's, not by believing the date the object declares —that one cannot be validated—. On the first day there is no yesterday to compare against, so **everything censused that day is recorded as already existing** and stays out of any birth cohort for good. Only what appears from the second day onwards has a whole measurable life. The fraction of the population in each case is published with the series.
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

**Never backwards**: a new method is not re-executed over old data passing it off as original, nor are already sealed observations relabelled. An error is corrected by **adding** a correction entry with its date, and the original remains intact.

---

*This method is public. The archive it produces is not. The reason is that the method is replicable and the historical record is not: publishing it gives nothing away, and in exchange it allows someone to distrust us and still be able to accept the datum.*

---

## 9. Version history of this method

| Version | What changed | Why |
|---|---|---|
| 1 | — | first version |
| 3 | **section 7**: it is now stated that the first day's population is left-censored and cannot enter any birth cohort, and that birth is asserted from our own coverage rather than from the date the object declares | the previous version said nothing about this, and the instrument was classifying as «born under observation» whoever **declared** it: 474 objects from the first sweep, not one of them seen to appear. Letting a declaration —which cannot be validated— decide a classification of ours is what section 4 forbids |
| 2 | **section 1**: the five enumerable lists are now **named**, with their traversal order, and a rule is added that each is recorded as *enumerated*, *excluded* or *unreadable*, never omitted in silence | version 1 said «public registries and directories» without naming them. The instrument implemented two out of five and the other three were left **absent**, not excluded: they appeared neither in the results nor in the discards. A universe that is not named cannot be audited |

**Version 4 is not a discontinuity either**, by the same test in section 8: re-measuring yesterday would not give a different result, because **nothing new is measured**. The state of each source was already computed and already decided who counted as born; all that changes is that it is now sealed, so that it can be checked from outside. It is declared all the same because it changes the archive format —`strata-sello/3` → `strata-sello/4`— and a format change is announced even when it moves no measurement.

**This version bump is not a discontinuity**, and that can be asserted with the test in section 8: measuring yesterday's again would not give a different result, **because there is no yesterday** — there was not a single real observation sealed when the change was made. It is the only window in which widening the universe is free.

After the archive's first day, adding a source **would** be a declared discontinuity: it would change what the population means, and moreover every object from the new source would enter as «already existed when we arrived», impoverishing the born-under-observation cohort for good.
