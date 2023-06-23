# Load testing Grafbase with Artillery

Grafbase is a unified data layer platform, that lets you combine your data sources into a centralized GraphQL endpoint. Grafbase manages all the infrastructure for you to let you focus on shipping products instead of building infrastructure.

This repo contains example scripts to show how a Grafbase deployment can be load tested with Artillery.

The application under test is the [example BaseNews application](https://grafbase.com/docs/quickstart/get-started).

## Run a test

1. Follow the [Grafbase quickstart guide](https://grafbase.com/docs/quickstart/get-started) to deploy an application from the schema under `grafbase/` in this repo.
2. Install Artillery with `npm install -g artillery` and set up AWS credentials to run [distributed tests on AWS Lambda](https://www.artillery.io/docs/load-testing-at-scale/aws-lambda)
3. Create a dotenv file with your Grafbase API key:
    ```
    echo "GRAFBASE_API_KEY=yourkey" >> .env
    ```
4. Run the Artillery test locally with:

    ```sh
    artillery run -e prod --dotenv .env artillery/basenews-post-and-comment.yml
    ```
5. Scale out and run the same test from AWS Lambda - using 10 workers in `us-east-1`:

    ```sh
    artillery run:lambda --region us-east-1 --count 10 -e prod --dotenv .env artillery/basenews-post-and-comment.yml
    ```
