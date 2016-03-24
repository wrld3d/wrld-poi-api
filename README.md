![eeGeo](images/pois.jpg)

eeGeo POI REST API v1.0
==================

This document describes version 1.0 of the eeGeo POI REST API for submitting and managing custom Points of Interest. The POI API is primarily intended for use with [eegeo-example-app](http://github.com/eegeo/eegeo-example-app).

---

## Quick Start

1. Obtain a Developer Authentication Token by signing up at [https://www.eegeo.com/developers/](https://www.eegeo.com/developers/)
2. Create an Application API Key at [https://www.eegeo.com/developers/](https://www.eegeo.com/developers/)
3. Create A new POI Set
4. Associate your Application API Key with your newly created POI Set
5. Add POIs to your POI Set
6. Perform Free-Text, Category or Indoor queries

---

## Full POI API Specification

#### Authentication Token

Obtain a Developer Authentication Token by signing up at [https://www.eegeo.com/developers/](https://www.eegeo.com/developers/). The Developer Authentication Token allows you to make authenticated requests against the POI service.

The Authentication Token will be referred to as ```dev_auth_token``` throughout this README

#### Application API Key

The Application API Key is the API key used to authenticate the eeGeo SDK. Application Keys can be associated with POI sets, providing that Application access to the POI set. Obtain Application API keys from [https://www.eegeo.com/developers/](https://www.eegeo.com/developers/).

Application API Keys will be referred to as ```app_api_key``` throughout this README

#### POI Sets

A POI Set is a collection of Points of Interest. You can associate multiple Application API keys with POI Sets, allowing multiple applications or platforms access to the same POI Set.

A POI Set is a JSON object with the following attributes:

|Field|Type|Description|
 --- | --- | ---
|`id`|integer| a unique identifier for the poi set
|`name`|string| an appropriate name for the poi set
|`api_key_permissions`|string list| app api keys that have access to this poi set

##### Create a POI Set

To create a new POI Set, make a RESTful request passing the name of the POI set:

```sh
$ curl -v -XPOST https://poi.eegeo.com/v1/poisets/?token=dev_auth_token -d '{"name":"my-poi-set"}'
```

The response will be a JSON object specifying the newly created POI Set:

```json
{
"id":1, 
"name":"my-poi-set", 
"api_key_permissions":[]
}
```

Make note of the POI Set ID, in this case ```1``` as this is used to make future requests against this newly created POI Set.

##### Query all POI sets

All POI Sets you own can be listed by making a RESTful request to the poisets resource:

```
$ curl -v https://poi.eegeo.com/v1/poisets/?token=<dev_auth_token>
```

This will return a collection of all POI Sets you own

##### Query a POI set

To query an individual POI Set, make a RESTful request to the poiset:

```
$ curl -v https://poi.eegeo.com/v1/poisets/<SID>?token=<dev_auth_token>
```

Where ```<SID>``` is the POI Set ID to query. This will return the POI Set as JSON.

##### Delete a POI Set

To delete a POI Set, make a RESTful request to the poiset:
```
$ curl -v -XDELETE https://poi.eegeo.com/v1/poisets/<SID>?token=<dev_auth_token>
```
Where ```<SID>``` is the POI Set ID to delete.

##### Associate App API Key

Application API Keys can be associated with a POI Set to provide that Application access to the POIs in the POI Set.

To do this, make a RESTful call:

```sh
$ curl -v -XPOST https://poi.eegeo.com/v1/poisets/<SID>?token=<dev_auth_token> -d '{"apikey":"<app_api_key>"}'
```

Where ```app_api_key``` is the Application API Key, and where ```<SID>``` is the POI Set ID to add the Application API Key to.

##### Unassociate App API Key

To unassociate an Application API Key from a POI Set, perform the following RESTful call:

```sh
$ curl -v -XDELETE https://poi.eegeo.com/v1/poisets/<SID>/<app_api_key>?token=<dev_auth_token>
```

Where ```app_api_key``` is the Application API Key, and where ```<SID>``` is the POI Set ID to remove the Application API Key from.

#### POI

A POI is a Point of Interest.

#### Indoor POI

Indoor POIs are supported, Indoor POIs are associated with an indoor map and are only visible within that indoor map.

#### Default Taxonomy


---

#### Disclaimer
This is an early version of the data format and API for eeGeo indoor maps.  eeGeo Ltd reserves the right to make changes to the API and its documentation at any time.  

---

#### Contact us
If you have any problems or queries please [raise an issue](https://github.com/eegeo/indoor-maps-api/issues/new) or alternatively get in touch with us at support@eegeo.com.
