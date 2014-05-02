<img src="http://efemurl.com/themes/efemurl/images/logo.jpg" width="150"><br>

This is a profile of the [XDI2](http://github.com/projectdanube/xdi2) server, configured to 
act as an Efemurl-hosted registry for cloud names and cloud numbers, and to instantiate
XDI graphs for personal clouds.

### How to build

First, you need to build the main [XDI2](http://github.com/projectdanube/xdi2) project.

After that, just run

    mvn clean install

To build all components.

### How to run

    mvn jetty:run

Then the XDI2 status page is available at

	http://localhost:15540/admin

### Registry

How to register a cloud name and cloud number:

For example, to register cloud name **=william** with cloud number **[=]!:uuid:bd00b25b-d93f-4f42-93a9-25d7ad2ba305**:

	POST the following XDI message to http://localhost:15540/registry

	=sender[$msg]!1/$is()/([+]!:uuid:d541e1ec-7b19-42ee-ae9b-5f6e0d239a26)
	=sender[$msg]!1$do/$set/((=william)/$ref/([=]!:uuid:bd00b25b-d93f-4f42-93a9-25d7ad2ba305))
	=sender[$msg]!1$do/$set/(([=]!:uuid:bd00b25b-d93f-4f42-93a9-25d7ad2ba305)/$is$ref/(=william))
	=sender[$msg]!1$do/$set/(([=]!:uuid:bd00b25b-d93f-4f42-93a9-25d7ad2ba305)<$xdi><$uri>&/&/"http://localhost:15540/users/%5B%3D%5D%21%3Auuid%3Abd00b25b-d93f-4f42-93a9-25d7ad2ba305")

### User clouds

How to write data to =william's XDI graph (= personal cloud):

	POST the following XDI message to http://localhost:15540/users/%5B%3D%5D%21%3Auuid%3Abd00b25b-d93f-4f42-93a9-25d7ad2ba305

	=sender[$msg]!1/$is()/([=]!:uuid:bd00b25b-d93f-4f42-93a9-25d7ad2ba305)
	=sender[$msg]!1$do/$set/(...some.xdi.statement.here...)

### Persistence

For now the configuration will store graphs in memory, i.e. not persist them, but we can change that.

### Security

Let's leave out authentication and access control (using "link contracts") for now...
