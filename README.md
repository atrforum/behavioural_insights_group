ATRF Committee for Behavioural Insights (CBI)
=============================================

Source for the website of the Committee for Behavioural Insights, a standing group of the
[Australasian Transport Research Forum (ATRF)](https://australasiantransportresearchforum.org.au/).


## Editing

There are two ways to update the site:

- **The easy way — email the site coordinator.** If you'd just like your headshot added, an event listed, or any other change made on your behalf, email the details to the [site coordinator](mailto:jan@outerloop.io) and they'll take care of it.
- **DIY on GitHub.** You'll need a (free) GitHub account. With this, there are two options: Option 1 (if you know GitHub workflows) fork the repository, make edits in your fork and open a pull request against the main repository. Option 2 is to be added to this repository as a collaborator and edit the files in this repository directly in your web browser through GitHub's file editor. For the second option, the video below from the PT Research Committee website lays out the steps in detail. The layout of our site is slightly different (see details below), but the GitHub workflow shown — editing files in the browser, committing changes — is the same.

[![Editing tutorial](https://github.com/atrforum/pt_research_committee/assets/7377666/884c8b30-6f64-4a29-8c4e-7dfb7dd691b4)](https://youtu.be/-8pIQiQ1Ly0)

### Adding your headshot

1. Save your photo as a square JPG or PNG, around 400×400 pixels. Name it after yourself in lower-case with hyphens — e.g. `jane-smith.jpg` or `jane-smith.png`.
2. In GitHub, open the [img/team/](img/team/) folder and use **Add file → Upload files** to upload your photo there.
3. Open [_data/people.yml](_data/people.yml) and find your entry. It will currently look like this:

   ```yaml
   - name: Jane Smith
     pic: placeholder
     position: member
   ```

   Edit the `pic:` line so it matches the filename you uploaded, **without** the extension:

   ```yaml
   - name: Jane Smith
     pic: jane-smith
     position: member
   ```

   If you uploaded a PNG, also add `image_ext: png`. JPG is the default, so you only need `image_ext:` for non-JPG headshots:

   ```yaml
   - name: Jane Smith
     pic: jane-smith
     image_ext: png
     position: member
   ```

You can also optionally add contact links on the Team page with `email:` and `url:` fields, for example `url: https://www.linkedin.com/in/jane-smith/`.

Leadership entries in [_data/leadership.yml](_data/leadership.yml) support a separate `committee_role:` field for the person's role within the Behavioural Insights Group, while `position:` can be used for their job title and organisation.

4. Commit the change (GitHub will prompt you with a "Commit changes" button). The site rebuilds automatically and your headshot should appear on the Team page within a couple of minutes.

If you don't yet have an entry in [_data/people.yml](_data/people.yml), add one in the same shape, keeping the list in alphabetical order by first name.

### Adding a research-needs survey link

To add a standalone survey link beneath the Research Needs list, edit [_data/research_needs_survey.yml](_data/research_needs_survey.yml) and paste in the public respondent URL:

```yaml
text: Suggest an additional research need via our public survey
url: https://example.com/your-public-form-link
```

Use the public response link only, not the admin or edit link.

### Adding an event

Events live in [_data/events.yml](_data/events.yml), split into two lists: `upcoming:` and `past:`. Open the file and copy one of the existing entries as a template.

**Upcoming event** — needs a name, location, date, and a link (use `"#"` if there isn't one yet):

```yaml
upcoming:
  - name: CBI Monthly Meeting (July) — Guest speaker TBC
    location: Online (Teams)
    date: July 2026 (TBC)
    url: "#"
```

**Past event** — needs a short description (speaker, affiliation, date) and optionally a link to slides:

```yaml
past:
  - name: Title of the talk
    url: "#"
    description: "Speaker Name (Affiliation) presented on <topic>. Hosted by the ATRF Committee for Behavioural Insights on <date>."
    slides: /assets/presentations/speaker-name-talk-title.pdf   # optional — leave the line out if no slides
```

If you're attaching slides, upload the PDF to [assets/presentations/](assets/presentations/) first (same **Add file → Upload files** flow as for headshots), then reference the filename in the `slides:` line.

When an upcoming event has happened, simply move the entry from the `upcoming:` list down to the `past:` list and add a `description:` line.

## Developer notes

### Stack

- **Jekyll 4.x** static site (see [Gemfile](Gemfile)).
- **[Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes)** theme, pinned to `4.26.2` and pulled in via `jekyll-remote-theme` rather than vendored — see `remote_theme:` in [_config.yml](_config.yml). The theme's source files are *not* in this repo; only the overrides we need.
- Hosted on **GitHub Pages**, built and deployed by the workflow at [.github/workflows/jekyll.yml](.github/workflows/jekyll.yml) on every push to `main`. There's no GitHub Pages branch — the action builds with full Jekyll (so plugins like `jekyll-remote-theme` work) and uploads the `_site/` artifact directly.

### Repo layout

| Path | What's there |
| --- | --- |
| [_config.yml](_config.yml) | Site-wide settings: title, baseurl, theme, plugins, footer/social links, Sass config. |
| [_data/](_data/) | Structured content driving the page sections — `people.yml`, `leadership.yml`, `events.yml`, `resources.yml`, `research_needs.yml`, `navigation.yml`. Editing these is the day-to-day way the site changes. |
| [index.md](index.md) | The single landing page. Front matter sets the splash hero; the body just `{% include %}`s the section partials in display order. |
| [_includes/sections/](_includes/sections/) | One HTML partial per page section (`about`, `research-needs`, `resources`, `events`, `team`). These are local — they're not part of Minimal Mistakes. |
| [_includes/masthead.html](_includes/masthead.html), [_includes/head/custom.html](_includes/head/custom.html) | **Local overrides** of theme partials. Jekyll picks the local copy over the remote-theme copy for any same-named file under `_includes/`. The masthead override exists for the dual-logo (CBI + ATRF) layout; `head/custom.html` is MM's intentional extension point for favicons/meta tags. |
| [assets/css/main.scss](assets/css/main.scss) | The site's compiled stylesheet. Imports the theme's skin and base styles, then layers our brand-colour and component overrides on top. Has front matter (so Jekyll runs it through Liquid + Sass). |
| [img/team/](img/team/) | Headshot JPGs. Filenames must match the `pic:` field in `_data/people.yml` / `_data/leadership.yml` (without the extension). `placeholder.jpg` is the default. |
| [assets/presentations/](assets/presentations/) | Slide PDFs referenced from past-event entries in `_data/events.yml`. |

### Local preview

```
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000/behavioural_insights_group/ (note the `baseurl` — the bare `http://localhost:4000/` will 404).

Note on some linux systems you might need to run `bundle config set --local path vendor/bundle` before the `bundle install` to avoid system gem permission errors.


### Deployment

A push to `main` triggers [.github/workflows/jekyll.yml](.github/workflows/jekyll.yml), which builds with `JEKYLL_ENV=production` and deploys to GitHub Pages. Build status is visible on the repo's **Actions** tab; the deployed URL is shown on the workflow run summary.
