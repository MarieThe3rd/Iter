# Iter

A personal, single-user tool for organizing and prioritizing what to learn, tracking proficiency against tree-shaped roadmaps, and tying that learning back to the reasons it matters (a promotion, a project, a technology, a methodology). Named "Iter," short for Itinerary — also a nod to learning iteratively.

## Language

**Roadmap**:
A tree of Nodes representing a curriculum toward a specific area (e.g. "ASP.NET Core," "Azure Developer"), modeled after roadmap.sh's roadmap trees. Arbitrary depth, no level limit. Built manually, optionally using a roadmap.sh page as a visual reference to copy from — there is no automated import, since roadmap.sh does not publish its tree structure publicly.
_Avoid_: Learning path, curriculum, track

**Node**:
A single item within a Roadmap's tree — a topic or skill (e.g. "Minimal APIs," "Kubernetes"). A Node with children is a **branch node**, purely organizational, carrying no tracked state of its own. A Node with no children is a **leaf node**, the actual trackable unit — it carries a Level and optional journal entries. A Node can exist without belonging to any Roadmap (standalone) and without belonging to any Goal.
_Avoid_: Topic, skill, item (when the tree-position meaning is intended)

**Level**:
A leaf Node's current proficiency, set manually by the user: New, Beginner, Intermediate, Strong, or Master. Reflects actual skill today, independent of any Goal.
_Avoid_: Status, progress, completion

**Goal**:
A first-class entity representing *why* a cluster of learning matters — e.g. "Promotion to Principal Developer," "Project Phoenix," "Learn Azure Networking." Has a category (drawn from a user-extensible list, seeded with Promotion, Project, Technology Interest, Methodology, Personal Interest), optional free-text detail, an optional target date, and a lifecycle status (Active, Achieved, or Abandoned) set manually by the user — never auto-computed. A Goal links to one or more Roadmaps and/or one or more individual Nodes (which may be standalone or drawn from different Roadmaps).
_Avoid_: Why, motivation, reason

**Target Level**:
The Level a Goal requires of a specific Node in order to consider that Node satisfied for that Goal. Set per Goal-Node pairing — the same Node can carry a different Target Level under a different Goal. Linking a whole Roadmap to a Goal sets one Target Level as the default for all its leaf Nodes, individually overridable.
_Avoid_: Desired level, required level

**Attainment**:
A Goal's computed fraction of linked Nodes whose current Level meets or exceeds their Target Level (e.g. "4/6 targets met"). Informational only — it does not drive the Goal's lifecycle status.
_Avoid_: Goal progress, completion percentage

**Priority**:
A manual value the user sets on a Node, informed by (but not computed from) its attached Goal(s). A Node with no Goal cannot carry a Priority and does not appear in the active priority view.
_Avoid_: Rank, weight, importance
