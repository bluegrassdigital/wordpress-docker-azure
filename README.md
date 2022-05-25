# WordPress-Azure-Docker
This open source Docker project is designed to speed up the execution of PHP applications on Azure that require App Service Storage to be enabled. With App Service Storage enabled, the latency is considerably high. This Docker image eliminates latency by running a sync from the shared  `/home`  folder to a local  `/homelive`  folder when the  `DOCKER_SYNC_ENABLED`  environment variable is set. The sync is unidirectional - on startup it syncs from /home to /homelive (with rsync) and on changes to files in /homelive it syncs back to /home (with unison).

## Features
- Based on PHP 8.0
- Apache server
- Pre-installed PHP extensions
- Optimized for WordPress

## Using on app service


## Development
### Prerequisites
- [Docker](https://www.docker.com/)
### Building the Docker image
To build the Docker image, clone the repository and run the following command in the project directory:
docker build -t <your-image-name> .
Replace  `<your-image-name>`  with the desired name for the Docker image.
### Deploying to Dockerhub
You can deploy the image to Dockerhub by following these steps:
1. Log in to your Dockerhub account:
docker login
2. Tag the image:
docker tag <your-image-name> <your-dockerhub-username>/<your-image-name>:<tag>
Replace  `<your-dockerhub-username>` ,  `<your-image-name>` , and  `<tag>`  with the appropriate values.
3. Push the image to Dockerhub:
docker push <your-dockerhub-username>/<your-image-name>:<tag>
### Running the Docker container
To run the Docker container, execute the following command:
docker run -d -p 2222:2222 -p 80:80 --name <container-name> <your-image-name>
Replace  `<container-name>`  and  `<your-image-name>`  with the desired container name and Docker image name, respectively.
## Environment variables
The following environment variables can be set to configure the container:
-  `DOCKER_SYNC_ENABLED`  - Enables Docker Sync when set
-  `APACHE_LOG_DIR`  - Path to Apache access and error logs (default:  `/home/LogFiles/sync/apache2` )
-  `APACHE_DOCUMENT_ROOT`  - Path to the Apache document root (default:  `/home/site/wwwroot` )
-  `APACHE_SITE_ROOT`  - Path to the Apache site root (default:  `/home/site/` )
-  `WP_CONTENT_ROOT`  - Path to the WordPress content root (default:  `/home/site/wwwroot/wp-content` )
## License
This project is open source and available under the [MIT License](LICENSE).
