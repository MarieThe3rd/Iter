# Issue tracker: Trello (custom)

Work items for this repo live in a Trello board, not GitHub Issues. GitHub is used only for the code repo and pull requests — [github.com/MarieThe3rd/Iter](https://github.com/MarieThe3rd/Iter).

## Board

[Iter board](https://trello.com/b/69p9AgaH/iter) (short id `69p9AgaH`).

## Hierarchy

Three levels, each a Trello card, tagged with a label:

- **Epic** (label id `6a946a7ed41650de9b3d0b99`) — the largest unit. Contains enough context to be broken into Features.
- **Feature** (label id `6a946a7ed41650de9b3d0b9c`) — a child of one Epic. Contains enough context to be broken into Stories.
- **Story** (label id `6a946a7ed41650de9b3d0b98`) — a child of one Feature. The unit of work handed to an agent one at a time. Contains a prompt for the work plus a definition of done.

Two more labels exist for work outside that hierarchy:

- **Bug** (`6a946a7ed41650de9b3d0b9a`) — incoming bug reports, relevant if/when the `triage` flow is used (see `triage-labels.md`).
- **Task** (`6a94835d0a14d649231fe5d1`) — standalone work items that aren't part of an Epic/Feature/Story breakdown (e.g. repo/tooling setup).

Use these five existing labels as-is — don't create new ones for the same purpose.

Each card references its parent card with a link in the card description (e.g. `Parent: https://trello.com/c/<shortLink>`).

## Workflow (lists)

Card progress is tracked by which list it sits in, not a status field:

| List      | Meaning                    | id                         |
| --------- | --------------------------- | -------------------------- |
| Backlog   | Not yet started              | `6a946a8a8363ee479348d35a` |
| To Do     | Ready to be picked up         | `6a946a9b9569428edc5fe22e` |
| Doing     | In progress                   | `6a946a9ff1522b511b1101ef` |
| Review    | Awaiting PR review/testing    | `6a946aa31fe5a29e8a1c9cb1` |

## Access

Via the Trello REST API (`https://api.trello.com/1/`) using a personal API key + token, stored as environment variables (`TRELLO_API_KEY`, `TRELLO_API_TOKEN`) in a local, gitignored `.env` — never committed, never pasted into chat. Provisioned via `scripts/setup-trello-access.sh`.

## Conventions

Board short id: `69p9AgaH`.

- **Create a card**: `POST /1/cards?idList=<listId>&name=<title>&desc=<body>&idLabels=<levelLabelId>&key=$TRELLO_API_KEY&token=$TRELLO_API_TOKEN`
- **Read a card**: `GET /1/cards/<cardId>?key=...&token=...`
- **List cards on the board**: `GET /1/boards/69p9AgaH/cards?key=...&token=...`
- **Comment on a card**: `POST /1/cards/<cardId>/actions/comments?text=...&key=...&token=...`
- **Move a card to a new list** (e.g. Doing → Review): `PUT /1/cards/<cardId>?idList=<listId>&key=...&token=...`
- **Archive/close a card**: `PUT /1/cards/<cardId>?closed=true&key=...&token=...`

## When a skill says "publish to the issue tracker"

Create a Trello card at the appropriate level (Epic, Feature, or Story) on the Iter board, tagged with its level label and linking to its parent card if it has one.

## When a skill says "fetch the relevant ticket"

Fetch the Trello card by ID via the API and read its description and comments.

## Workflow notes

- Elaborate just-in-time, not waterfall: an Epic needs only enough detail to be broken into Features; a Feature needs only enough detail to be broken into Stories. Don't try to fully specify every Feature or Story up front when creating an Epic — later levels get filled in when work actually approaches them, since the answers aren't all known yet.
- Stories are the unit an agent picks up — one at a time, not a full backlog hand-off. Each Story card's description is the prompt plus its definition of done.
- TDD is required for behavior/business logic; not required for infrastructure code.
- Work proceeds with checkpoints: the user reviews and approves each PR (opened against [github.com/MarieThe3rd/Iter](https://github.com/MarieThe3rd/Iter)) and tests the change before the next Story is picked up. Don't chain multiple Stories into one PR, and don't start the next Story without that approval.
