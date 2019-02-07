How to use the CSR tools
========================

Let us assume that you have unpacked these tools into the directory
`/etc/elasticsearch/certs`.

Files:

* gencsr
* genadmincsr
* importcert
* importadmincert

Make sure to set the envar KEYSTORE_PASSWORD to something nontrivial:

```
export KEYSTORE_PASSWORD="correct horse battery staple"
```


To create a CSR for a fresh server certificate
----------------------------------------------

```
cd /etc/elasticsearch/certs
./gencsr
```

This will generate a fresh CSR that you can send to your CA with instructions
to make a certificate valid for both server AND client use (if you are using
a fake CA, then read `../fake-ca/README.md` and follow the instructions there).

Your CA should return a certificate in a usable format, e.g. PEM.


To create a CSR for a fresh sgadmin client certificate
------------------------------------------------------

```
cd /etc/elasticsearch/certs
./genadmincsr
```

This will do the same, but for sgadmin rather than the server. You should send
this to your CA with instructions to make a TLS client certificate.

Your CA should return a certificate in a usable format, e.g. PEM.

If you need to import PEM format certs into a keystore/truststore pair, run:

```
export TRUSTSTORE_PASSWORD="correct horse battery staple"
./importcert
```

This will attempt to find the host certificate automatically in the current
directory and import it to an existing pkcs12 keystore in the format created by
`gencsr`. It will also load the CA cert into a truststore.

To load the sgadmin cert, run:

```
./importadmincert
```

This will load the sgadmin cert into the existing pkcs12 keystore for sgadmin.

Advanced options
================

The tools attempt to automatically detect several parameters such as the host
name, primary IP address, X509 DN etc. These assumed values are printed on
STDOUT during normal operation, and can be overridden by setting various
environment variables:

* HOST_NAME - the host name to use in the server certificate (gencsr)
* HOST_IP   - the primary IP address to use in the server certificate (gencsr)
* HOST_DN   - the X509 DN to use in the server certificate (gencsr)
* SGADMIN_DN - the X509 DN to use in the admin client certificate (genadmincsr)
