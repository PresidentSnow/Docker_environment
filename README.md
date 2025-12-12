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
