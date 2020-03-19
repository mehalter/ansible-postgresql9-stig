# ansible-postgresql9-stig

This is a work in progress of an Ansible playbook that will audit and harden
PostgreSQL to the DoD STIG v1r6.

## Rules to Investigate Manually

| Severity | Vulid   | STIG-ID        | Note                                                             |
|----------|---------|----------------|------------------------------------------------------------------|
| CAT II   | V-72843 | PGS9-00-000200 | setup pgaudit                                                    |
| CAT I    | V-72845 | PGS9-00-000300 | security updates                                                 |
| CAT II   | V-72849 | PGS9-00-000500 | organization level authentication                                |
| CAT II   | V-72855 | PGS9-00-000710 | limit privleges to specific users/tasks                          |
| CAT II   | V-72859 | PGS9-00-000900 | authentication requirements                                      |
| CAT II   | V-72861 | PGS9-00-001100 | security labeling in transmission                                |
| CAT II   | V-72865 | PGS9-00-001300 | permissions of roles                                             |
| CAT II   | V-72867 | PGS9-00-001400 | users must be uniquely identifiable                              |
| CAT II   | V-72869 | PGS9-00-001700 | security labeling in storage                                     |
| CAT II   | V-73055 | PGS9-00-001800 | validity of data inputs                                          |
| CAT II   | V-72873 | PGS9-00-001900 | limit dynamic code execution                                     |
| CAT II   | V-72875 | PGS9-00-002000 | dynamic code execution must check inputs                         |
| CAT II   | V-72877 | PGS9-00-002100 | make sure there is enough audit space                            |
| CAT II   | V-72883 | PGS9-00-002200 | enforce access control policies                                  |
| CAT II   | V-72885 | PGS9-00-002300 | logging permissions (same as PGS9-00-000400)                     |
| CAT II   | V-72891 | PGS9-00-002600 | logging permissions (same as PGS9-00-000400)                     |
| CAT II   | V-72895 | PGS9-00-003000 | configure ssl (Appendix G)                                       |
| CAT II   | V-72897 | PGS9-00-003100 | make sure every object has an owner                              |
| CAT II   | V-72899 | PGS9-00-003200 | admin account must restrict access                               |
| CAT II   | V-72901 | PGS9-00-003300 | make sure no software is installed in the postgresql data folder |
| CAT II   | V-72903 | PGS9-00-003500 | set up pgaudit (Appendix B)                                      |
| CAT II   | V-72905 | PGS9-00-003600 | limit access to privileged functions                             |
| CAT II   | V-72907 | PGS9-00-003700 | set up pgaudit (Appendix B)                                      |
| CAT II   | V-72911 | PGS9-00-004000 | isolate security and non-security functions                      |
| CAT II   | V-72913 | PGS9-00-004100 | set up logging (Appendix C)                                      |
| CAT II   | V-72915 | PGS9-00-004200 | logging permissions (same as PGS9-00-000400)                     |
| CAT II   | V-72917 | PGS9-00-004300 | make sure old postgres installs are removed                      |
| CAT II   | V-72921 | PGS9-00-004500 | set up logging (Appendix C)                                      |
| CAT II   | V-72925 | PGS9-00-004700 | log connections (same as PGS9-00-004600)                         |
| CAT II   | V-72927 | PGS9-00-004800 | set up logging (Appendix C)                                      |
| CAT II   | V-72929 | PGS9-00-004900 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72931 | PGS9-00-005000 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72933 | PGS9-00-005100 | log connections (same as PGS9-00-004600)                         |
| CAT II   | V-72939 | PGS9-00-005200 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72941 | PGS9-00-005300 | set up logging (Appendix C)                                      |
| CAT II   | V-72949 | PGS9-00-005600 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72951 | PGS9-00-005700 | set up logging (Appendix C)                                      |
| CAT II   | V-72955 | PGS9-00-005900 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72957 | PGS9-00-006000 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72959 | PGS9-00-006100 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72961 | PGS9-00-006200 | log connections (set with PGS9-00-004600)                        |
| CAT II   | V-72963 | PGS9-00-006300 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72965 | PGS9-00-006400 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72969 | PGS9-00-006500 | set up logging (Appendix C)                                      |
| CAT II   | V-72971 | PGS9-00-006600 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72973 | PGS9-00-006700 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-72975 | PGS9-00-006800 | set up logging (Appendix C)                                      |
| CAT II   | V-72977 | PGS9-00-006900 | set up logging (Appendix C)                                      |
| CAT II   | V-72979 | PGS9-00-007000 | set up ssl (Appendix G)                                          |
| CAT II   | V-72981 | PGS9-00-007200 | set up ssl (Appendix G)                                          |
| CAT II   | V-72983 | PGS9-00-007400 | set up pgaudit (Appendix B)                                      |
| CAT II   | V-72985 | PGS9-00-007700 | set up logging (Appendix C)                                      |
| CAT II   | V-72987 | PGS9-00-007800 | set up logging (Appendix C)                                      |
| CAT I    | V-72989 | PGS9-00-008000 | enable FIPS                                                      |
| CAT II   | V-72991 | PGS9-00-008100 | set up ssl (Appendix G)                                          |
| CAT I    | V-72993 | PGS9-00-008200 | enable FIPS                                                      |
| CAT II   | V-72995 | PGS9-00-008300 | set up pgcrypto (Appendix E)                                     |
| CAT II   | V-72997 | PGS9-00-008400 | maintain appropriate permissions                                 |
| CAT II   | V-72999 | PGS9-00-008500 | separate admins and general users                                |
| CAT II   | V-73001 | PGS9-00-008600 | set up logging (Appendix C)                                      |
| CAT II   | V-73003 | PGS9-00-008700 | set up pgcrypto (Appendix E)                                     |
| CAT II   | V-73005 | PGS9-00-008800 | log connections (set with PGS9-00-004600)                        |
| CAT II   | V-73007 | PGS9-00-008900 | drop unused extensions                                           |
| CAT II   | V-73009 | PGS9-00-009100 | maintain access to external functions                            |
| CAT II   | V-73011 | PGS9-00-009200 | remove unused database components                                |
| CAT II   | V-73013 | PGS9-00-009400 | maintain organization level security                             |
| CAT II   | V-73017 | PGS9-00-009600 | separate admins and general users                                |
| CAT II   | V-73019 | PGS9-00-009700 | log connections (set with PGS9-00-004600)                        |
| CAT II   | V-73023 | PGS9-00-009900 | notify sys admin when audit space hits 75% capacity              |
| CAT II   | V-73025 | PGS9-00-010000 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-73027 | PGS9-00-010100 | postgresql must require reauthentication when necessary          |
| CAT I    | V-73029 | PGS9-00-010200 | make sure ssl keys are stored in a protected directory           |
| CAT II   | V-73031 | PGS9-00-010300 | set up ssl (Appendix G)                                          |
| CAT II   | V-73033 | PGS9-00-010400 | log connections (set with PGS9-00-004600)                        |
| CAT II   | V-73035 | PGS9-00-010500 | set up pgcrypto (Appendix E)                                     |
| CAT II   | V-73039 | PGS9-00-010700 | prevent unauthorized audit access                                |
| CAT II   | V-73041 | PGS9-00-011100 | log connections (set with PGS9-00-004600)                        |
| CAT II   | V-73043 | PGS9-00-011200 | logging permissions (same as PGS9-00-000400)                     |
| CAT II   | V-73045 | PGS9-00-011300 | off-load audit data (same as PGS9-00-003800)                     |
| CAT II   | V-73047 | PGS9-00-011400 | set up ssl (Appendix G)                                          |
| CAT II   | V-73049 | PGS9-00-011500 | require unique authentication for all roles                      |
| CAT II   | V-73051 | PGS9-00-011600 | automatically disconnect users after timeout (Appendix A)        |
| CAT I    | V-73053 | PGS9-00-011700 | maintain appropriate permissions                                 |
| CAT II   | V-73055 | PGS9-00-011800 | set up ssl (Appendix G)                                          |
| CAT II   | V-73057 | PGS9-00-011900 | protect data during data transfer                                |
| CAT II   | V-73059 | PGS9-00-012000 | maintain appropriate permissions                                 |
| CAT II   | V-73061 | PGS9-00-012200 | logging permissions (same as PGS9-00-000400)                     |
| CAT I    | V-73063 | PGS9-00-012300 | set up ssl (Appendix G)                                          |
| CAT II   | V-73065 | PGS9-00-012500 | pgaudit log (set with PGS9-00-004400)                            |
| CAT II   | V-73067 | PGS9-00-012600 | log connections (set with PGS9-00-004600)                        |
| CAT II   | V-73069 | PGS9-00-012700 | log connections (set with PGS9-00-004600)                        |
| CAT I    | V-73071 | PGS9-00-012800 | enable FIPS                                                      |
