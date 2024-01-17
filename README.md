[![Build status](https://github.com/navikt/helseopplysninger-pdfgen/workflows/Build,%20push%20and%20deploy/badge.svg)](https://github.com/navikt/helseopplysninger-pdfgen/workflows/Build,%20push%20and%20deploy/badge.svg)
# Helseopplysninger PDF generator
Repository for team helseopplysninger pdfgen templates.

## Technologies & Tools

* [pdfgen](https://github.com/navikt/pdfgen)

#### Creating a docker image
Creating a docker image should be as simple as
```bash
docker build -t helseopplysninger-pdfgen .
```

## Getting started
### Run in development mode
To run the application with templates, data and fonts locally mounted you can use
```bash
export CURRENT_PATH="$(cd "$(dirname "$1")" || exit; pwd)/$(basename "$1")" && 
docker run \
        -v "$CURRENT_PATH"/templates:/app/templates \
        -v "$CURRENT_PATH"/fonts:/app/fonts \
        -v "$CURRENT_PATH"/data:/app/data \
        -v "$CURRENT_PATH"/resources:/app/resources \
        -p 8080:8080 \
        -e DISABLE_PDF_GET=false \
        -e JDK_JAVA_OPTIONS \
        -it \
        --rm \
        ghcr.io/navikt/pdfgen:2.0.17
```

Or you can use the convenience script
```bash
./run_development.sh
```

When running the application you can use the env var `DISABLE_PDF_GET` to enable GET requests at
`/api/v1/genpdf/<application>/<template>` which looks for test data at `data/<application>/<template>.json` and outputs
a PDF to your browser. Additionally, the template folder will be fetched on every request, and reflect any changes made
since the last GET, making this ideal for developing new templates for your application.

The template and data directory structure both follow the `<application>/<template>` structure.
Example url: `http://0.0.0.0:8080/api/v1/genpdf/helseopplysninger/legeerklaering-pleiepenger-for-sykt-barn`

### Contact

This project is maintained by [navikt/teams/helseopplysninger](CODEOWNERS)

Questions and/or feature requests? Please create an [issue](https://github.com/navikt/helseopplysninger-pdfgen/issues)

If you work in [@navikt](https://github.com/navikt) you can reach us at the Slack
channel [#team-helseopplysninger](https://nav-it.slack.com/archives/C01AQTAU3CH)
