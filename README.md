# Steam Games Vector DB Recommender

## Introduction
This project uses [Milvus](https://milvus.io/) as a vector db to store the video games' similarity, [FastAPI](https://fastapi.tiangolo.com/) for the backend and [streamlit](https://streamlit.io/) for the frontend.


## Prerequisites

- A Kaagle API to download the data

- A Milvus API to upload the data

## Getting Started

To get started, simply download the Steam Games dataset from [kaggle](https://www.kaggle.com/datasets/fronkongames/steam-games-dataset) in the notebook at the Notebook folder.

The Notebook has all the code to get started and uploading the data to Milvus.


## Poetry

This project uses poetry. It's a modern dependency management
tool.

```bash
poetry install
poetry run python -m recommender_api
```

This will start the server on the configured host.

You can find swagger documentation at `/api/docs`.

You can read more about poetry here: https://python-poetry.org/

## Docker

You can start the project with docker using this command:

```bash
docker-compose -f deploy/docker-compose.yml --project-directory . up --build
```

If you want to develop in docker with autoreload add `-f deploy/docker-compose.dev.yml` to your docker command.
Like this:

```bash
docker-compose -f deploy/docker-compose.yml -f deploy/docker-compose.dev.yml --project-directory . up --build
```

This command exposes the web application on port 8000, mounts current directory and enables autoreload.

But you have to rebuild image every time you modify `poetry.lock` or `pyproject.toml` with this command:

```bash
docker-compose -f deploy/docker-compose.yml --project-directory . build
```

## Project structure

```bash
$ tree "Steam Games Recommender"
recommender_frontend
recommender_api
├── conftest.py  
├── __main__.py  
├── services 
├── settings.py  
├── static  
├── tests  
└── web 
    ├── api 
    │   └── router.py 
    ├── application.py  
    └── lifetime.py  
```

## Configuration

You can create `.env` file in the root directory and place all
environment variables here.

All environment variables should start with "RECOMMENDER_API_" prefix.

For example if you see in your "recommender_api/settings.py" a variable named like
`random_parameter`, you should provide the "RECOMMENDER_API_RANDOM_PARAMETER"
variable to configure the value. This behaviour can be changed by overriding `env_prefix` property
in `recommender_api.settings.Settings.Config`.

An example of .env file:
```bash
RECOMMENDER_API_RELOAD="True"
RECOMMENDER_API_PORT="8000"
RECOMMENDER_API_ENVIRONMENT="dev"
RECOMMENDER_API_MILVUS_URI = "...zillizcloud.com"
RECOMMENDER_API_MILVUS_TOKEN = "fake-token-text"
RECOMMENDER_API_COLLECTION_NAME =  "fake-collection-name"
```

You can read more about BaseSettings class here: https://pydantic-docs.helpmanual.io/usage/settings/


## Running tests

For running tests on your local machine.

```bash
pytest -vv . -p no:warnings
```
