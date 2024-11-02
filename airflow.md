# airflow

## Prerequisite

- Python 3.8+
- Linux, MacOS, Windows ( WSL2 )

## Installation

1. Create a new directory for airflow

```sh
mkdir airflow
```

2. Create a new virtual environment

```sh
cd airflow
virtualenv .venv
```

3. Install airflow

Linux, MacOS

```sh
source .venv/bin/activate
```

Install package

```sh
python -m pip install apache-airflow
```

## First start

```sh
airflow standalone
```

This command will start the airflow webserver and scheduler.

Also, it will initialize the database.

## Service Registration

going to edit in future
