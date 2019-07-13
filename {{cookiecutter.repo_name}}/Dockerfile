FROM python:3.7 AS base

ARG DEV_{{ cookiecutter.package_name }}
ARG CI_USER_TOKEN
RUN echo "machine github.com\n  login $CI_USER_TOKEN\n" >~/.netrc

ENV \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONHASHSEED=random \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    PIP_SRC=/src \
    PIPENV_HIDE_EMOJIS=true \
    PIPENV_COLORBLIND=true \
    PIPENV_NOSPIN=true

RUN pip install pipenv

WORKDIR /app
COPY Pipfile .
COPY Pipfile.lock .
COPY setup.py .
COPY src/{{ cookiecutter.package_name }}/__init__.py src/{{ cookiecutter.package_name }}/__init__.py
RUN pipenv install --system --deploy --ignore-pipfile --dev