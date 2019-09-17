# httpd-mysql-server docker

Docker configuration for Hippo development with `httpd (apache2)` and `mysql`
pre-configured. It also includes a `install-tomcat.sh` shell script to install
tomcat with the required configuration from `cargo` the Hippo project with
tomcat and IntelliJ.  See `./install-tomcat.sh -h` for more information and the
usage of the script.

## Preparations

1. `git clone
   https://gitlab.issc.leidenuniv.nl/thijssesc/httpd-mysql-server-docker.git`
2. Install [`docker`](https://docs.docker.com/) and
   [`docker-compose`](https://docs.docker.com/compose/)

## Initialize

1. `cd httpd-mysql-server-docker`
2. `docker-compose up`

Or run in daemon mode:
 - `docker-compose up -d`

## Configurations

The following services are loaded by the `docker-compose.yml` configuration.

### httpd

The `httpd` service is loaded with the virtual hosts of all the sites of
Universiteitleiden pre-configured, these configurations are stored in the
`./conf/vhosts` folder of this repository. The logs files for the virtual hosts
will be stored in `/usr/local/apache2/logs` of the file system of the
container. The rest of the `httpd` configuration is stored in the
`./conf/httpd.conf` file.

### mysql-server

The `mysql-server` service is loaded with the following `root` password:
`toor`. Also loaded is a database for development named `universiteitleiden`.
And to connect to the server the user `hippolocal` has been created, the
password for this user is also `hippolocal`. Lastly in the root of the file
system of the container there is a script to clean the `universiteitleiden`
database, named `drop_universiteitleiden.sql`. To edit the usernames and
passwords you can edit the `docker-compose.yml` file in the root of this
repository.

Some example commands you can use in the container:

```bash
 $ mysql -u root -ptoor -Duniversiteitleiden
 $ mysql -u hippolocal -phippolocal -Duniversiteitleiden
 $ mysql -u root -ptoor < drop_universiteitleiden.sql
```

## License

MIT License
