# Configuring PostgreSQL for Remote Access

This document outlines the steps to install and configure PostgreSQL, create a new database, and set it up for remote access.

## Step 1: Update the System

Ensure your system's package list is updated:

```bash
sudo apt update
```

## Step 2: Install PostgreSQL

Install PostgreSQL from the system's package manager:

```bash
apt install postgresql
```
## Step 3: Access PostgreSQL Command Line

To interact with PostgreSQL, switch to the `postgres` user and open the PostgreSQL command line:

```bash
sudo -u postgres psql
```

### List Existing Databases

To list all databases, use the following command:

```sql
\l
```

### Set the Password for the `postgres` User

To set a password for the `postgres` user, enter the following command within the PostgreSQL command line:

```sql
\password postgres
```

## Step 4: Create a New Database

Create a new database named `test`:

```sql
CREATE DATABASE test;
```

### Connect to the New Database

Connect to the `test` database:

```sql
\c test
```

## Step 5: Configure PostgreSQL for Remote Access

Navigate to the PostgreSQL configuration directory:

```bash
cd /etc/postgresql/16/main
```

### Configure `postgresql.conf`

Edit the `postgresql.conf` file to allow connections from all IP addresses:

```bash
nano postgresql.conf
```

Uncomment and set `listen_addresses` to `'*'`:

```text
listen_addresses = '*'
```

### Configure `pg_hba.conf`

Edit the `pg_hba.conf` file to allow remote connections with MD5 password authentication:

```bash
nano pg_hba.conf
```

Add the following line to grant access from any IP address:

```text
host all all 0.0.0.0/0 md5
```

## Step 6: Restart PostgreSQL

Restart PostgreSQL to apply the configuration changes:

```bash
sudo systemctl restart postgresql
```

## Step 7: Verify PostgreSQL is Listening on Port 5432

To confirm PostgreSQL is listening on the default port (5432), run the following command:

```bash
ss -nlt | grep 5432
```

If everything is configured correctly, you should see output indicating that PostgreSQL is listening on port 5432.

## Conclusion

You've successfully configured PostgreSQL to allow remote access and created a new database. If you encounter any issues, ensure that your firewall rules allow traffic on port 5432 and that PostgreSQL is correctly set up to accept remote connections.
