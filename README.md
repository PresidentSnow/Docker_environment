# Docker_environment
Repo for manage the Docker images, containers and his environment.

* Container for Wordpress.
    - If there's problem with this:
    
    'The theme directory "twentytwentyfive" does not exist.
    Error: The themes directory is either empty or does not
    exist. Please check your installation.'

    Do this steps:

    docker exec -u root -it wp_app bash

    ls -la /var/www/html/wp-content/themes/

    apt-get update
    apt-get install -y wget

    cd /tmp
    wget https://wordpress.org/latest.tar.gz
    tar -xzf latest.tar.gz
    cp -r wordpress/wp-content/themes/* /var/www/html/wp-content/themes/
    chown -R [wp_user]:[wp_user] /var/www/html/wp-content/themes/

    ls -la /var/www/html/wp-content/themes/
