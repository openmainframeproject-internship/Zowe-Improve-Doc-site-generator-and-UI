# Configuring Zowe certificates 

Zowe uses a certificate to encrypt data for communication across secure sockets. An instance of Zowe references a USS directory referred to as a KEYTORE_DIRECTORY which contains information about where the certificate is located.  More than one instance of Zowe can share the same KEYSTORE_DIRECTORY, which is defined by the variable `KEYSTORE_DIRECTORY` in the `instance.env` file. For more information, see [Creating and configuring the Zowe instance directory](./configure-instance-directory.md).  

The `KEYSTORE_DIRECTORY` is created by running the script `<ROOT_DIR>/bin/zowe-setup-certificates.sh`.  This script has a number of input parameters that are specified in the configuration file `<ROOT_DIR>/bin/zowe-setup-certificates.env`.  The `zowe-setup-certificates.env` file should be customized based on security rules and practices for the z/OS environment.  Once the script has been successfully executed, it does not need to be re-run as the `KEYSTORE_DIRECTORY` is used at runtime.  A `KEYSTORE_DIRECTORY` can be used by more than one instance of Zowe.

The file `zowe-certificates.env` created in the `KEYSTORE_DIRECTORY` is executed each time a Zowe instance is started and will set a number of USS shell configuration variables. For more information, see [Creating and configuring the Zowe instance directory](../user-guide/configure-instance-directory.md#keystore-configuration).	

Learn more about the key concepts of Zowe certificates in the following sections.
 
## Northbound Certificate

The Zowe certificate is used by the API Mediation Layer on its northbound edge when identifying itself and encrypting `https://` traffic to web browsers or REST client applications.  If the Zowe Command Line Interface (CLI) has been configured to use the Zowe API Mediation Layer then the CLI is a client of the Zowe certificate. For more information, see [Using the Zowe Command Line Interface, Integrating with the API Mediation Layer](./cli-usingcli.md#integrating-with-api-mediation-layer).

## Southbound Certificate

As well as being a server, Zowe itself is a client to services on the southbound edge of its API Mediation Layer that it communicates to over secure sockets.  These southbound services use certificates to encrypt their data, and Zowe uses a trust store to store its relationship to these certificates.  The southbound services that are started by Zowe itself and run as address spaces under its `ZWESVSTC` started task (such as the API discovery service, the explorer JES REST API server) re-use the same Zowe certificate used by the API Mediation Layer on its northbound client edge.  

## Trust store

As well as Zowe using its certificates intra-address space, to encrypt messages between its servers, Zowe uses external services on z/OS (such as z/OSMF or Zowe conformant extensions that have registered themselves with the API Mediation Layer).  These services will present their own certificate to the API Mediation Layer, in which case the trust store is used to capture the relationship between Zowe's southbound edge and these external certificates.  

If you wish to disable the trust store validation of southbound certificates, you can set the value `VERIFY_CERTIFICATES=true` to `false` in the `zowe-setup-certificates.env` file in the `KEYSTORE_DIRECTORY`.  A scenario when this is recommended is if certificate being presented to the API Mediation Layer is self-signed (that is, from an unknown certificate authority).  For example, the z/OSMF certificate may be self-signed in which case the Zowe API Mediation Layer will not recognize the signing authority.  

## Certificates in the Zowe architecture

The [Zowe architecture diagram](../getting-started/zowe-architecture.md) shows the Zowe API Mediation Layer positioned on the client-server boundary between applications such as web browsers or the Zowe CLI accessing z/OS services.  The following diagram is a section of the architecture annotated to describe the role of certificates and trust stores.  

<img src={require("../images/common/zowe-ssl.png").default} alt="Zowe SSL" width="700px"/> 

The lines shown in bold red are communication over a TCP/IP connection that is encrypted with the Zowe certificate.  
- On the northbound edge of the API gateway, the certificate is used between client applications such as web browsers, Zowe CLI, or any other application wishing to access Zowe's REST APIs.  
- On the southbound edge of the API Gateway, there are a number of Zowe micro services providing HTML GUIs for the Zowe desktop or REST APIs for the API Catalog.  These also use the Zowe certificate for data encryption.

The lines in bold green are external certificates for servers that are not managed by Zowe, such as z/OSMF itself or any Zowe conformant REST API or App Framework servers that are registered with the API Mediation Layer.  For the API Mediation Layer to be able to accept these certificates, they either need to be signed by a recognized certificate authority, or else the API Mediation Layer needs to be configured to accept unverified certificates.  Even if the API Mediation Layer is configured to accept certificates signed by unverified CAs on its southbound edge, client applications on the northbound edge of the API gateway will be presented with the Zowe certificate.  

## Keystore versus key ring

Zowe supports certificates that are stored in a USS directory **Java KeyStore** format.  

Beginning with release 1.15, Zowe is including the ability to work with certificates held in a **z/OS Keyring**.  Support for Keyring certificates is currently incomplete and being provided as a beta technical preview for early preview by customers.  If you have any feedback using keyrings please create an issue in the [zowe-install-packaging repo](https://github.com/zowe/zowe-install-packaging/issues).  It is expected that in a future release keyring support will be made available as a fully supported feature.  

<!--
Zowe supports certificates that are stored either in a USS directory **Java KeyStore** format or else held in a **z/OS Keyring**.  z/OS keystore are the preferred choice for storing certificates where system programmers are already familiar with their operation and usage.  The user ID setting up a keystore and connecting it with certificates requires elevated permissions, and in scenarios where you need to create a Zowe sandbox environment or for testing purposes and your TSO user ID doesn't have authority to manipulate key rings, USS keystores are a good alternative.  
-->

If you are using a USS keystore, then the script `zowe-setup-certificates.env` is the only configuration step required.  This is described in detail in [Configuring Zowe certificates in a USS KeyStore](./configure-certificates-keystore.md).

If you are using a key ring, the sample JCL member `ZWEKRING` provided in the PDS library `SZWESAMP` contains the security commands to create a key ring and manage its associated certificates. This is described in [Configuring Zowe certificates in a key ring](./configure-certificates-keyring.md).  

For both scenarios, where the certificate is held in a USS Java Keystore or a z/OS key ring, the USS `KEYSTORE_DIRECTORY` is still required which is created with the script `zowe-setup-certificates.sh`.  

