# Dockerfile for Flask app
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy application files to the container
COPY . /app

# Install dependencies
RUN pip install -r requirements.txt

# Expose the port the Flask app runs on
EXPOSE 5000

# Command to run the application
CMD ["python", "app.py"]


