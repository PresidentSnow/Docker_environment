# Docker_environment
Repo for manage the Docker images, containers and his environment.

* Tips for docker containers:
    - To create a non user without privileges, for specific service or docker container. You can run this command for create new user:

        sudo adduser --system --uid 115 \
            --no-create-home \
            --group \
            --home /var/empty \
            --shell /usr/sbin/nologin \
            wp_user
        
        This is just an example; the '115' (UID) can be whatever you want, BUT it's important that it's in the range of 100-999 and not already use by another service or user in your system. On the other hand, the 'wp_user' (username) follows the same rule; it can be whatever you want, but it mustn't already be used by others in your system.

* Container for Wordpress:
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
    
    - For change the language of the Wordpress, follow this steps:

        1. Enter the docker container.

        2. Access to the '/var/www/html/wp-content/languages' and if it doesn't exist, created it.
        
        3. After that, enter in to the folder and execute this:
            wget https://downloads.wordpress.org/translation/core/[WORDPRESS_VERSION]/[LANGUAGE].zip
        
        4. Decompress the file with unzip.

        5. Remove the .zip file.
        rm es_ES.zip

        6. Add in the file '/var/www/html/wp-config.php' INSIDE of the docker container this line:

        define('WPLANG', 'es_ES');
        
        *IMPORTANT*: put this line BEFORE this line: /* That's all, stop editing! Happy publishing. */
