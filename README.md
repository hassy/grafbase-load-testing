# Load testing Grafbase with Artillery

Grafbase is a unified data layer platform, that lets you combine your data sources into a centralized GraphQL endpoint. Grafbase manages all the infrastructure for you to let you focus on shipping products instead of building infrastructure.

This repo contains example scripts to show how a Grafbase deployment can be load tested with Artillery.

The application under test is the [example BaseNews application](https://grafbase.com/docs/quickstart/get-started).

## Run a test

1. Follow the Grafbase guide to deploy an application from the schema under `grafbase/` in this repo.
2. Install Artillery with `npm install -g artillery`
3. Export your Grafbase API key with `export GRAFBASE_API_KEY=yourkey`
4. Run the Artillery test with:

    ```sh
    artillery run -e prod artillery/create-post.yml
    ```
5. Scale out and run the same test from AWS Lambda:

    ```sh
    artillery run --platform aws:lambda --count 10 --platform-opt region=eu-central-1 -e prod artillery/create-post.yml
    ```
