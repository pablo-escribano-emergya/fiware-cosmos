#Custom Http PEP proxy for Cosmos
cosmos-proxy is a custom Http proxy acting as a Policy Enforcement Point (PEP). This means:

* cosmos-proxy is deployed before any Cosmos Http service aimed to be protected.
* cosmos-proxy is designed to authenticate and authorize the requests originally sent to the Cosmos Http service.

Authentication and authorization are based on [OAuth2](http://oauth.net/2/) tokens generated by any trusted third party (TTP; in the case of FIWARE, this is the [Keyrock Identity Manager](http://catalogue.fiware.org/enablers/identity-management-keyrock)) that must be attached to the Http requests as `X-Auth-Token` headers. Once received:

1. The token is used to get the user ID from the TTP.
2. The ID is checked against the Cosmos ID within the resource aimed to be used (any Cosmos resource is a URI containing the HDFS user space which is based in the TTP ID, e.g. `hdfs:///user/ID`).
3. If matching both TTP and Cosmos IDs then the user is authorized to use the Cosmos resource.

Further information can be found in the documentation at [fiware-cosmos.readthedocs.io](http://fiware-cosmos.readthedocs.io/en/latest/).
