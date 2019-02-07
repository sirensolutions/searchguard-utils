sgtool

You need to create a config file `/etc/sgconfig` in the following format:

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

The location of this file can be overridden by setting the envar SGTOOL_CONF
