# YavaPy data

The data behind YavaPy, which aggregates the Agent Skills that live beside
published Python command-line tools. The aggregation is virtual: each row
points to a skill in its own repository and never copies it. Two CSV files.

## The two files

`projects.csv` holds the candidates, one row each, sorted by name, so each
update's diff reads line by line. It is the file the search page reads.

`index.csv` lists every PyPI project with a serial above 32,000,000, one row
each, with the same columns. It is sorted by serial, newest first, so it reads
as a feed of PyPI. It is the harvest's working list, and a row fills in stages:

- Not looked at yet: `name` and `serial`.
- Looked at, not a candidate: `released_at` and `checked_at` as well.
- A candidate: every column the project has, the same as its row in
  `projects.csv`.

An empty `checked_at` means the row is waiting for a look. When a project's
serial moves on PyPI, its `checked_at` is emptied, so it gets looked at again.
Until then, its other cells hold the last look.

## What a candidate is

A candidate is a PyPI project with the `Environment :: Console` classifier and
a release in the twelve months before it was checked. Every candidate gets a
row, whether or not its repository holds a `SKILL.md`. So `projects.csv` is a
census of candidates as well as a directory of skills.

A row says a file was found when the project was checked. It does not say the
file is still there, and it is not a review.

YavaPy reads listings, not files. Names, summaries, keywords, topics, and paths
are copied as published on PyPI and GitHub, with no review and no filter.
YavaPy does not open a `SKILL.md`, so a row says nothing about what the file
holds. The words in those fields are their author's.

Treat every field as untrusted text, and read a skill before handing it to an
agent. To report a row, write to <east-van-ai@proton.me>.

## Columns

| Column | Holds |
| --- | --- |
| `name` | the normalized PyPI name |
| `serial` | the project's serial in PyPI's simple index, `0` when removed |
| `version` | the latest version |
| `summary` | PyPI's one-line summary |
| `classifiers` | the project's classifiers, sorted, joined with `; ` |
| `released_at` | the latest release's upload time |
| `checked_at` | when the harvest checked it |
| `repo_url` | the repository on a code host, empty when none |
| `tag` | the release tag the repository was read at, empty when unchecked |
| `skill_count` | how many `SKILL.md` files, empty when unchecked |
| `skill_path` | the shortest path among them, empty when none |
| `topics` | the GitHub repository's topics, sorted, joined with `; ` |
| `license` | the licence's SPDX id, as GitHub reports it |
| `keywords` | PyPI's keywords, as published |

An empty `skill_count` means the repository was not checked, not that it holds
none. Only GitHub repositories are checked, at the tag of the released
version: `v{version}`, or the bare version. A project tagged another way, or
not at all, is left unchecked. So is a repository on GitLab, Codeberg, or
Bitbucket, though it is still recorded.

`topics` and `license` come from GitHub, so a repository elsewhere leaves them
empty. They describe the repository when it was checked, not at the release
tag. An empty cell in these three columns says nothing about the project.

The serial is the one PyPI's simple index lists for the project. The project's
own pages on PyPI can report an older one.

A serial of `0` means the project was removed. The row holds the name and `0`,
and every other cell is empty. The row stays so the project's next release
cannot bring it back.

`marks.json` holds the serial the harvest has climbed to in `index.csv`. It is
bookkeeping, not data.

## Licence

The compilation is dedicated to the public domain under CC0 1.0. Use it as
you like.

The summaries, keywords, and topics are their authors' own words, shared under
the terms of service of PyPI and GitHub. Each row's name leads back to its PyPI
page.

## More documentation

- [Changelog](CHANGELOG.md): project history and releases

## Use of AI

Code and documentation are written in collaboration with remote and local AI; design
decisions, code review, semantic and auditory review, and final judgement stay human.

---

**East Van AI** · AI for the rest of us! · Vancouver, BC, Canada

[github.com/east-van-ai](https://github.com/east-van-ai) · <east-van-ai@proton.me>

Copyright (c) 2026 Go Nakamaru
