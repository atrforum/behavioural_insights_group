ATRF Behavioural Insights Group (BIG)
=====================================

> **This is a preview site. Content has not been reviewed or endorsed.**


Source for the website of the Behavioural Insights Group, a standing group of the
[Australasian Transport Research Forum (ATRF)](https://australasiantransportresearchforum.org.au/).



## Editing

There are two ways to update the site:

- **The easy way — email the site coordinator.** If you'd just like your headshot added, an event listed, or any other change made on your behalf, email the details to the site coordinator (TODO: contact email) and they'll take care of it.
- **DIY on GitHub.** All the edits below can be made directly in your web browser through GitHub's file editor. You'll need a (free) GitHub account and to be added to this repository as a collaborator. No coding required.

### Adding your headshot

1. Save your photo as a JPG. A square crop, around 400×400 pixels, looks best. Name it after yourself in lower-case with hyphens — e.g. `jane-smith.jpg`.
2. In GitHub, open the [img/team/](img/team/) folder and use **Add file → Upload files** to upload your photo there.
3. Open [_data/people.yml](_data/people.yml) and find your entry. It will currently look like this:

   ```yaml
   - name: Jane Smith
     pic: placeholder
     position: member
   ```

   Edit the `pic:` line so it matches the filename you uploaded, **without** the `.jpg` extension:

   ```yaml
   - name: Jane Smith
     pic: jane-smith
     position: member
   ```

4. Commit the change (GitHub will prompt you with a "Commit changes" button). The site rebuilds automatically and your headshot should appear on the Team page within a couple of minutes.

If you don't yet have an entry in [_data/people.yml](_data/people.yml), add one in the same shape, keeping the list in alphabetical order by first name.

### Adding an event

Events live in [_data/events.yml](_data/events.yml), split into two lists: `upcoming:` and `past:`. Open the file and copy one of the existing entries as a template.

**Upcoming event** — needs a name, location, date, and a link (use `"#"` if there isn't one yet):

```yaml
upcoming:
  - name: BIG Monthly Meeting (July) — Guest speaker TBC
    location: Online (Teams)
    date: July 2026 (TBC)
    url: "#"
```

**Past event** — needs a short description (speaker, affiliation, date) and optionally a link to slides:

```yaml
past:
  - name: Title of the talk
    url: "#"
    description: "Speaker Name (Affiliation) presented on <topic>. Hosted by the ATRF Behavioural Insights Group on <date>."
    slides: /assets/presentations/speaker-name-talk-title.pdf   # optional — leave the line out if no slides
```

If you're attaching slides, upload the PDF to [assets/presentations/](assets/presentations/) first (same **Add file → Upload files** flow as for headshots), then reference the filename in the `slides:` line.

When an upcoming event has happened, simply move the entry from the `upcoming:` list down to the `past:` list and add a `description:` line.

### Editing tutorial (video walkthrough)

The video below is from the PT Research Committee website. The layout of our site is slightly different, but the GitHub workflow shown — editing files in the browser, committing changes — is the same.

[![Editing tutorial](https://github.com/atrforum/pt_research_committee/assets/7377666/884c8b30-6f64-4a29-8c4e-7dfb7dd691b4)](https://youtu.be/-8pIQiQ1Ly0)


## Developer notes

The site is a Jekyll static site. Most content lives in [_config.yml](_config.yml)
(team, research needs, resources, events) with copy in [_includes/](_includes/).

### Local preview

```
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000/.

