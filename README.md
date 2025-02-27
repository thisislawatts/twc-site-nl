# TWC The Netherlands

This repository is responsible for most content visible on the website [techwerkers.nl](https://techwerkers.nl). The site is made with a static site generator called [Jekyll](https://jekyllrb.com/) in a language called Ruby.

## Getting Started

### With Docker (recommended)

We use Docker to have a reproducible development environment.
Before proceeding, install [Docker Compose](https://docs.docker.com/compose/install/) on your system.

1. Start the application with the command: `docker-compose up`
2. Access the application in a browser at `localhost:4000`
3. Execute other commands in the Docker container: `docker-compose run --rm --service-ports jekyll bash`

### Without Docker

1. Install dependencies: `bundle install`
2. Start a local server: `bundle exec jekyll serve`
3. Verify all internal links are valid: `bundle exec rake`
4. (Optional) to reproduce Netlify functions run `npx decap-server`; then you can access `/admin` or other Netlify services

Open a browser to localhost:4000

## Add an event

Add a file inside the [`_events`](_events) directory. Copy a previous file as a template, and make sure to include the right time zone for The Netherlands!

## Add a blog post (inside /blog)

Add a file inside the [`_blog`](_blog) directory. Copy a previous file as a template. If an author does not exist, add one inside [`_data/authors.yml`](_data/authors.yml). A name is the only thing necessary, but photo is optional too.

## Add a press mention

Inside [`_data/press.yml`](_data/press.yml) file, add a media entry, with date format in `YYYY-MM-DD`.

## Translation

I18n (internationalization) is made available with the [jekyll-multiple-languages-plugin](https://github.com/kurtsson/jekyll-multiple-languages-plugin/). When a page has a translated version available, a link will show up on the top right if you use the [default_translate](_layouts/default_translate.html) layout. English is the default language, while other languages have their two letter ISO code prefixed, for example [TechWorkersCoalition.org/ru](https://TechWorkersCoalition.org/ru) for Russian.

### Localise date
Normally displaying a date is done using native liquid templates `{{ page.date | date: '%-d %B %Y' }}`, but for localisation, we need to pass it a language which can be done using our custom [_plugins/i18n_filter.rb](_plugins/i18n_filter.rb), and translation keys. We would replace our liquid template with the following:

`{{ page.date | localize: site.lang, '%-d %B %Y' }}`

### Adding new language
1. Add new language key to [en.yml](_i18n/en.yml)
2. Add two letter iso code in [config](_config.yml). The order here determines the order shown on the page. English must be first.
3. Inside the [i18n](_i18n) directory create a
  - `LANGUAGE.yml` with the language key and value in its own language, for example `es: Español`

Note, only the default [en.yml](_i18n/en.yml) must contain the names of each language. The other language yaml files contain just their own language key. To include only certain languages, specify the exact language keys you want. For example `languages: ["en", 'ja']`

![Screen Shot 2019-07-21 at 14 48 46](https://user-images.githubusercontent.com/7111514/61591397-cb0cd180-abc6-11e9-9876-1577d5c8b4bd.png)


### API feeds

Currently [techworkerscoalition.org](https://techworkerscoalition.org) uses Berlin press and events either from GitHub or directly from our exposed APIs e.g [/events.json](https://techwerkers.nl/events.json). You can find other uses cases [here](https://github.com/techworkersco/twc-site/blob/master/_config.yml#L32)


### Supported Pages
* Landing Page [index.yml](index.md)
* Join Page [join.md](join.md)
* Events [events.md](events.md)
* Press mentions [press_mentions.md](press_mentions.md)

### Supported Languages
* English
* German
* Russian
* Polish
