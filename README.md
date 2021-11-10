# Advanced styles for CARTO Mobile SDK

## About

This project contains 3 styles (**OSM**, **Outdoor**, **Streets**) that can be used as a replacement
for built-in CARTO Mobile SDK styles (Voyager, Positron, Darkmatter).

Unlike built-in CARTO Mobile SDK styles, which are intended as non-intrusive background layers for
data overlays, these styles are full featured and can be used as main layers in routing or hiking
applications.

Major features:

* Rendering of additional map features like mountain peaks, beaches, parks, wet areas
* Contours (requires data source with contour data)
* Advanced POI styling
* Marking of one-way streets

## Requirements

The styles are developed and tested with CARTO Mobile SDK 4.4.2. They may work with older SDK versions, but we strongly suggest using this SDK version (or any newer version). 

## Usage

First step is to checkout the project, zip it into a single archive. Then add the archive
to the assets of your project.

### Android (Java)

```
String styleName = "osm"; // use "osm", "outdoors" or "streets"
BinaryData styleData = AssetUtils.loadAsset("new_carto_theme.zip"); // name of your zipped archive
AssetPackage styleAssetPackage = new ZippedAssetPackage(styleData);
CompiledStyleSet styleSet = new CompiledStyleSet(styleAssetPackage, styleName);
MBVectorTileDecoder tileDecoder = new MBVectorTileDecoder(styleSet);
TileDataSource tileDataSource = new CartoOnlineVectorTileDataSource("carto.streets"); // or any other data source
VectorTileLayer tileLayer = new VectorTileLayer(tileDataSource, tileDecoder);
mapView.getLayers().add(tileLayer);
```

### iOS (Objective C)

```
NSString* styleName = @"osm"; // use "osm", "outdoors" or "streets"
NTBinaryData* styleData = [NTAssetUtils loadAsset:@"new_carto_theme.zip"]; // name of your zipped archive
NTAssetPackage* styleAssetPackage = [[NTZippedAssetPackage alloc] initWithZipData:styleData];
NTCompiledStyleSet* styleSet = [[NTCompiledStyleSet alloc] initWithAssetPackage:styleAssetPackage styleName:styleName];
NTMBVectorTileDecoder* tileDecoder = [[NTMBVectorTileDecoder alloc] initWithCompiledStyleSet:styleSet];
NTTileDataSource* tileDataSource = [[NTCartoOnlineVectorTileDataSource alloc] initWithSource:@"carto.streets"]; // or any other data source
NTVectorTileLayer* tileLayer = [[NTVectorTileLayer alloc] initWithDataSource:tileDataSource decoder:tileDecoder];
[[mapView getLayers] add:tileLayer];
```

### Supported 'nutiparameters'

All styles support following 'nutiparameters' for customizing:

* `lang`: Language of the map ("en", "de", ...). Default is "en".
* `fallback_lang`: Fallback language in case when main language name is not available. Default is "en".
* `contours`: Either 0 (no contours) or 1 (contours). The default is 1. Note that this requires data source with contour data.
* `contoursOpacity`: Value between 0.0 and 1.0. Default is 1.0.
* `buildings`: Either 0 (no buildings), 1 (2D buildings) or 2 (3D buildings). Default is 1.
* `texts3d`: Either 0 (2D texts) or 1 (3D texts, billboards). Default is 1.
* `markers3d`: Either 0 (2D markers) or 1 (3D markers, billboards). Default is 1.
* `shields3d`: Either 0 (2D shields) or 1 (3D shields, billboards). Default is 1.

The parameters can be set via `MBVectorTileDecoder` `setStyleParameter` method.
