# Agent Tracer

**Watch your AI agents talk to each other — and watch the gates that refuse.**

One HTML file. No build step, no dependencies, works offline.
Open it, and it moves.

**Live demo → https://fotsopatrick.github.io/agent-tracer/**

---

## Why

Everyone builds agents. Nobody *sees* them.

My agents have been writing to each other for months: 7 218 messages, 411
correspondents, 446 links. All of it lived in rows and columns. I could
**read** that a message had been refused. I could not **see** it.

So I copied Packet Tracer — the tool we all used at school to learn networks.
The devices are the agents. The cables are the pairs that talk. The packets
are their messages.

Green: the gate said yes. Red: it refused — and it writes down **why**.

> A gate that never refused guards nothing.

## Use it

Open `index.html`. That's it. A demo conversation plays on its own, with two
real refusals in it.

To watch **your** agents, drag your log onto the page, or use *Open my log…*.

## Log format

JSON, or one JSON object per line (`.jsonl`):

```json
{
  "agents": ["planner", "coder", "reviewer"],
  "messages": [
    { "from": "planner",  "to": "coder",    "verb": "ASK",
      "subject": "add the retry to the fetch" },
    { "from": "reviewer", "to": "coder",    "verb": "REFUSE",
      "subject": "the patch swallows the error",
      "why": "A caught exception with an empty body hides the failure." }
  ]
}
```

* `agents` is optional — it is rebuilt from the messages if absent.
* `verb` is free text. These seven are coloured: `ASK`, `READBACK`, `RUN`,
  `DONE`, `REFUSE`, `BLOCKED`, `DUNNO`.
* `why` is optional, and it is the most useful field you have. A refusal
  without a reason teaches nobody anything.
* French field names work too (`de`, `vers`, `etat`, `sujet`, `motif`) — my
  own logs are in French.

Nothing leaves your machine. There is no server, no fetch, no telemetry.

## The seven words

A protocol borrowed from air traffic control: the tower gives a heading, and
the pilot **repeats it back** before turning.

| Word | Meaning |
|---|---|
| `ASK` | I ask you to do something |
| `READBACK` | Understood — I repeat your order in my own words |
| `RUN` | I am doing it |
| `DONE` | Finished, here is the proof |
| `REFUSE` | I will not, and here is why |
| `BLOCKED` | I cannot continue, here is what blocks me |
| `DUNNO` | I do not know, and here is what would settle it |

The last three are the ones that matter. An agent that can only say yes is
not an agent, it is a pipe.

## Where it comes from

Agent Tracer is the front door of a bigger thing: a control tower where a team
of agents works behind gates that can say no — checks, reviews, and a human
who has the last word.

* The tower → https://matourdecontrole.fr
* Community edition (Odoo bricks, AGPL) →
  https://github.com/fotsopatrick/tour-community

## Licence

Apache 2.0. Use it, change it, ship it.
