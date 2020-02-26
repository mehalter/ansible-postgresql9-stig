# ansible-postgresql9-stig

This is a work in progress of an Ansible playbook that will audit and harden
PostgreSQL to the DoD STIG v1r6.

## Rules to Investigate Manually

| Severity | Vulid   | STIG-ID        | Note |
|----------|---------|----------------|------|
| CAT II   | V-72843 | PGS9-00-000200 | 
| CAT II   | V-72849 | PGS9-00-000500 | 
| CAT II   | V-72855 | PGS9-00-000710 | limit privleges to specific users/tasks |
| CAT II   | V-72859 | PGS9-00-000900 | authentication requirements |
| CAT II   | V-72865 | PGS9-00-001300 | permissions of roles |
| CAT II   | V-72885 | PGS9-00-002300 | logging |