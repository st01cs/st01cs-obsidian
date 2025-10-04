---
title: "How I use Obsidian"
source: "https://stephango.com/vault"
author:
  - "[[Steph Ango]]"
published:
created: 2025-09-30
description: "My personal Obsidian vault template. A bottom-up approach to note-taking and organizing things I am interested in."
tags:
  - "clippings"
---
I use [Obsidian](https://stephango.com/obsidian) to think, take notes, write essays, and publish this site. This is my bottom-up approach to note-taking and organizing things I am interested in. It embraces chaos and laziness to create emergent structure.

In Obsidian, a “vault” is simply a folder of files. This is important because it adheres to my [file over app](https://stephango.com/file-over-app) philosophy. If you want to create digital artifacts that last, they must be files you can control, in formats that are easy to retrieve and read. Obsidian gives you that freedom.

The following is in no way dogmatic, just one example of how you can use Obsidian. Take the parts you like.

## Vault template

1. [Download my vault](https://github.com/kepano/kepano-obsidian/archive/refs/heads/main.zip) or clone it from [the Github repo](https://github.com/kepano/kepano-obsidian).
2. Unzip the `.zip` file to a folder of your choosing.
3. In Obsidian open the folder as a vault.
- My theme [Minimal](https://stephango.com/minimal) with the [Flexoki](https://stephango.com/flexoki) color scheme.
- [Obsidian Web Clipper](https://stephango.com/obsidian-web-clipper) to save articles and pages from the web, see my [clipper templates](https://github.com/kepano/clipper-templates) for specific sites I clip from.
- [Obsidian Sync](https://obsidian.md/sync) to sync notes between my desktop, phone and tablet.
- [Obsidian Bases](https://help.obsidian.md/bases) to view notes by category.
- [Leaflet](https://github.com/javalent/obsidian-leaflet) plugin for maps used in some of my templates.

## Personal rules

Rules I follow in my personal vault:

- Avoid splitting content into multiple vaults.
- Avoid folders for organization.
- Avoid non-standard Markdown.
- Always pluralize categories and tags.
- Use internal links profusely.
- Use `YYYY-MM-DD` dates everywhere.
- Use the 7-point scale for ratings.
- Keep [a single to-do list](https://stephango.com/todos) per week.

Having a [consistent style](https://stephango.com/style) collapses hundreds of future decisions into one, and gives me focus. For example, I always pluralize tags so I never have to wonder what to name new tags. Choose rules that feel comfortable to you and write them down. Make your own style guide. You can always change your rules later.

## Folders and organization

I use very few folders. I avoid folders because many of my entries belong to more than one area of thought. My system is oriented towards speed and laziness. I don’t want the overhead of having to consider where something should go.

I do not use nested sub-folders. I do not use the file explorer much for navigation. I mostly navigate using the quick switcher, backlinks, or links within a note.

My notes are primarily organized using the `categories` property. Categories display an overview of related notes, using the [bases](https://help.obsidian.md/bases) feature in Obsidian.

**Most of my notes are in the root of the vault**, not a folder. This where I write about my personal world: journal entries, essays, [evergreen](https://stephango.com/evergreen-notes) notes, and other personal notes. If a note is in the root, I know it’s something I wrote, or relates directly to me.

Two reference folders I use:

- **References** where I write about things that exist outside my world. Books, movies, places, people, podcasts, etc. Always named using the title e.g. `Book title.md` or `Movie title.md`.
- **Clippings** where I save things other people wrote, mostly essays and articles.

Three admin folders exist so that their contents don’t show up in the file navigation:

- **Attachments** for images, audio, videos, PDFs, etc.
- **Daily** for my daily notes, all named `YYYY-MM-DD.md`. I do not write anything in daily notes, they exist solely to be linked to from other entries.
- **Templates** for templates.

Two folders are present in the downloadable version of my vault for the sake of clarity. In my personal vault, these notes would be in the root, not a folder.

- **Categories** contains top-level overviews of notes per category (e.g. Books, Movies, Podcasts, etc).
- **Notes** contains example notes.

## Links

I use internal links profusely throughout my notes. I try to always link the first mention of something. My journal entries are often a stream of consciousness cataloging recent events, finding connections between things. Often the link is *unresolved*, meaning that the note for that link isn’t created yet. Unresolved links are important because they are breadcrumbs for future connections between things.

A journal entry in the **root** of my vault might look something like this:

```
I went to see the movie [[Perfect Days]] with [[Aisha]] at [[Vidiots]] and had Filipino food at [[Little Ongpin]]. I loved this quote from Perfect Days: [[Next time is next time, now is now]]. It reminds me of the essay ...
```

The movie, movie theater, and restaurant each link to entries in my **References** folder. In these reference notes I capture properties, my rating, and thoughts about that thing. I use [Web Clipper](https://stephango.com/obsidian-web-clipper) to help populate properties from databases like IMDB. The quote was meaningful to me, so it became an [evergreen note](https://stephango.com/evergreen-notes) in my root folder. The essay I mention is in my **Clippings** folder, because I didn’t write it myself.

This heavy linking style becomes more useful as time goes on, because I can trace how ideas emerged, and the branching paths these ideas created.

## Fractal journaling and random revisit

Fractal journaling and randomization are how I tame the wilderness that a knowledge base can grow into.

Throughout the day I use Obsidian’s *unique note* hotkey to write individual thoughts as they come up. This shortcut automatically creates a note with the prefix `YYYY-MM-DD HHmm` to which I may add a title that describes the idea.

Every few days I review these journal fragments and compile the salient thoughts. I then review those reviews monthly, and review the monthly reviews yearly (using [this template](https://stephango.com/40-questions)). The result is a fractal web of my life that I can zoom in and out of at varying degrees of detail. I can trace back where individual thoughts came from, and how they bubbled up into bigger themes.

Every few months I set aside time for a “random revisit”. I use the *random note* hotkey to quickly travel randomly through my vault. I often use the local graph at shallow depth to see related notes. This helps me revisit old ideas, create missing links, and find inspiration in past thoughts. It’s also an opportunity to do maintenance, like fix formatting based on new rules in my personal style guide.

People have asked me if this could be automated with language models but I do not care to do so. I enjoy this process. Doing this maintenance helps me understand my own patterns. [Don’t delegate understanding](https://stephango.com/understand).

## Properties and templates

Almost every note I create starts from a [template](https://github.com/kepano/kepano-obsidian/tree/main/Templates). I use templates heavily because they allow me to lazily add information that will help me find the note later. I have a template for every category with [properties](https://help.obsidian.md/properties) at the top, to capture data such as:

- **Dates** — created, start, end, published
- **People** — author, director, artist, cast, host, guests
- **Themes** — grouping by genre, type, topic, related notes
- **Locations** — neighborhood, city, coordinates
- **Ratings** — more on this below

A few rules I follow for properties:

- Property names and values should aim to be reusable across categories. This allows me to find things across categories, e.g. `genre` is shared across all media types, which means I can see an archive of *Sci-fi* books, movies and shows in one place.
- Templates should aim to be composable, e.g. *Person* and *Author* are two different templates that can be added to the same note.
- Short property names are faster to type, e.g. `start` instead of `start‑date`.
- Default to `list` type properties instead of `text` if there is any chance it might contain more than one link or value in the future.

The [.obsidian/types.json](https://github.com/kepano/kepano-obsidian/blob/main/.obsidian/types.json) file lists which properties are assigned to which types (i.e. `date`, `number`, `text`, etc).

## Rating system

Anything with a `rating` uses an integer from 1 to 7:

- 7 — **Perfect**, must try, life-changing, go out of your way to seek this out
- 6 — **Excellent**, worth repeating
- 5 — **Good**, don’t go out of your way, but enjoyable
- 4 — **Passable**, works in a pinch
- 3 — **Bad**, don’t do this if you can
- 2 — **Atrocious**, actively avoid, repulsive
- 1 — **Evil**, life-changing in a bad way

Why this scale? I like rating out of 7 better than 4 or 5 because I need more granularity at the top, for the good experiences, and 10 is too granular.

## Publishing to the web

This site is written, edited, and published directly from Obsidian. To do this, I break one of my rules listed above — I have a separate vault for my site. I use a *static site generator* called [Jekyll](https://jekyllrb.com/) to automatically compile my notes into a website and convert them from Markdown to HTML.

My publishing flow is easy to use, but a bit technical to set up. This is because I like to have full control over every aspect of my site’s layout. If you don’t need full control you might consider [Obsidian Publish](https://obsidian.md/publish) which is more user-friendly, and what I use for my [Minimal documentation site](https://minimal.guide/publish/download).

For this site, I push notes from Obsidian to a GitHub repo using the [Obsidian Git](https://obsidian.md/plugins?id=obsidian-git) plugin. The notes are then automatically compiled using [Jekyll](https://jekyllrb.com/) with my web host [Netlify](https://www.netlify.com/). I also use my [Permalink Opener](https://stephango.com/permalink-opener) plugin to quickly open notes in the browser so I can compare the draft and live versions.

The color palette is [Flexoki](https://stephango.com/flexoki), which I created for this site. My Jekyll template is not public, but you can get similar results from [this template](https://github.com/maximevaillancourt/digital-garden-jekyll-template) by Maxime Vaillancourt. There are also many alternatives to Jekyll you can use to compile your site such as [Quartz](https://quartz.jzhao.xyz/), [Astro](https://astro.build/), [Eleventy](https://www.11ty.dev/), and [Hugo](https://gohugo.io/).

- [File over app](https://stephango.com/file-over-app)
- [Concise explanations accelerate progress](https://stephango.com/concise)
- [Evergreen notes turn ideas into objects that you can manipulate](https://stephango.com/evergreen-notes)
- [40 questions to ask yourself every year](https://stephango.com/40-questions)
- [40 questions to ask yourself every decade](https://stephango.com/40-questions-decade)
- [How I do my to-dos](https://stephango.com/todos)