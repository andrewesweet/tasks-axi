# tasks-axi

An agent-ergonomic task/backlog CLI: plain-markdown storage behind a swappable backend seam, so the CLI layer never knows which backend is active.

## Language

**Task**:
The unit of work: an id, a title, a state, links, dependency edges, and an optional hold.
_Avoid_: issue, ticket (GitHub issues are the outward-facing discussion surface, not tasks)

**Backlog**:
The markdown file where tasks live, organized into queued, in-flight, and done sections.
_Avoid_: database, board

**Store**:
The interface every backend implements; the only storage seam the CLI talks to.
_Avoid_: database, repository

**Backend**:
A storage implementation behind the Store seam. Markdown is the only one shipped today; sqlite and remote trackers are deferred.
_Avoid_: driver

**Dependency**:
A typed edge between two tasks — `blocked-by` is the type in use today, alongside the defined `parent` and `discovered-from` — optionally carrying a free-text reason.
_Avoid_: link (links are typed PR, report, or doc references, not edges)

**Hold**:
A structured pause on dispatch: a reason, an optional kind, and an optional until-date gate. Active holds keep queued work out of ready.
_Avoid_: pause, park

**Ready**:
A derived projection, not a stored state: queued tasks other than public follow-ups, with no active blocker and no active hold. Public follow-ups have their own delivery readiness.
_Avoid_: queue (queued is an explicit state, a pre-projection input)

**Blocked**:
A derived projection: a task that is not done and has a blocker that exists and is not done. A blocker that no longer exists counts as resolved.
_Avoid_: held (a hold is set directly on a task; blocked is derived from dependency edges)

**Public follow-up**:
A task with kind `public-followup` carrying versioned durable data for a promised public deliverable; only a posted receipt or an explicit waiver completes it.
_Avoid_: followup note
