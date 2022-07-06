# CONFIGURE BUILDER

[DOCS](https://www.electron.build/configuration/configuration)

## Config options

### Table of content

- [appId](#appid)
- [productName](#productname)
- [artifactName](#artifactname)
- [copyright](#copyright)
- [files](#files)
- [extraResources](#extraresources)
- [asar](#asar)
- [asarUnpack](#asarunpack)
- [directories](#directories)
  - [app](#directoriesapp)
  - [buildResources](#directoriesbuildresources)
  - [output](#directoriesoutput)
- [afterSign](#aftersign)
- [publish](#publish)
  - [provider](#publishprovider)
  - [url](#publishurl)
  - [channel](#publishchannel)
  - [publishAutoUpdate](#publishautoupdate)
  - [publisherName](#publishername)
  - [example](#publishexample)
- [generateUpdatesFilesForAllChannels](#generateupdatesfilesforallchannels)
- [mac](#mac)
  - [category](#category)
  - [target](#target)

---

### appId

Type: `null | string`   
Default: `com.electron.${name}`

The application id. Used
as [CFBundleIdentifier](https://developer.apple.com/library/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html#//apple_ref/doc/uid/20001431-102070)
for MacOS and
as [Application User Model ID](https://msdn.microsoft.com/en-us/library/windows/desktop/dd378459(v=vs.85).aspx) for
Windows (NSIS target only, Squirrel.Windows not supported)

### productName

Type: `null | string`

As [name](#Metadata-name), but allows you to specify a product name for your executable which contains spaces and other
special characters not allowed in the [name property](https://docs.npmjs.com/files/package.json#name)

### artifactName

Type: `null | string`

The [artifact file name template](/configuration/configuration#artifact-file-name-template). Defaults
to `${productName}-${version}.${ext}` (some target can have other defaults, see corresponding options)

### copyright

Type: `null | string`  
Default: `Copyright © year ${author}`

The human-readable copyright line for the app

### files

[docs](https://www.electron.build/configuration/contents#files)  
Type: `Array<String | FileSet> | String | FileSet`

A glob patterns relative to the app directory, which specifies which files to include when copying files to create the
package

### extraResources

[docs](https://www.electron.build/configuration/contents#extraresources)  
Type: `Array<String | FileSet> | String | FileSet`

A glob patterns relative to the project directory, when specified, copy the file or directory with matching names
directly into the app’s resources directory (Contents/Resources for MacOS, resources for Linux and Windows).

File patterns (and support for from and to fields) the same as for files

### asar

Type: `boolean | null | object`  
Default: `true`

Whether to package the application's source code into an archive,
using [Electron's archive format](http://electron.atom.io/docs/tutorial/application-packaging/).

Node modules, that must be unpacked, will be detected automatically, you don't need to explicitly
set [asarUnpack](#configuration-asarUnpack) - please file an issue if this doesn't work

### asarUnpack

Type: `array | null | string`

A glob patterns relative to the app directory, which specifies which files to unpack when creating the asar archive.

### directories

Type: `null | object`

#### app<a name="directoriesapp"></a>
Type: `null | string`

The application directory (containing the application package.json), defaults to `app`, `www` or working directory

#### buildResources<a name="directoriesbuildResources"></a>

Type: `null | string`  
Default: `build`

The path to build resources.

Please note — build resources is not packed into the app. If you need to use some files, e.g. as tray icon, please
include required files explicitly: `"files": ["**\/*", "build/icon.*"]`

#### output<a name="directoriesoutput"></a>

Type: `null | string`  
Default: `dist`

The output directory. [File macros](/file-patterns#file-macros) are supported.

### afterSign

Type: `null | string`

The function (or path to file or module id) to be [run after pack and sign](#aftersign) (but before pack into
distributable format)

### publish

[docs](https://www.electron.build/configuration/publish)  
Type: `Array | null | object | string`

You can use one of `[github, snapStore, spaces, keygen, bitbucket, s3, generic]` provider. Read about any
in [docs](https://www.electron.build/configuration/publish)

To publish on own server use *`generic`* provider

**GenericServerOptions**  
Generic (any HTTP(S) server) options.
In all publish options [File Macros](/file-patterns#file-macros) are supported

#### provider<a name="publishprovider"></a>

Type: `string`  
Value: `"generic"`

The provider. Must be `generic`

#### url<a name="publishurl"></a>

Type: `string`

The base url

#### channel<a name="publishchannel"></a>

Type: `null | string`  
Default: `"latest"`  
Required: `false`

The channel

#### publishAutoUpdate<a name="publishAutoUpdate"></a>

Type: `boolean`  
Default: `true`  
Required: `false`

Whether to publish auto update info files.

Auto update relies only on the first provider in the list (you can specify several publishers).
Thus, probably, there`s no need to upload the metadata files for the other configured providers. But by default will be
uploaded

#### publisherName<a name="publisherName"></a>

Type: `String | Array<String> | “undefined”`  
Required: `false`

The publisher name, exactly as in your code signed certificate. Several names can be provided. Defaults to common name
from your code signing certificate.

#### example<a name="publishexample"></a>

Minimum config to publish option

```json
{
  "publish": {
    "provider": "generic",
    "url": "http://127.0.0.1:8080"
  }
}
```

### generateUpdatesFilesForAllChannels

Type: `boolean`  
Default: `false`

Please
see [Building and Releasing using Channels](https://github.com/electron-userland/electron-builder/issues/1182#issuecomment-324947139)

### mac

Type: `null | object`

Options related to how build macOS targets

#### category

Type: `null | string`

The application category type, as shown in the Finder via *View -> Arrange by Application Category* when viewing the
Applications directory.

For example, `"category": "public.app-category.developer-tools"` will set the application category to *Developer Tools*.

Valid values are listed
in [Apple's documentation](https://developer.apple.com/library/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/LaunchServicesKeys.html#//apple_ref/doc/uid/TP40009250-SW8)

#### target
