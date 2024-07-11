# Official image
FROM python:3.12-slim

# Working directory in the container
WORKDIR /application

# Copies the current directory contents into the container at /application
COPY . /application/

# Copy pyproject.toml and poetry.lock to the working directory
COPY pyproject.toml poetry.lock ./

# Install poetry
RUN pip install poetry

# Install any needed packages specified in pyproject.toml
RUN poetry install --no-root

# Make sure the prestart script is executable
RUN chmod +x /application/prestart.sh

ENV PYTHONPATH=/application

# Make port available outside this container
EXPOSE 8000

# Start the application
CMD ["bash", "-c", "poetry run /application/prestart.sh && poetry run uvicorn app.main:app --proxy-headers --reload --host 0.0.0.0 --port 8000"]