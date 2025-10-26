# Warning: this mostly vibe coded, and seems to work :D

# Description
`estimate` is a small command-line tool that back-calculates when you must begin a sequence of steps in order to meet a target time (e.g., arrival). The script reads a simple text plan with durations such as `30m`, `1h20m`, or `15m`, supports optional steps, variant generation, inline comments, labels, and machine-readable JSON output.

Goal of this is to help preplan on when to wake up or leave home when you have a list of things to do and a specific time to be somewhere.

There is a way to list out optional things and generate plan variations.

Just type `estimate` to get help

# Key Features
- Back-calculate start time from a final target time
- Optional steps (? step 15m) with variant generation
- Human and JSON output modes
- Inline comments allowed (# or ;)
- Flexible input: plan file, stdin, or shorthand name
- Duration formats: 30m, 1h10m, or numbers-only minutes
- Shorthands:
  - -v variants
  - -s summary-only
  - -a ASCII
  - -j JSON
  - -d date selector

# Usage samples
Example plan: `today.plan`
```
prep 30m
? pick up vladis 20m
? grab food 20m
drive 1h10m
park 20m
meeting 11 30
```

(assuming you got `today.plan` or `today.txt` at workingdir)

## Simple plan
```
estimate today
```

Sample output:
```
Step                       Dur    All    Core
----                       ---    ---    ----
prep                       30m    08:50  09:30
pick up vladis *           20m    09:20  —
grab food *                20m    09:40  —
drive                      1h10m  10:00  10:00
park                       20m    11:10  11:10

Begin at (All) → meeting                 08:50
Begin at (Core) → meeting                09:30
meeting                                  11:30
```

## Only summary of all possible options
```
estimate today -v -s
```

Variant summary output:
```
Variant starts:
  base                        09:30
  pick up vladis              09:10
  grab food                   09:10
  pick up vladis + grab food  08:50
```

## Detailed variants list
```
estimate today -v
```

Variants output:
```
Variant: base
Begin: 09:30
09:30 (30m) prep
10:00 (1h10m) drive
11:10 (20m) park
11:30 meeting
------------------------------------------------
Variant: pick up vladis
Begin: 09:10
09:10 (30m) prep
09:40 (20m) pick up vladis
10:00 (1h10m) drive
11:10 (20m) park
11:30 meeting
------------------------------------------------
Variant: grab food
Begin: 09:10
09:10 (30m) prep
09:40 (20m) grab food
10:00 (1h10m) drive
11:10 (20m) park
11:30 meeting
------------------------------------------------
Variant: pick up vladis + grab food
Begin: 08:50
08:50 (30m) prep
09:20 (20m) pick up vladis
09:40 (20m) grab food
10:00 (1h10m) drive
11:10 (20m) park
11:30 meeting
------------------------------------------------
Variant starts:
  base                        09:30
  pick up vladis              09:10
  grab food                   09:10
  pick up vladis + grab food  08:50
```

# Installation
```
git clone https://github.com/TomasLiutvinas/estimate-cli.git
cd estimate-cli
chmod +x estimate
ln -s "$(pwd)/estimate" ~/.local/bin/estimate
```
