
```markdown
# Installing Nextcloud with Docker and MariaDB

This repository provides an example configuration for installing Nextcloud using Docker and MariaDB. By following the steps outlined here, you will be able to set up an instance of Nextcloud with the necessary containers.

## Prerequisites

Ensure you have the following installed on your system:

- **Docker**: [Docker Installation Guide](https://docs.docker.com/get-docker/)
- **Docker Compose**: [Docker Compose Installation Guide](https://docs.docker.com/compose/install/)

## Project Structure

The project includes a `docker-compose.yml` file that defines the following containers:

- **Nextcloud**: The Nextcloud application for file management.
- **MariaDB**: The database used to store Nextcloud data.
- **Redis**: A caching system to improve Nextcloud performance.
## Creating the Network

Before running the Docker containers, you need to create a Docker network named `nextcloud`:

```bash
docker network create nextcloud


### Container Descriptions

- **MariaDB**:
  - **Image**: `mariadb:10.6`
  - **Environment Variables**:
    - `MYSQL_ROOT_PASSWORD`: Password for the root user.
    - `MYSQL_DATABASE`: Name of the Nextcloud database.
    - `MYSQL_USER`: Database username.
    - `MYSQL_PASSWORD`: Database user password.
  - **Volume**: Persistent storage for database data.

- **Nextcloud**:
  - **Image**: `nextcloud:latest`
  - **Dependencies**: This container depends on the `db` and `redis` containers.
  - **Environment Variables**:
    - `NEXTCLOUD_ADMIN_USER`: Administrator username for Nextcloud.
    - `NEXTCLOUD_ADMIN_PASSWORD`: Administrator password for Nextcloud.
    - `NEXTCLOUD_DB_TYPE`: Database type (mysql).
    - `NEXTCLOUD_DB_HOST`: Database host.
    - `NEXTCLOUD_DB_USER`: Database user.
    - `NEXTCLOUD_DB_PASSWORD`: Database password.
    - `NEXTCLOUD_REDIS_HOST`: Redis host.
  - **Volume**: Persistent storage for Nextcloud data.
  - **Ports**: The Nextcloud service is accessible locally on port **8080**.

- **Redis**:
  - **Image**: `redis:alpine`
  - **Volume**: Persistent storage for caching data.

## Installation Instructions

1. **Clone the repository**:

   ```bash
   git clone https://github.com/your-username/install-nextcloud-in-docker.git
   cd install-nextcloud-in-docker
   ```

2. **Start the containers**:

   ```bash
   docker-compose up -d
   ```

3. **Access Nextcloud**:

   After the containers are up and running, you can access Nextcloud through your browser at the following address:

   ```
   http://your-public-ip:8080
   ```

4. **Configure Redis**:

   Modify the `config.php` file of Nextcloud to enable Redis as the caching system. You can find the configuration file in the Nextcloud volume. Make sure to add the following lines:

   ```php
   'memcache.local' => '\\OC\\Memcache\\Redis',
   'memcache.locking' => '\\OC\\Memcache\\Redis',
   'redis' => [
       'host' => 'nextcloud_redis',
       'port' => 6379,
   ],
   ```

5. **Restart the Nextcloud container**:

   ```bash
   docker restart nextcloud
   ```

## Conclusion

You now have a working instance of Nextcloud running on Docker with MariaDB and Redis configured. You can start using Nextcloud to manage your files and collaborate with others.

For more information, visit the [Nextcloud Official Documentation](https://docs.nextcloud.com/).
```

### Customization
Please remember to replace `your-username` and `your-public-ip` with the appropriate values when you set up the repository. If you need any more modifications or assistance, just let me know!

--- 

If you found this guide helpful and would like to support the project, consider making a donation. Your contributions help maintain and improve this resource.

### Donate via Bitcoin
You can send Bitcoin directly to the following address:

**`bc1qy0l39zl7spspzhsuv96c8axnvksypfh8ehvx3e`**

### Donate via Lightning Network
For faster and lower-fee donations, you can use the Lightning Network:

**asyscom@sats.mobi**

Thank you for your support!

## License
This project is licensed under the MIT License.
