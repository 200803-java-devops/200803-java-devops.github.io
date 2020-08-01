# PostgreSQL

## Local install
### Windows
- Chocolatey: `choco install postgresql`
- [Official Download](https://www.postgresql.org/download/)

## Cloud
### AWS
Create a free-tier RDS instance in the cloud on Amazon Web Services.
1. Sign up for an account on aws.amazon.com
2. Create an RDS ([tutorial](https://aws.amazon.com/getting-started/tutorials/create-connect-postgresql-db/))

### ElephantSQL/Heroku
Alternatively, use an alternative cloud service provider like [ElephantSQL](https://www.elephantsql.com/docs/index.html) or [Heroku](https://www.heroku.com/postgres).

## Docker
Docker is a containerization tool written in Go to create lightweight containers running isolated file systems and processes. Docker can be run on non-Enterprise Windows using Docker toolbox (soon with WSL2 on Windows 10 Home), or on a Cloud EC2 linux instance.

### Installation
To install the latest version however, it is recommended to follow the official [Docker Installation](https://docs.docker.com/engine/install/centos/) documentation:

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
```

Run `docker`'s hello-world container to verify installation:
>sudo docker run hello-world

### Permissions
Docker requires super user permissions and must be run with the `sudo` command by default. This can be bypassed for convenience by adding your user to the docker unix group:
>sudo usermod -aG docker <USER>

Log out, then log back in to see the changes. If successful, the following command will now work:
>docker run hello-world

### Example: PostgreSQL Server
To run a simple Postgres server instance:
>docker run -p [port]:5432 postgres

Where [port] is your choice of port. A common port is 5432, a default for many Postgres databases:
>docker run -p 5432:5432 postgres

To run a database as a background process, use the `-d` switch:
>docker run -d -p 5432:5432 postgres

It's a good idea to label a database with the `--name` switch:
>docker run -d --name my_postgres -p 5432:5432 postgres

To see running containers, use:
>docker ps

To stop a container, run:
>docker stop <CONTAINER-NAME-OR-ID>

### Running PostgreSQL from a Dockerfile
To create a custom postgres database, create a file named `Dockerfile`:
```Dockerfile
FROM postgres:10
ENV POSTGRES_USER hello-postgres
ENV POSTGRES_PASSWORD hello-postgres
ADD init.sql /docker-entrypoint-initdb.d
EXPOSE 5432
```

Where init.sql is an optional `.sql` script file in the same directory as your Dockerfile. Use `ENV` to set the username and password as needed. Both `ENV` lines can be omitted, causing the username to default to `postgres` and no password required.

To build an image from the Dockerfile:
>docker build -t demo-postgres .

Where `demo-postgres` is the name you wish to give this image. Then to run the build:
>docker run -p 5432:5432 -d demo-postgres

Remember to expose the ports and use any desired flags.

### Connecting to a Docker PostgreSQL database with `psql`
With your Docker postgres image built and a container running, use `docker exec` to run the `psql` tool on the running container:
>docker exec -it demo-postgres psql -U hello-postgres

Enter your Postgres username after `-U` (`postgres` by default if no `POSTGRES_USER` was set) and enter your password when prompted.

## Resources
### Articles
- [The SQL Standard](https://blog.ansi.org/2018/10/sql-standard-iso-iec-9075-2016-ansi-x3-135/)
- [Life of a SQL query](https://numeracy.co/blog/life-of-a-sql-query)
- [How does a relational database execute SQL statements and prepared statements](https://vladmihalcea.com/relational-database-sql-prepared-statements/)
- [A beginner’s guide to database table relationships](https://vladmihalcea.com/database-table-relationships/)
- [A beginner’s guide to ACID and database transactions](https://vladmihalcea.com/a-beginners-guide-to-acid-and-database-transactions/)
- [A Simple Guide to Five Normal Forms](http://www.bkent.net/Doc/simple5.htm)
- [Say NO to Venn Diagrams When Explaining JOINs](https://blog.jooq.org/2016/07/05/say-no-to-venn-diagrams-when-explaining-joins/)

### Books
- [Wikibooks - SQL](https://en.wikibooks.org/wiki/Structured_Query_Language)
- [Wikibooks - PostgreSQL](https://en.wikibooks.org/wiki/PostgreSQL)
- [Wikibooks - Relational Database Design](https://en.wikibooks.org/wiki/Relational_Database_Design)
- [The Internals of PostgreSQL](http://www.interdb.jp/pg/)
- [Database Design](https://opentextbc.ca/dbdesign01/)

### Documentation
- [SQL92 Specification](http://www.contrib.andrew.cmu.edu/~shadow/sql/sql1992.txt)
- [PostgreSQL 12 Documentation](https://www.postgresql.org/docs/12/index.html)
- [PostgreSQL SQL Command Reference](https://www.postgresql.org/docs/12/sql-commands.html)
- [psql](https://www.postgresql.org/docs/12/app-psql.html)
- [PostgreSQL on Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_PostgreSQL.html)

### Tutorials
- [Example of a Step by Step Normalization](https://en.wikipedia.org/wiki/Database_normalization#Example_of_a_step_by_step_normalization)
- [Description of the Database Normalization Basics](https://docs.microsoft.com/en-us/office/troubleshoot/access/database-normalization-description)
- [3 Normal Forms Database Tutorial](http://phlonx.com/resources/nf3/)
- [SQL Bolt](https://sqlbolt.com/)
- [SQLZOO](https://sqlzoo.net/wiki/SQL_Tutorial)
- [postgresql.org Tutorial](https://www.postgresql.org/docs/12/tutorial.html)
- [Postgres Guide](http://www.postgresguide.com/)
- [PostgreSQL Exercises](https://pgexercises.com/)
- [Developer's Guide to PostgreSQL on Linux: psql shell](https://thecodinginterface.com/blog/postgresql-psql-shell/)
- [Setting Up for Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SettingUp.html)
- [Creating Postgres RDS and Connecting Using pgAdmin](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)