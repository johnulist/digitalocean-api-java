# DigitalOcean API Client  [![Build Status](https://travis-ci.org/jeevatkm/digitalocean-api-java.svg?branch=master)](https://travis-ci.org/jeevatkm/digitalocean-api-java) [![Version](https://img.shields.io/badge/version-2.16-blue.svg)](https://github.com/jeevatkm/digitalocean-api-java/releases/latest) [![License](https://img.shields.io/github/license/jeevatkm/digitalocean-api-java.svg)](LICENSE)

***v2.16 [released](https://github.com/jeevatkm/digitalocean-api-java/releases/latest) and tagged on Sep 03, 2018***

Simple & Lightweight API client library for Enterprise Application or Utilities Integration around [DigitalOcean RESTful APIs][1]. You can use this library with project based (JVM hosted languages) on Java, Groovy, Scala, Clojure, etc.

Give your support by clicking Hearts on [DigitalOcean Developers Community](https://www.digitalocean.com/community/projects/api-client-in-java) :)

# Getting Started

For handy use, DigitalOcean API Client library project dependency definition provided below or you wanna jar [Download it][16] from Maven central repo.

*Note: [master][11] branch maps to v2 APIs and digitalocean turned off [v1 APIs](https://developers.digitalocean.com/documentation/changelog/api-v1/sunsetting-api-v1/) as on Nov 9, 2015 .*

**Maven dependency**
```xml
<dependency>
    <groupId>com.myjeeva.digitalocean</groupId>
    <artifactId>digitalocean-api-client</artifactId>
    <version>2.16</version>
</dependency>
```
**Gradle/Grails dependency**
```shell
compile 'com.myjeeva.digitalocean:digitalocean-api-client:2.16'
```
**Groovy Grape**
```groovy
@Grapes(
@Grab(group='com.myjeeva.digitalocean', module='digitalocean-api-client', version='2.16')
)
```
**Scala SBT**
```shell
libraryDependencies += "com.myjeeva.digitalocean" % "digitalocean-api-client" % "2.16"
```

**Note:** For Android projects, kindly include the `httpclient-android` library explicitly in your project dependencies.

* * *

# Getting Help

For API documentation see:

* [DigitalOcean API Client in Java][2]

For Example usage see:

* Have a look at [DigitalOceanIntegrationTest][7]

# Samples

**Creating a DigitalOcean Client in three simple ways!**
```java
// Way one, just pass on authToken
DigitalOcean apiClient = new DigitalOceanClient(authToken);

// Way two, pass on version number & authToken
DigitalOcean apiClient = new DigitalOceanClient("v2", authToken);

// Way three, pass on version number, authToken & httpClient
// Go ahead and customize httpClient attributes for requirements
CloseableHttpClient httpClient = HttpClients.createDefault();
DigitalOcean apiClient = new DigitalOceanClient("v2", authToken, httpClient);
```

**Let's invoke the method(s) as per need via apiClient**
```java
// Fetching all the available droplets from control panel
Droplets droplets = apiClient.getAvailableDroplets(pageNo, perPage);

// Fetching all the available kernels for droplet
Kernels kernels = apiClient.getAvailableKernels(dropletId, pageNo, perPage);

// Create a new droplet
Droplet newDroplet = new Droplet();
newDroplet.setName("api-client-test-host");
newDroplet.setSize(new Size("512mb")); // setting size by slug value
newDroplet.setRegion(new Region("sgp1")); // setting region by slug value; sgp1 => Singapore 1 Data center
newDroplet.setImage(new Image(1601)); // setting by Image Id 1601 => centos-5-8-x64 also available in image slug value
newDroplet.setEnableBackup(Boolean.TRUE);
newDroplet.setEnableIpv6(Boolean.TRUE);
newDroplet.setEnablePrivateNetworking(Boolean.TRUE);

// Adding SSH key info
List<Key> keys = new ArrayList<Key>();
keys.add(new Key(6536653));
keys.add(new Key(6536654));
newDroplet.setKeys(keys);

// Adding Metadata API - User Data
newDroplet.setUserData(" < YAML Content > "); // Follow DigitalOcean documentation to prepare user_data value
Droplet droplet = apiClient.createDroplet(newDroplet);


// Creating multiple droplets
Droplet droplet = new Droplet();
droplet.setNames(Arrays.asList("sub-01.example.com", "sub-02.example.com"));
droplet.setSize("512mb");
droplet.setImage(new Image("ubuntu-14-04-x64"));
droplet.setRegion(new Region("nyc1"));
Droplets droplets = apiClient.createDroplets(droplet);

// Fetch droplet information
Droplet droplet = apiClient.getDropletInfo(dropletId);

// Fetch Available Plans/Sizes supported by DigitalOcean
Sizes sizes = apiClient.getAvailableSizes(pageNo);

// Fetch Available Regions supported by DigitalOcean
Regions regions = apiClient.getAvailableRegions(pageNo);
```

**Accessing `RateLimit` header values from return object. This is applicable for all requests**.
```java
Droplets droplets = getAvailableDroplets(1, 20);
RateLimit rateLimit = droplets.getRateLimit();

Actions actions = getAvailableActions(2, 40);
RateLimit rateLimit = actions.getRateLimit();

Domain domain = getDomainInfo("myjeeva.com");
RateLimit rateLimit = domain.getRateLimit();

Droplet droplet = getDropletInfo(10000001);
RateLimit rateLimit = droplet.getRateLimit();
```

# Reporting Issues

DigitalOcean API Client uses [GitHub’s integrated issue tracking system][3] to record bugs and feature requests. If you want to raise an issue, please follow the recommendations bellow:

* Before you log a bug, please search the issue tracker to see if someone has already reported the problem. If the issue doesn’t already exist, create a new issue.
* Please provide as much information as possible with the issue report, we like to know the version of DigitalOcean API Client that you are using.
* If you need to paste code, or include a stack trace use Markdown ``` escapes before and after your text.

# Supported API's and Changelogs

Refer to [CHANGELOG.md](CHANGELOG.md)

# Author

Jeevanandam M. - jeeva@myjeeva.com

# Contributing

1. Fork it
2. Create your feature branch - `git checkout -b my-new-feature`
3. Implement your changes and apply [Google Java Code Formatter][13]
4. Commit your changes - `git commit -am 'Added feature'`
5. Push to the branch - `git push origin my-new-feature`
6. Create new Pull Request

# License

DigitalOcean API Client - [MIT License][6].


[1]: https://developers.digitalocean.com
[2]: https://docs.myjeeva.com/javadoc/digitalocean-api-client/2.16/
[3]: https://github.com/jeevatkm/digitalocean-api-java/issues
[4]: https://oss.sonatype.org/content/repositories/snapshots/com/myjeeva/digitalocean/digitalocean-api-client/
[5]: https://myjeeva.com
[6]: https://github.com/jeevatkm/digitalocean-api-java/blob/master/LICENSE
[7]: https://github.com/jeevatkm/digitalocean-api-java/blob/master/src/test/java/com/myjeeva/digitalocean/DigitalOceanIntegrationTest.java
[8]: http://search.maven.org/remotecontent?filepath=com/myjeeva/digitalocean/digitalocean-api-client/1.5/digitalocean-api-client-1.5.jar
[9]: https://github.com/jeevatkm/digitalocean-api-java/blob/master/src/test/java/com/myjeeva/digitalocean/DigitalOceanMockTest.java
[10]: http://docs.myjeeva.com/javadoc/digitalocean-api-client/2.4-SNAPSHOT/com/myjeeva/digitalocean/DigitalOcean.html
[11]: https://github.com/jeevatkm/digitalocean-api-java
[12]: https://github.com/jeevatkm/digitalocean-api-java/tree/api-v1
[13]: https://raw.githubusercontent.com/darcyliu/google-styleguide/master/eclipse-java-google-style.xml
[14]: https://developers.digitalocean.com/documentation/changelog/api-v2/add-status-to-account/
[15]: https://developers.digitalocean.com/documentation/changelog/api-v2/deprecate-final-snaphots/
[16]: http://search.maven.org/remotecontent?filepath=com/myjeeva/digitalocean/digitalocean-api-client/2.16/digitalocean-api-client-2.16.jar
