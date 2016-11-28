# Extending Directus

### Custom User-Interfaces (UIs)
Similar to extensions, if you need an input more specific to your application than provided by core Directus, you can duplicate, tweak, or create your own. Need a custom room-mapping interface or a proprietary client input? Just create a quick custom UI and it will immediately be available for use.
**[todo]**

### Custom Extensions
By design, Directus keeps things simple. Only key features utilized by more than 80% of users make it into the core software. Anything not covered under the base suite is possible within extensions. Extensions take advantage of the system’s authentication, ACL, and data connections but force absolutely no restrictions. These sandboxed areas can be used to create custom interfaces, data-visualizations, interaction points, dashboards, point-of-sales, or anything else required by your project.
**[todo]**

### Custom API Endpoints
If you’re using Directus' API endpoints (possibly feeding a mobile app or providing a SASS interface) you can always write custom endpoints to compliment the core data/schema/user access.
**[todo]**

### Custom File Storage Adapters

Beyond local storage, Directus comes with the ability to connect to a number of popular file storage systems such as CDNs, Amazon S3, Rackspace, Azure and Dropbox.

As with most things within Directus, if you need something more specific the tools exist to easily implement a custom adapter. Directus uses [Flysystem](https://github.com/thephpleague/flysystem), you can read [how to create new custom adaptes](https://flysystem.thephpleague.com/creating-an-adapter/) on their site.

Storage Adapters enable a Directus instance to configure the destination for writing and reading the files which is loaded into the application. Within the `configuration.php` file, they are defined by the `filesystem` attribute. (Currently there is not an application-level interface to view or edit these.)

As of writing, these are the adapters can be used out of the box:

- Local – Maps to local filesystem of the application server which hosts the Directus instance
- Ftp **TODO**

These are the supported adapters (Installation required):
- [Amazon Web Services - S3 V2](https://github.com/thephpleague/flysystem-aws-s3-v2) – Maps to Amazon S3 v2 CDN Buckets
- [Amazon Web Services - S3 V3](https://github.com/thephpleague/flysystem-aws-s3-v3) – Maps to Amazon S3 v3 CDN Buckets

### @TODO (Supporting)

_This adapter is planned for an upcoming release._

These are also available (Installation required):

- [Rackspace Cloud Files](https://github.com/thephpleague/flysystem-rackspace) – Maps to Rackspace OpenCloud CDN Containers
- [Dropbox](https://github.com/thephpleague/flysystem-dropbox)
- [Amazon Cloud Drive](https://github.com/nikkiii/flysystem-acd)
- [OneDrive](https://github.com/jacekbarecki/flysystem-onedrive)
- [Sftp (through phpseclib)](https://github.com/thephpleague/flysystem-sftp)
- [Zip (through ZipArchive)](https://github.com/thephpleague/flysystem-ziparchive)
- [WebDAV (through SabreDAV)](https://github.com/thephpleague/flysystem-webdav)
- [PHPCR](https://github.com/thephpleague/flysystem-phpcr)
- [Redis (through Predis)](https://github.com/danhunsaker/flysystem-redis)
- [Fallback](https://github.com/Litipk/flysystem-fallback-adapter)
- [Memory](https://github.com/thephpleague/flysystem-memory)
- [Google Cloud Storage](https://github.com/Superbalist/flysystem-google-storage)
- [SinaAppEngine Storage](https://github.com/litp/flysystem-sae-storage)
- [Gaufrette](https://github.com/jenkoian/flysystem-gaufrette)
- [OpenStack Swift](https://github.com/nimbusoftltd/flysystem-openstack-swift)

These are the ones listed on the flysystem page, if the one you are looking for is not listed above, it can be found on GitHub, otherwise you have to create a custom one.

All adapters have different configurable parameters.

```php
'filesystem' => [
    // adapter name
    'adapter' => 'local',
    // By default media directory are located at the same level of directus root
    // To make them a level up outsite the root directory
    // use this instead
    // Ex: 'root' => realpath(BASE_PATH.'/../storage/uploads'),
    // Note: BASE_PATH constant doesn't end with trailing slash
    'root' => BASE_PATH . '/storage/uploads',
    // This is the url where all the media will be pointing to
    // here all assets will be (yourdomain)/storage/uploads
    // same with thumbnails (yourdomain)/storage/uploads/thumbs
    'root_url' => '/storage/uploads',
    'root_thumb_url' => '/storage/uploads/thumbs',
    //   'key'    => 's3-key',
    //   'secret' => 's3-key',
    //   'region' => 's3-region',
    //   'version' => 's3-version',
    //   'bucket' => 's3-bucket'
],
```

#### Installing an adapter

Installing a new adapter using composer can be done executing the command below in a terminal:

Ex: Installing Amazon S3 v3 Adapter.

```
composer require league/flysystem-aws-s3-v3
```

You can read on each adapter GitHub page on how to install each one if you are having issues related to the installation process.

#### Code samples

When building out Directus core functionality and derivative client functionality, it may be necessary to invoke the storage adapter component. Listed below are some references to code samples which demonstrate various ways of deploying storage adapters.

These links point directly to the commit hash which is current as of this writing, so that line numbers do not move out of sync with the documentation. Remember to compare these code snippets with the current state of Directus code in the future, and to update these docs if necessary.

`/directus/api/api.php`

The [definition of the upload route](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2FRNGR%2Fdirectus6%2Fblob%2Ff386da45a4957f776c4a701fdd31aae2c93e1273%2Fapi%2Fapi.php%23L781&sa=D&sntz=1&usg=AFQjCNF61vBWbi9eTJc1FvUaSCXAnXM_uQ) shows the most generic (core) way of implementing the storage adapter interface.  We instantiate a new `\Directus\Media\Storage\Storage` object and then simply call the `acceptFile` method with the incoming local file. The interface automatically fetches the default/thumbnail adapters and passes this information to them.

`/directus/media_auth_proxy/index.php`

The authenticated media proxy front controller uses a [slightly more complex implementation](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2FRNGR%2Fdirectus6%2Fblob%2Ff386da45a4957f776c4a701fdd31aae2c93e1273%2Fmedia_auth_proxy%2Findex.php%23L120&sa=D&sntz=1&usg=AFQjCNFvgWXCSmwfnxuTzYVgymy3TNEujg). After identifying the Directus Media record being requested, it fetches the record for the corresponding storage adapter. It then passes this record to the method `\Directus\Media\Storage\Storage::getStorage`, which returns the corresponding adapter object, allowing the front controller to fetch the file contents abstractly, irrespective of the underlying driver / file location.

`/directus/bin/generateMissingThumbnails.php`

[This implementation](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2FRNGR%2Fdirectus6%2Fblob%2Ff386da45a4957f776c4a701fdd31aae2c93e1273%2Fbin%2FgenerateMissingThumbnails.php&sa=D&sntz=1&usg=AFQjCNFJOUy3bKpTj0W4XtYE5nwsP_9ZUg) uses the same approach as the authenticated media front controller, however it performs more complex operations, such as checking if a file exists, and writing a file to the adapter.

### Hooks

Hooks allow project-specific (non-Directus core) code to interact directly with Directus core events. The two hooks which are currently supported are `postUpdate` and `postInsert`, which enable logic to react to Directus record update and insert events, respectively. The hooks are very simple to implement: just add custom logic to the (untracked) config file at  /directus/api/configuration.php. [See this example configuration file as a reference.](https://github.com/RNGR/directus6/blob/f386da45a4957f776c4a701fdd31aae2c93e1273/api/configuration.example.php#L31)
