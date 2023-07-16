<a href="https://elest.io">
  <img src="https://elest.io/images/elestio.svg" alt="elest.io" width="150" height="75">
</a>

[![Discord](https://img.shields.io/static/v1.svg?logo=discord&color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=Discord&message=community)](https://discord.gg/4T4JGaMYrD "Get instant assistance and engage in live discussions with both the community and team through our chat feature.")
[![Elestio examples](https://img.shields.io/static/v1.svg?logo=github&color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=github&message=open%20source)](https://github.com/elestio-examples "Access the source code for all our repositories by viewing them.")
[![Blog](https://img.shields.io/static/v1.svg?color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=elest.io&message=Blog)](https://blog.elest.io "Latest news about elestio, open source software, and DevOps techniques.")

# Directus, verified and packaged by Elestio

[Directus](https://github.com/directus/directus) is a real-time API and App dashboard for managing SQL database content.

<img src="https://raw.githubusercontent.com/elestio-examples/directus/main/directus.jpg" alt="directus" width="800">

Deploy a <a target="_blank" href="https://elest.io/open-source/directus">fully managed directus</a> on <a target="_blank" href="https://elest.io/">elest.io</a> if you want automated backups, reverse proxy with SSL termination, firewall, automated OS & Software updates, and a team of Linux experts and open source enthusiasts to ensure your services are always safe, and functional.

[![deploy](https://github.com/elestio-examples/directus/raw/main/deploy-on-elestio.png)](https://dash.elest.io/deploy?source=cicd&social=dockerCompose&url=https://github.com/elestio-examples/directus)

# Why use Elestio images?

- Elestio stays in sync with updates from the original source and quickly releases new versions of this image through our automated processes.
- Elestio images provide timely access to the most recent bug fixes and features.
- Our team performs quality control checks to ensure the products we release meet our high standards.

# Usage

## Git clone

You can deploy it easily with the following command:

    git clone https://github.com/elestio-examples/directus.git

Copy the .env file from tests folder to the project directory

    cp ./tests/.env ./.env

Edit the .env file with your own values.

Create data folders with correct permissions

    mkdir -p ./uploads;
    chmod 777 ./uploads;

    mkdir -p ./extensions;
    chmod 777 ./extensions;

    mkdir -p ./extensions/displays;
    chmod 777 ./extensions/displays;

    mkdir -p ./data;
    chmod 777 ./data;

Run the project with the following command

    docker-compose up -d

You can access the Web UI at: `http://your-domain:8055`

## Docker-compose

Here are some example snippets to help you get started creating a container.

    version: "3.3"
    services:
        database:
            image: postgres:15
            restart: always
            volumes:
                - ./data:/var/lib/postgresql/data
            networks:
                - directus
            environment:
                POSTGRES_USER: "directus"
                POSTGRES_PASSWORD: ${SOFTWARE_PASSWORD}
                POSTGRES_DB: "directus"
        cache:
            image: redis:6
            restart: always
            networks:
                - directus
        directus:
            restart: always
            image: elestio4test/directus:${SOFTWARE_VERSION_TAG}
            ports:
                - 172.17.0.1:8055:8055
            user: 0:0
            volumes:
                - ./uploads:/directus/uploads
                - ./extensions:/directus/extensions
            networks:
                - directus
            depends_on:
                - cache
                - database
            environment:
                KEY: ${SOFTWARE_PASSWORD}
                SECRET: ${SOFTWARE_PASSWORD}
                PUBLIC_URL: https://${DOMAIN}
                DB_CLIENT: "pg"
                DB_HOST: "database"
                DB_PORT: "5432"
                DB_DATABASE: "directus"
                DB_USER: "directus"
                DB_PASSWORD: ${SOFTWARE_PASSWORD}
                EMAIL_FROM: ${EMAIL_FROM}
                EMAIL_TRANSPORT: "smtp"
                EMAIL_SMTP_HOST: "172.17.0.1"
                EMAIL_SMTP_PORT: 25
                EMAIL_SMTP_SECURE: "false"
                EMAIL_SMTP_IGNORE_TLS: "false"
                CACHE_ENABLED: "true"
                CACHE_STORE: "redis"
                CACHE_REDIS: "redis://cache:6379"
                REDIS: "redis://cache:6379"
                ADMIN_EMAIL: ${ADMIN_EMAIL}
                ADMIN_PASSWORD: ${ADMIN_PASSWORD}
                CACHE_AUTO_PURGE: "true"

    networks:
    directus:

### Environment variables

|       Variable       | Value (example) |
| :------------------: | :-------------: |
|    ADMIN_USERNAME    | test@gmail.com  |
|      EMAIL_FROM      | from@gmail.com  |
|    ADMIN_PASSWORD    |  your-password  |
|  SOFTWARE_PASSWORD   |  your-password  |
| SOFTWARE_VERSION_TAG |     latest      |
|        DOMAIN        | your.domain.com |

# Maintenance

## Logging

The Elestio Directus Docker image sends the container logs to stdout. To view the logs, you can use the following command:

    docker-compose logs -f

To stop the stack you can use the following command:

    docker-compose down

## Backup and Restore with Docker Compose

To make backup and restore operations easier, we are using folder volume mounts. You can simply stop your stack with docker-compose down, then backup all the files and subfolders in the folder near the docker-compose.yml file.

Creating a ZIP Archive
For example, if you want to create a ZIP archive, navigate to the folder where you have your docker-compose.yml file and use this command:

    zip -r myarchive.zip .

Restoring from ZIP Archive
To restore from a ZIP archive, unzip the archive into the original folder using the following command:

    unzip myarchive.zip -d /path/to/original/folder

Starting Your Stack
Once your backup is complete, you can start your stack again with the following command:

    docker-compose up -d

That's it! With these simple steps, you can easily backup and restore your data volumes using Docker Compose.

# Links

- <a target="_blank" href="https://github.com/directus/directus">Directus Github repository</a>

- <a target="_blank" href="https://docs.directus.io/getting-started/introduction.html">Directus documentation</a>

- <a target="_blank" href="https://github.com/elestio-examples/directus">Elestio/Directus Github repository</a>
