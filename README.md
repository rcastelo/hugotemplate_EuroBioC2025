
# European Bioconductor Conference 2025 Website

This repository contains material for the European Bioconductor annual conference. 
View the corresponding [GitHub repo](https://github.com/rcastelo/EuroBioC2025).
Created using [BioC_template](https://github.com/Bioconductor/BioC_template), and
the contents of the website of the previous 2024 edition of the conference. There
may be contents corresponding to 2024, they will be updated soon.

Run Hugo to preview the webpage locally.

```shell
# UNIX
rm -rf public; hugo --verbose; hugo server --disableFastRender --verbose
# MS Windows
rm -rf public; hugo --verbose; hugo.exe server --disableFastRender --verbose
```

# Adding items to the schedule table

1. Make changes in the "schedule table" spreadsheet https://docs.google.com/spreadsheets/d/1tGtGffcbCRxQFjE3ej42IcWlN4FJCsuQeZvETt9g0oA/edit#gid=0. NOTE - For the "time" column, set the format to custom "hh:mm" (IMPORTANT)
2. Run the following command in the terminal in the base directory:
```bash
Rscript --vanilla 1_create_yaml.R; bash 2_create_abstracts.sh; bash 3_create_tracks.sh
```

### Adding data for the schedule

+ Data for the abstracts and other elements for the schedule table should be located in `data/abstracts/`. This folder is populated by `1_create_yaml.R` from the "schedule table" spreadsheet.

There are three types of abstracts.

1. papers. Name format: day1_1315_longWorkshop_paper25.yaml. 
2. tracks. Name format: day1_0900_shortTalksSysEpi_track.yaml.
3. All other elements that will be added to the schedule.

Abstract file name format: day[1-3]_HHMM_type_paper/track#.yaml. 
The abstracts should all contain these fields. If any field isn't used, it should remain blank. 

```
title: "" # A string with the full title.
paper: "" # Number of paper or track. Valid options: paper# or track#. For example, paper2, track1, etc. track is only used for the short talks tracks. There is no defined track number as in the case of the papers, they should be added in order of appearance in the document.
session_type: "" # String with the type. Valid options: "Short talk", "Short talks track", "Package demo", "Workshop".
authors: "" # String with the authors separated by comma.
presenting_author: "" # Author who will present. The first author by default.
affiliation: "" # String with the affiliation.
abstract: "" # String with the abstract. Sometimes there are quotes in the text which should be escaped.
time: "" # The time in 24h format. Example: 1300 for 1 PM.
github: "" # Haven't used this field. Not sure if this has been provided.
twitter: "" # Twitter handle without the @.
youtube: "" # Link to youtube video when available.
day: "" # Valid options: day1, day2, day3.
talks: "" # This field is only for the short talk tracks. This should list the number of papers under this track. This should be a YAML array. Example: ["paper10", "paper20"]
```

+ The `content/abstracts/` directory contains the individual pages for the
abstracts. This directory could be ignored as it will be updated with
the `2_create_abstracts.sh` and `3_create_tracks.sh` bash scripts. These scripts
convert the elements in data to content pages.

======

# data

YAML files that need to be adjusted for each conference. 

## abstracts

YAML files for every event.
`Workshop_paper` are processed by [content/workshops.md](content/workshops.md) and [layouts/shortcodes/workshops.html](layouts/shortcodes/workshops.html).
All events are processed by [layouts/shortcodes/schedule.html](layouts/shortcodes/schedule.html).

File naming convention: `<day[:digit:]+>_<HHMM>_<type>_paper[:digit:]+.yaml`.

Examples:

- `day1_0915_OpeningSession.yaml`
- `day1_0930_Keynote.yaml`
- `day1_1015_Shorttalk_paper19.yaml`
- `day1_1030_Coffeebreak.yaml`

Documentation needed:

- `day1_1015_Shorttalkstrack_track1.yaml` : What does this do? How are tracks managed?

## carousel

YAML files for the carousel panels. Processed by the main theme.

## clients

YAML files for sponsors.
Processed by the main theme and [layouts/shortcodes/sponsors.html](layouts/shortcodes/sponsors.html)

File naming convention: `<unique_numeric_id>.<name>.<level>.yaml`

Contents:

```
name: "Sponsor name"
name2: ""
image: "/img/clients/sponsor_logo.png"
name2: ""
url: "https://sponsor_url.com"
name2: ""
level: "platinum" # one of: platinum|gold|silver|other|patronage|academic_supporter
name2: ""
```

## organizers

YAML files for co-chairs and committee. Processed by [content/organizers.md](content/organizers.md), [layouts/shortcodes/cochairs.html](layouts/shortcodes/cochairs.html) and [layouts/shortcodes/committee.html](layouts/shortcodes/committee.html).

## speakers

YAML files for each speaker.
Processed by [layouts/partials/speakers.html](layouts/partials/speakers.html).

File naming convention: `<unique_numeric_id>.yaml`

Contents:

```
text: "Biography including link to web page."
name: "FirstName LastName, Keynote"
position: "Position, Institution"
avatar: "img/speakers/avatar.png"
```

## Registration and payment

The registration form can be found in [layouts/shortcodes/registrationForm.html](layouts/shortcodes/registrationForm.html) and is embedded in [content/registration.md](content/registration.md).  We use the [Netlify Forms](https://www.netlify.com/products/forms/) functionality to capture each input.  We then use [Zapier](www.zapier.com) to insert each form entry into a new row of a Google Sheet.  An example Zapier workflow for EuroBioc2023 can be found at https://zapier.com/shared/4359ba00c688fff90371d071fc364d2619b1d53c

The code behind the PayPal payment form is found in [content/payment.md](content/payment.md).  This is produced by PayPal for each event and can be copied directly into the file, replacing whatever is already there.  **The form code includes links to "success" and "cancellation" pages that should be updated for the specific event.**

# Disclaimer

This template was created using the modified.
[hugo-universal-theme](https://github.com/devcows/hugo-universal-theme).
See the [demo web site](https://themes.gohugo.io/theme/hugo-universal-theme/),
the original [github repository](https://github.com/devcows/hugo-universal-theme)
and the [exampleSite files](https://github.com/devcows/hugo-universal-theme/tree/master/exampleSite).
Template by [Bootstrapious](https://bootstrapious.com/p/universal-business-e-commerce-template).
Ported to Hugo by [DevCows](https://github.com/devcows/hugo-universal-theme).
The theme is added as selected files, not as a submodule, for easier modification.

