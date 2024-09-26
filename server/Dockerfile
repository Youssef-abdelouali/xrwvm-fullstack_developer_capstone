# Use Python 3.12 slim image as the base
FROM python:3.12.0-slim-bookworm

# Environment variables to avoid buffering and bytecode creation
ENV PYTHONBUFFERED 1
ENV PYTHONWRITEBYTECODE 1

# Set the working directory inside the container
ENV APP=/app
WORKDIR $APP

# Copy the requirements.txt file and install dependencies
COPY requirements.txt $APP
RUN pip3 install --no-cache-dir -r requirements.txt

# Copy the rest of the application files
COPY . $APP

# Expose the port the app will run on
EXPOSE 8000

# Give execute permission to the entrypoint script
RUN chmod +x /app/entrypoint.sh

# Set the entrypoint to run the shell script
ENTRYPOINT ["/bin/bash", "/app/entrypoint.sh"]

# Command to run the application using gunicorn
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi"]
