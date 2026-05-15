ATRF Behavioural Insights Group (BIG)
=====================================

> **This is a preview site. Content has not been reviewed or endorsed.**


Source for the website of the Behavioural Insights Group, a standing group of the
[Australasian Transport Research Forum (ATRF)](https://australasiantransportresearchforum.org.au/).



## Editing

### Editing tutorial
This tutorial is for the PT Research Committee website. While the layout of our site is slightly different, the github workflow is the same.
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

