FROM wordpress:latest

# Install PHP extensions
RUN apt-get update && apt-get install -y \
    nano \
    && rm -rf /var/lib/apt/lists/*

# Create user and personalized
RUN groupadd -r wpuser && useradd -r -g wpuser wpuser

# Create directory for the user and change permissions
RUN mkdir -p /home/wpuser && chown -R wpuser:wpuser /home/wpuser

# Change Wordpress permissions (just read for the user)
RUN chown -R wpuser:wpuser /var/www/html

# Change non-privileges user
USER wpuser

# Establish work directory
WORKDIR /var/www/html

# Expose port
EXPOSE 80