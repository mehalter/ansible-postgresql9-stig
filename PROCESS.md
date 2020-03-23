---
title: STIG Postgresql 12
date: March 23, 2020
author: Micah Halter
---

# Set Up Environment Variables

Find the `postgresql` data folder and version

```
$~ sudo su - postgres
$~ psql -c "SHOW data_directory"
$~ psql -c "SHOW server_version"
```

As a DB administrator, add the following lines to `~/.bashrc` (Updated for your `postgresql` installation

```
export PATH="/usr/pgsql-12/bin:$PATH"
export PGDATA='/var/lib/pgsql/12/data'
export PGVER=12
```

# Set up pgaudit

Install `pgaudit` extension with

```
$~ sudo yum install pgaudit14_12
```

Change `shared_preload_libraries` line in `${PGDATA}/postgresql.conf` to

```
shared_preload_libraries = 'pgaudit'
```

Add `pgaudit` configuration options to the bottom of `${PGDATA}/postgresql.conf`

```
#------------------------------------------------------------------------------
# PGAUDIT OPTIONS
#------------------------------------------------------------------------------

# Enable catalog logging - default is 'on'
pgaudit.log_catalog='on'

# Specify the verbosity of log information (INFO, NOTICE, LOG, WARNING, DEBUG)
pgaudit.log_level='log'

# Log the parameters being passed
pgaudit.log_parameter='on'

# Log each relation (TABLE, VIEW, etc.) mentioned in a SELECT or DML statement
pgaudit.log_relation='off'

# For every statement and substatement, log the statement and parameters
pgaudit.log_statement_once='off'

# Define the master role to use for object logging
# pgaudit.role=''
# Choose the statements to log:
# READ - SELECT, COPY
# WRITE - INSERT, UPDATE, DELETE, TRUNCATE, COPY
# FUNCTION - Function Calls and DO Blocks
# ROLE - GRANT, REVOKE, CREATE/ALTER/DROP ROLE
# DDL - All DDL not included in ROLE
# MISC - DISCARD, FETCH, CHECKPOINT, VACUUM
pgaudit.log='ddl,role,write,read'
```

# Set up Logging

Verify the following logging settings in `${PGDATA}/postgresql.conf`

```
log_destination = 'syslog'
logging_collector = on
log_directory = 'log'
log_filename = 'postgresql-%a.log'
log_file_mode = 0600
log_truncate_on_rotation = on
log_rotation_age = 1d
log_rotation_size = 0

syslog_facility = 'LOCAL0'
syslog_ident = 'postgres'

log_checkpoints = on
log_connections = on
log_disconnections = on
log_duration = off
log_error_verbosity = default
log_hostname = on
log_line_prefix = '%m %u %d: '
log_lock_waits = on
log_statement = 'none'
log_timezone = 'America/New_York'

client_min_messages = notice
log_min_messages = warning
log_min_error_statement = error
log_min_duration_statement = -1
```

Add the following rule to `/etc/rsyslog.conf`

```
local0.*    /var/log/postgresql
```

# Install pgcrypto

Run

```
$~ sudo su - postgres
$~ psql -c "CREATE EXTENSION pgcrypto"
```

# Setup SSL

COMING SOON...

# Run the ansible

Set the defaults in `roles/disa-v1r6/defaults/main.yml`

```
$~ sudo ansible-playbook playbook.yml
```
