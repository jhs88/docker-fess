# OpenSearch POC

A fork of [codelibs/docker-fess](https://github.com/codelibs/docker-fess) which contains configuration & Dockerfiles for Fess and OpenSearch.
Elastic Search is also compatible, but this POC is focused on OpenSearch.
The compose folder contains default example environment with Fess and OpenSearch.

## Getting Started

### Install Docker

Install Docker and Docker Desktop

- [Docker installation Windows](https://docs.docker.com/desktop/install/windows-install/)
- [Docker installation Mac](https://docs.docker.com/desktop/install/mac-install/)
- [Docker installation Linux](https://docs.docker.com/desktop/install/linux-install/)

### Clone Repo

```bash
git clone https://gitlab.com/klish-group/fess-poc.git fess-poc
cd fess-poc
```

### Build and Run Fess and OpenSearch containers

```bash
# (add build to rebuild the images)
docker compose up -d --build
```

### Import Fess configuration

1) Login to [Fess Dashboard](http://localhost:8080/login). Default credentials are `admin/admin`.
2) Navigate to the `System Info` tab and select `Back Up`. 
3) Upload the `fess_basic_config.bulk` file to import configuration.
4) Click on play button in top right corner and start the default crawling job.

You should now have some data in your search engine.

## Fess Docker

Custom Dockerfiles for each version of Fess are available in the `fess` directory.
They can also be downloaded directly from the [Docker Hub](https://hub.docker.com/r/codelibs/fess).

This POC uses a custom build of Fess 14 (see `compose.yml`).
This is because the official Docker image does not include the dependencies required for indexing dynamic content like client-side rendered pages.
This is controlled by the playwright library. Fess documentation does not mention this dependency, but it is required for indexing dynamic content.

### Fess Search API Endpoints

A list of Fess API endpoints can be found in the [Fess documentation](https://fess.codelibs.org/14.17/api/api-search.html).

## OpenSearch Docker

Custom Dockerfiles for each version of OpenSearch are available in the `opensearch` directory.
A custom Dockerfile for OpenSearch Dashboards is also included in `compose/dashboards` for the default example environment.
The custom Dockerfile is removing the default security plugin. This configuration can be achieved by adding environment variables to default docker images:

### `opensearchproject/opensearch`:

- `DISABLE_INSTALL_DEMO_CONFIG=true`  
- `DISABLE_SECURITY_PLUGIN=true`

### `opensearchproject/opensearch-dashboards`:

- `DISABLE_SECURITY_DASHBOARDS_PLUGIN=true`

For more information on OpenSearch Docker images, see the [OpenSearch Docker documentation](https://opensearch.org/docs/latest/install-and-configure/install-opensearch/docker/).

## Validating the Setup

1) Follow the steps in the `Getting Started` section.
2) Query the search engine in the searchbox at [http://localhost:8080/](http://localhost:8080/).
3) Searching 'fluint' should pin the about page to the top of the search results.

## Issues

- Dynamic Content is not working
- Cannot get synonyms to work in Fess but they work when directly querying OpenSearch
