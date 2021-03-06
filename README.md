# hydra-jetty-lyo

This is a copy of jetty with applications for running Hydra.  These include two java-based applications:

* [Patched Lyo repository](https://github.com/barmintor/lyo)
* [Solr](http://lucene.apache.org/solr/)

## Included Versions

* jetty: 8.1.16
* solr: 4.10.3
* lyo: 3.0.0-SNAPSHOT patched for:
 * HTTP PATCH Sparql-Update for RdfResource
 * 410 (GONE) for requests to deleted resources

## Usage

### Dependencies

* [Java 7 (JRE)](https://java.com/en/download/index.jsp)

### Manual
  
    git clone https://github.com/barmintor/hydra-jetty-lyo
    cd hydra-jetty-lyo
    java -Xmx512m -XX:MaxPermSize=512m -jar start.jar

You can also change the port jetty starts on by editing the file etc/jetty.xml and changing this line to indicate a different port number:

    <Set name="port"><SystemProperty name="jetty.port" default="8983"/></Set>

### Using jettywrapper

For use within your Hydra application's Rails directory.

    rake jetty:install
    rake jetty:start

See [jettywrapper](https://github.com/projecthydra/jettywrapper) for more information regarding configuration and usage.
Port numbers and other java options maybe configured via the gem. 
    
### Interaction

When jetty is finished initializing itself, Solr is available at 

* [http://localhost:8983/solr/](http://localhost:8983/solr/)

and Lyo is available at

* [http://localhost:8983/ldp/](http://localhost:8983/ldp/)
* basic authorization is enabled an requires the username/password `fedoraAdmin/fedoraAdmin`
* this is configured under [jetty-users.properties](resources/jetty-users.properties)

You can see a list of all installed applications at

* [http://localhost:8983](http://localhost:8983)

### Updating

#### Solr and Jetty

Solr is updated by downloading the latest from [Lucene](http://lucene.apache.org/solr/), which includes an instance of Jetty in the
`example` directory.  Updating is a process of replacing the jar files as well as the solr.war and start.jar files.  Note that the
example from Lucene does not include the start.ini file.

