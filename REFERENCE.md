# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

* [`geoip`](#geoip): The geoip module installs tools and databases GeoIP resolution from MaxMind.  You may replace userid and licensekey with your subscription an
* [`geoip::config`](#geoipconfig): This class implements the configuration stage of this module. It should not be called directly.  Configuration file defined with `geoip::conf
* [`geoip::config::ge311`](#geoipconfigge311): This class is creating a GeoIP.conf configuration file for geoipupdate versions >= 3.1.1.
* [`geoip::config::lt311`](#geoipconfiglt311): This class is creating a GeoIP.conf configuration file for geoipupdate versions < 3.1.1.
* [`geoip::install`](#geoipinstall): This class implements the installation stage of the module. It should not be called directly.  This will install or remove software packages 
* [`geoip::service`](#geoipservice): This class implements the service control stage of the module. It should not be called directly.  If `geoip::manage_service` enabled, an upda
* [`geoip::systemd::service`](#geoipsystemdservice): Controling SystemD service unit for update
* [`geoip::systemd::timer`](#geoipsystemdtimer): Controll the SystemD Timer unit

## Classes

### <a name="geoip"></a>`geoip`

The geoip module installs tools and databases GeoIP resolution from MaxMind.

You may replace userid and licensekey with your subscription and
add the productids you want to sync. Leaving these options on default
will allow you to sync all free available databases. With
database_directory the destination directory of the databases can be
set, protocol, proxy* and *_verification may only be needed in the
case your host needs some specific proxy settings to get to the
internet.

#### Examples

##### hiera

```puppet
geoip::config:
  userid: '999999'
  licensekey: '000000000000'
  productids:
    - GeoLite2-City
    - GeoLite2-Country
  database_directory:
  protocol:
  proxy:
  proxy_user_password:
  skip_hostname_verification:
  skip_peer_verification:
```

#### Parameters

The following parameters are available in the `geoip` class:

* [`ensure`](#ensure)
* [`packages`](#packages)
* [`package_ensure`](#package_ensure)
* [`config_path`](#config_path)
* [`config_version`](#config_version)
* [`config`](#config)
* [`manage_service`](#manage_service)
* [`service_user`](#service_user)
* [`service_group`](#service_group)
* [`update_path`](#update_path)
* [`service_name`](#service_name)
* [`update_timers`](#update_timers)
* [`update_scatter`](#update_scatter)

##### <a name="ensure"></a>`ensure`

Data type: `Enum['present', 'absent']`

install or remove settings done by this module

Default value: `'present'`

##### <a name="packages"></a>`packages`

Data type: `Array[String]`

the software packages containing the tools to be installed

Default value: `['mmdb-bin', 'geoipupdate']`

##### <a name="package_ensure"></a>`package_ensure`

Data type: `String`

which version of the packages should be ensured

Default value: `'latest'`

##### <a name="config_path"></a>`config_path`

Data type: `Stdlib::Absolutepath`

path to the configuration and license file

Default value: `'/etc/GeoIP.conf'`

##### <a name="config_version"></a>`config_version`

Data type: `Enum['lt311','ge311']`

the config version to use for geoipupdate

Default value: `'lt311'`

##### <a name="config"></a>`config`

Data type: `Hash`

hash of configuration options

Default value: `{}`

##### <a name="manage_service"></a>`manage_service`

Data type: `Boolean`

whether to manage database updating service

Default value: ``true``

##### <a name="service_user"></a>`service_user`

Data type: `String`

effective user the update service should run

Default value: `'root'`

##### <a name="service_group"></a>`service_group`

Data type: `String`

effective group the update service should run

Default value: `'root'`

##### <a name="update_path"></a>`update_path`

Data type: `Stdlib::Absolutepath`

path to the geoipupdate tool, used by update service

Default value: `'/usr/bin/geoipupdate'`

##### <a name="service_name"></a>`service_name`

Data type: `String`

name of the update service

Default value: `'geoip_update'`

##### <a name="update_timers"></a>`update_timers`

Data type: `Array[String]`

wallclock timers when the update service should be triggered (for syntax see [systemd.time(7)#Parsing Timestamps](https://www.freedesktop.org/software/systemd/man/systemd.time.html#Parsing%20Timestamps))

Default value: `[]`

##### <a name="update_scatter"></a>`update_scatter`

Data type: `Integer`

a time window in seconds of randomized, host specific delay of the update trigger (see [systemd.timer(5)#AccuracySec](https://www.freedesktop.org/software/systemd/man/systemd.timer.html#AccuracySec=))

Default value: `1800`

### <a name="geoipconfig"></a>`geoip::config`

This class implements the configuration stage of this module. It should not be called directly.

Configuration file defined with `geoip::config_path` will be created using parameter from
`geoip::config`.

### <a name="geoipconfigge311"></a>`geoip::config::ge311`

This class is creating a GeoIP.conf configuration file for geoipupdate
versions >= 3.1.1.

#### Parameters

The following parameters are available in the `geoip::config::ge311` class:

* [`accountid`](#accountid)
* [`licensekey`](#licensekey)
* [`editionids`](#editionids)
* [`database_directory`](#database_directory)
* [`host`](#host)
* [`proxy`](#proxy)
* [`proxy_user_password`](#proxy_user_password)
* [`preserve_file_times`](#preserve_file_times)
* [`lock_file`](#lock_file)

##### <a name="accountid"></a>`accountid`

Data type: `String`

AccountID of your MaxMind subscription

##### <a name="licensekey"></a>`licensekey`

Data type: `String`

The license key issued by MaxMind to be used

##### <a name="editionids"></a>`editionids`

Data type: `Array[String]`

Edition IDs (formerly known as ProductIDs) to download

Default value: `['GeoLite2-ASN','GeoLite2-City','GeoLite2-Country']`

##### <a name="database_directory"></a>`database_directory`

Data type: `Optional[Stdlib::Absolutepath]`

Path where the database file to be stored

Default value: ``undef``

##### <a name="host"></a>`host`

Data type: `Optional[String]`

The update server to use

Default value: ``undef``

##### <a name="proxy"></a>`proxy`

Data type: `Optional[String]`

URL or IP:Port of the proxy to use when accessing the update server

Default value: ``undef``

##### <a name="proxy_user_password"></a>`proxy_user_password`

Data type: `Optional[String]`

Credentials as username:password for proxy authentication

Default value: ``undef``

##### <a name="preserve_file_times"></a>`preserve_file_times`

Data type: `Optional[Boolean]`

Whether to preserve modification times of files downloaded from the server

Default value: ``undef``

##### <a name="lock_file"></a>`lock_file`

Data type: `Optional[String]`

The lock file to use

Default value: ``undef``

### <a name="geoipconfiglt311"></a>`geoip::config::lt311`

This class is creating a GeoIP.conf configuration file for geoipupdate
versions < 3.1.1.

#### Parameters

The following parameters are available in the `geoip::config::lt311` class:

* [`userid`](#userid)
* [`licensekey`](#licensekey)
* [`productids`](#productids)
* [`database_directory`](#database_directory)
* [`protocol`](#protocol)
* [`proxy`](#proxy)
* [`proxy_user_password`](#proxy_user_password)
* [`skip_hostname_verification`](#skip_hostname_verification)
* [`skip_peer_verification`](#skip_peer_verification)

##### <a name="userid"></a>`userid`

Data type: `String`

UserID of your MaxMind subscription

##### <a name="licensekey"></a>`licensekey`

Data type: `String`

The license key issued by MaxMind to be used

##### <a name="productids"></a>`productids`

Data type: `Array[String]`

Product IDs to download

Default value: `['GeoLite2-ASN','GeoLite2-City','GeoLite2-Country']`

##### <a name="database_directory"></a>`database_directory`

Data type: `Optional[Stdlib::Absolutepath]`

Path where the database file to be stored

Default value: ``undef``

##### <a name="protocol"></a>`protocol`

Data type: `Optional[Enum['http','https']]`

Protocol to be used when accessing the update server

Default value: ``undef``

##### <a name="proxy"></a>`proxy`

Data type: `Optional[String]`

URL or IP:Port of the proxy to use when accessing the update server

Default value: ``undef``

##### <a name="proxy_user_password"></a>`proxy_user_password`

Data type: `Optional[String]`

Credentials as username:password for proxy authentication

Default value: ``undef``

##### <a name="skip_hostname_verification"></a>`skip_hostname_verification`

Data type: `Optional[Boolean]`

Whether to skip host name verification on HTTPS connections

Default value: ``undef``

##### <a name="skip_peer_verification"></a>`skip_peer_verification`

Data type: `Optional[Boolean]`

Whether to skip peer verification on HTTPS connections

Default value: ``undef``

### <a name="geoipinstall"></a>`geoip::install`

This class implements the installation stage of the module. It should not be called directly.

This will install or remove software packages listed in `geoip::packages`. When installing
package versions will be ensured as `geoip::package_ensure`.

### <a name="geoipservice"></a>`geoip::service`

This class implements the service control stage of the module. It should not be called directly.

If `geoip::manage_service` enabled, an update service will be created fitting to the service
provider available on the node. Service name is configured with `geoip::service_name`.

### <a name="geoipsystemdservice"></a>`geoip::systemd::service`

This class is creating a serivce unit for SystemD to update GeoIP databases.
The service is running the geoipupdate ones and retry as configured.

#### Parameters

The following parameters are available in the `geoip::systemd::service` class:

* [`restart`](#restart)
* [`restart_sec`](#restart_sec)

##### <a name="restart"></a>`restart`

Data type: `String`

update service retry behaviour

Default value: `'on-failure'`

##### <a name="restart_sec"></a>`restart_sec`

Data type: `String`

time to wait before retry

Default value: `'5min'`

### <a name="geoipsystemdtimer"></a>`geoip::systemd::timer`

This class will create a SystemD timer unit triggering the update service on
each wallclock timer.
