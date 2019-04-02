<!--

NOTE:
A new issue should be about a bug verified with a minimized example or about a new feature request.
New "bug" or "feature" reports not satisfying these requirement will be closed as "invalid".

Questions should go to the mailinglist at:  
mod_auth_openidc@googlegroups.com
The corresponding forum/archive is at:  
https://groups.google.com/forum/#!forum/mod_auth_openidc

-->

###### Environment 
PROD

- mod_auth_openidc version - 2.3.10
- Apache version - 2.4.9
- platform/distro - Linux

###### Expected behaviour
Access tokens will not be truncated

###### Actual behaviour
Access tokens are getting truncated when received by Apache.
I have a group of people who has multiple group memberships (I am getting them part of the OIDC scope for the user). When there are large number of groups a user is part of, the full access_token is not received by Apache and the browser shows 431 error.
Apache standard directives LimitRequestFieldSize did not help.


###### Minimized example
*Minimal, complete configuration that reproduces the behavior. Use the mailing list or get commercial support to discuss your own (full) setup.*

OIDCCryptoPassphrase somethingelse
    OIDCProviderMetadataURL https://ssotest.ad.corp.com/.well-known/openid-configuration
    OIDCClientID cie
    OIDCClientSecret somethingsomething
    OIDCRedirectURI https://cd02-1.searchcie.cas.ad.mvwcorp.com/redirect_uri
    OIDCCookiePath "/"
    OIDCCookieDomain ".cas.ad.mvwcorp.com"
    OIDCCacheType memcache
    OIDCMemCacheServers "mco11qm00lappc1 mco11qm00lappc2"
        OIDCCookie "mod_oidc_cd02"
    # maps the prefered_username claim to the REMOTE_USER environment variable
    OIDCRemoteUserClaim preferred_username
    OIDCScope "openid groups"
    OIDCStateMaxNumberOfCookies 1 true
        OIDCUnAuthAction 401

###### Configuration and Apache server log files
*Config and logs for the minimized example, possibly provided as attachments.*

