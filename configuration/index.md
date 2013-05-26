---
layout: page
title: Configuration
nav: endpoints
anchors:
  - title: Get configuration
    url: "#getconfig"
  - title: Aquire API key
    url: "#aquireapikey"
  - title: Delete API key
    url: "#deleteapikey"
  - title: Get full state
    url: "#getfullstate"
---

The configuration endpoint allows to retreive the current configuration of the gateway.

------------------------------------------------------

## Get configuration<a name="getconfig">&nbsp;</a>

	GET /api/<apikey>/config

Returns the current gateway configuration.

### Parameters

None

### Response
<pre class="headers">
<code>
HTTP/1.1 200 OK
Etag: 203941fel3ds8ad61903224
Last-Modified: Tue, 15 Nov 2012 10:12:00 GMT
</code>
</pre>
<pre class="highlight">
<code>
{
	"name": "deCONZ-RPi Gateway",
	"ipaddress": "192.168.1.20",
	"mac": "00:15:22:22:00:11:11:a3",
	"linkbutton": false,
	"utc": "2013-05-10T09:01:23",
	"swversion": "0114"
}
</code>
</pre>
#### Response fields

<table class="table table-bordered">
	<thead>
		<tr><th>Field</th><th>Type</th><th>Description</th></tr>
	</thead>
	<tbody>
		<tr>
			<td>name</td>
			<td>String</td>
			<td>Name of the gateway.</td>
		</tr>
		<tr>
			<td>ipaddress</td>
			<td>String</td>
			<td>IPv4 address of the gateway.</td>
		</tr>
		<tr>
			<td>mac</td>
			<td>String</td>
			<td>MAC address of the gateway.</td>
		</tr>
		<tr>
			<td>linkbutton</td>
			<td>Bool</td>
			<td>true if the linkbutton was pressed.</td>
		</tr>
		<tr>
			<td>utc</td>
			<td>String</td>
			<td>Current UTC time of the gateway in ISO 8601 format.</td>
		</tr>
		<tr>
			<td>swversion</td>
			<td>String</td>
			<td>API version as string.</td>
		</tr>
	</tbody>
</table>

### Possible errors

[403 Forbidden](/errors#403)

------------------------------------------------------

## Aquire API key<a name="aquireapikey">&nbsp;</a>

	POST /api

Creates a new [API key](/authorization) which provides authorized access to the REST API.

### Parameters

<table class="table table-bordered">
	<thead>
		<tr><th>Field</th><th>Type</th><th>Description</th><th>Required</th></tr>
	</thead>
	<tbody>
		<tr>
			<td>devicetype</td>
			<td>String (0..40 chars)</td>
			<td>Name of the client application.</td>
			<td>required</td>
		</tr>
		<tr>
			<td>username</td>
			<td>String (10..40 chars)</td>
			<td>Will be used as username. If not specified a random key will be generated.</td>
			<td>optional</td>
		</tr>
	</tbody>
</table>

### Example request data
	{
		"username": "988112a4e198cc1211",
		"devicetype": "my application"
	}

### Response

<pre class="headers">
<code>
HTTP/1.1 200 OK
</code>
</pre>
<pre class="highlight">
<code>
[ { "success": { "username": "988112a4e198cc1211" } } ]
</code>
</pre>

### Possible errors

[400 Bad Request](/errors#400)

------------------------------------------------------

## Delete API key<a name="deleteapikey">&nbsp;</a>

	DELETE /api/<apikey>/config/whitelist/<apikey2>

Deletes a API key so it could no longer be used.

### Parameters

None

### Possible errors

[403 Forbidden](/errors#403)

[404 Not Found](/errors#404)

------------------------------------------------------

## Get full state<a name="getfullstate">&nbsp;</a>

	GET /api/<apikey>

Returns the full state of the gateway including all its lights, groups, scenes and schedules.

### Parameters

None

### Response

<pre class="headers">
<code>
HTTP/1.1 200 OK
Etag: 203941fel3ds8ad61903224
Last-Modified: Tue, 10 Nov 2012 21:16:04 GMT
</code>
</pre>
<pre class="highlight">
<code>
{
    "config": {
        "dhcp": true,
        "gateway": "192.168.178.1",
        "ipaddress": "192.168.192.237",
        "linkbutton": true,
        "mac": "E0:69:95:58:06:7F",
        "name": "deCONZ Gateway",
        "netmask": "255.255.255.0",
        "portalservices": false,
        "proxyaddress": "",
        "proxyport": 0,
        "swupdate": {
            "notify": false,
            "text": "",
            "updatestate": 0,
            "url": ""
        },
        "swversion": "01005215",
        "utc": "2013-05-22T12:02:30",
        "whitelist": {}
    },
    "groups": {
        "32769": {
            "action": {
                "bri": 3945,
                "colormode": "hs",
                "ct": 500,
                "effect": "none",
                "hue": 0,
                "on": true,
                "sat": 17680,
                "xy": [
                    0.0610457,
                    0.219979
                ]
            },
            "etag": "893f60b611274d1803207298cf26b1e1",
            "lights": [],
            "name": "Demo",
            "scenes": []
        }
    },
    "lights": {},
    "schedules": {}
}
</code>
</pre>

#### Response fields

<table class="table table-bordered">
	<thead>
		<tr><th>Field</th><th>Type</th><th>Description</th></tr>
	</thead>
	<tbody>
		<tr>
			<td>config</td>
			<td>Object</td>
			<td>Configuration of the gateway.</td>
		</tr>
		<tr>
			<td>groups</td>
			<td>Object</td>
			<td>All groups of the gateway.</td>
		</tr>
		<tr>
			<td>lights</td>
			<td>Object</td>
			<td>All lights of the gateway.</td>
		</tr>
		<tr>
			<td>schedules</td>
			<td>Object</td>
			<td>All schedules of the gateway.</td>
		</tr>
	</tbody>
</table>

### Possible errors

[403 Forbidden](/errors#403)