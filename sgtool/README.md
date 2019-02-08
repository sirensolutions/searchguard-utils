sgtool
======

You first need to create a config file `/etc/sgconfig` in the following format:

```
ES_BASE=/opt/elasticsearch
SG_CONF_CACHE=/opt/elasticsearch/sgconfig
SG_HOST=localhost
SG_PORT=9300
KEY_STORE=/opt/elasticsearch/client-certificates/sgadmin-keystore.jks
KEY_PASS=<password>
TRUST_STORE=/data/elasticsearch/config/truststore.jks
TRUST_PASS=<password>
```

If you have PEM/CRT files instead, use the following instead of KEY_STORE and TRUST_STORE:

```
KEY_FILE=/opt/elasticsearch/client-certificates/sgadmin.key
KEY_PASS=<password>
CERT_FILE=/opt/elasticsearch/client-certificates/sgadmin.crt
CA_FILE=/opt/elasticsearch/client-certificates/ca.crt
```

The location of this file can be overridden by setting the envar SGTOOL_CONF.

Beware that the SG_CONF_CACHE directory will have its contents overwritten by the `sgtool dump` command.

Usage
-----

If you have a running elasticsearch cluster with searchguard already configured, then you can update the searchguard configuration by, e.g.:

```
sgtool dump
nano $SG_CONF_CACHE/sg_roles_mapping  # your favourite editor
sgtool push rolesmapping
```

A full description of the commands available can be found by running `sgtool help`.
