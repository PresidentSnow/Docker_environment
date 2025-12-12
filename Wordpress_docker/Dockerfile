FROM wordpress:latest

ARG WP_UID=1002
ARG WP_GID=1002
ARG WP_USER=wordpress-app

# Install PHP extensions and other tools
RUN apt-get update && apt-get install -y \
    nano curl wget \
    && rm -rf /var/lib/apt/lists/*

# Create user and personalized
RUN groupadd -g ${WP_GID} ${WP_USER} && \
    useradd -u ${WP_UID} -g ${WP_GID} \
    -s /usr/sbin/nologin -M -d /nonexistent \
    ${WP_USER}

# Create directory for the user and change permissions
RUN mkdir -p /home/${WP_USER} && chown -R ${WP_USER}:${WP_USER} /home/${WP_USER}
RUN mkdir -p /var/www/html/wp-content/uploads \
    /var/www/html/wp-content/upgrade \
    /var/www/html/wp-content/cache \
    /var/www/html/wp-content/languages

# Change Wordpress permissions
RUN chown -R ${WP_USER}:${WP_USER} /var/www/html
RUN chmod 755 /var/www/html && \
    find /var/www/html -type d -exec chmod 755 {} \; && \
    find /var/www/html -type f -exec chmod 644 {} \; && \
    chmod -R 775 /var/www/html/wp-content/uploads \
    /var/www/html/wp-content/upgrade \
    /var/www/html/wp-content/cache

# Monitoring
HEALTHCHECK --interval=30s --timeout=3s --start-period=30s --retries=3 \
    CMD curl -f http://localhost/ || exit 1

USER ${WP_USER}

# Establish work directory
WORKDIR /var/www/html
EXPOSE 80