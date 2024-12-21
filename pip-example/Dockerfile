# The build stage, with all of the dependencies
FROM ghcr.io/astral-sh/uv:python3.11-bookworm-slim AS builder

RUN python -m venv /opt/venv
# Make sure we use the virtualenv:
ENV PATH="/opt/venv/bin:$PATH"

# Copy over and install the requirements
COPY requirements.txt .
RUN pip install -r requirements.txt

# Now we move to a new image, without the build dependencies
FROM python:3.11-slim-bookworm AS final
COPY --from=builder /opt/venv /opt/venv

COPY . /app
WORKDIR /app

# Make sure we use the virtualenv
ENV PATH="/opt/venv/bin:$PATH"
