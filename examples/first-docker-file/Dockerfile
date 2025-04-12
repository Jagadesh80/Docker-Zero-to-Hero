# --- Stage 1: Build Stage ---
FROM ubuntu:latest as builder

# Set working directory
WORKDIR /app

# Copy files into the build container
COPY . /app

# Install build dependencies
RUN apt-get update && apt-get install -y python3 python3-pip

# Install Python packages into /install directory
RUN pip3 install --upgrade pip && \
    pip3 install -r requirements.txt --target /install

# --- Stage 2: Final Image ---
FROM ubuntu:latest

# Set environment variable
ENV NAME World

# Set working directory
WORKDIR /app

# Install only runtime dependencies
RUN apt-get update && apt-get install -y python3

# Copy app source code from build stage
COPY --from=builder /app /app

# Copy installed python packages from builder stage
COPY --from=builder /install /usr/local/lib/python3.10/dist-packages

# Set the default command
CMD ["python3", "app.py"]

