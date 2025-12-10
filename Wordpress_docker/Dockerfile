FROM wordpress:latest

# Install PHP extensions and other tools
RUN apt-get update && apt-get install -y \
    nano curl wget \
    && rm -rf /var/lib/apt/lists/*

# Create user and personalized
RUN groupadd -g 1001 wpuser && \
    useradd -u 1001 -g 1001 -m -s /bin/bash wpuser

# Create directory for the user and change permissions
RUN mkdir -p /home/wpuser && chown -R wpuser:wpuser /home/wpuser

# Change Wordpress permissions
RUN chown -R wpuser:wpuser /var/www/html && \
    chmod 755 /var/www/html && \
    find /var/www/html -type d -exec chmod 755 {} \; && \
    find /var/www/html -type f -exec chmod 644 {} \;

# Change non-privileges user
USER wpuser

# Establish work directory
WORKDIR /var/www/html
EXPOSE 80