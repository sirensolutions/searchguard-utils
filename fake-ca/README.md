How to set up the fake CA tools
===============================

Let us assume that you have unpacked these tools into the directory `~/fake-ca`

Files:

* genfakeca
* fakecasign

First, make sure that CA_CONFIG points to a valid openssl CA configuration file:

```
export CA_CONFIG=./ca.conf
```

Also make sure to set CA_PASSWORD to something nontrivial:

```
export CA_PASSWORD="correct horse battery staple"
```

Now change into the unpack directory and make the CA:

```
cd ~/fake-ca
./genfakeca
```

It will ask you some questions. Since this is a fake CA, the answers are not
crucial. Now you have a CA.


How to sign a CSR or CSRs
=========================

With CA_CONFIG and CA_PASSWORD set as above, change into the `~/fake-ca`
directory, and run:

```
./fakecasign $FILENAME
```

This will generate a server certificate for the CSR given on the command line.
You can specify multiple files in one go:

```
./fakecasign *.csr
```

Certificates will be created in the current directory with the extension `.crt`
