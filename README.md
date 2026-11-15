# Netheret help desk, step 10: knowledge base

A teaching example. Over sixteen steps we build a help desk web app for
Netheret, a made-up company that supports the IT of small businesses. This
step adds a knowledge base: articles about known problems that Tier 1 can
search, read and mark as helpful, and that staff can write and edit.

## What this step adds

- `helpdesk/articles.py`, a new blueprint with:
  - `/kb`: search by words and category, most helpful articles first;
  - `/kb/<id>`: read an article (each read adds one to its views);
  - `/kb/<id>/helpful`: the "Did this help?" button;
  - `/kb/new` and `/kb/<id>/edit`: one form for writing and editing
    (staff only).
- On a request's detail page, up to three articles in the same category,
  so Tier 1 can try a known fix before escalating.
- Everybody who is signed in can read articles, customers included.

## Run it

```
python -m venv .venv
source .venv/bin/activate        # on Windows: .venv\Scripts\activate
pip install -r requirements.txt
python seed.py
flask --app helpdesk run --debug
```

Sign in as `tier1@netheret.example` (demo password `password123`), search
for "printer", press "Yes, this helped", then write an article of your own.

## What to look at

- `icontains(q, autoescape=True)` searches without caring about capitals,
  and stops `%` and `_` in the search acting as wildcards.
- The search conditions are joined with `|`, which means OR in SQLAlchemy.
- The helpful vote is remembered in the session, so pressing the button again
  does not count twice. (Signing out clears it: good enough for a help desk,
  not for a public vote.)
- One view function, `edit`, has two routes: with an id it edits, without one
  it writes a new article.

## Learn this step

This is step 10 of 16 of **Task 2. Developing the solution**, a free series of T Level Digital Software Development
lessons that builds the Netheret help desk in agile sprints with Python and Flask. Read the lesson for this step:
[The knowledge base](https://mitsurutech.co.uk/resources/t-level/dsd-t2-10-knowledge-base).

- Previous step: [step 09, an engineer's schedule and job briefs](https://github.com/mitsurutech/netheret-helpdesk-09-my-schedule)
- Next step: [step 11, the customer's view of their requests](https://github.com/mitsurutech/netheret-helpdesk-11-customer-view)
- [Every free T Level Digital lesson](https://mitsurutech.co.uk/resources/t-level)
- [Teach these lessons to your class on MitsuruTech](https://mitsurutech.co.uk/learning), [see the pricing](https://mitsurutech.co.uk/pricing) or
  [start a free year for your college](https://mitsurutech.co.uk/signup)

## About

Written by [Mitsuru Technologies](https://mitsurutech.co.uk) (MitsuruTech) as a teaching example for T Level Digital
Software Development. The Netheret IT Support Solutions brief is from Pearson's sample assessment material; this code
and its notes are our own, and are not published, endorsed or approved by Pearson or the Department for Education.
'T Level' is a registered trade mark of the Department for Education.

