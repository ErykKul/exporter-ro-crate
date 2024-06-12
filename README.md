# Customizable RO-Crate Metadata Exporter for Dataverse
A customizable external metadata exporter for [Dataverse](https://dataverse.org) for exporting dataset metadata as an [RO-Crate JsonLD](https://www.researchobject.org/ro-crate/1.1/appendix/jsonld.html). 

RO-Crate is a "community effort to establish a lightweight approach to packaging research data with their metadata [...] based on schema.org annotations in JSON-LD" ([Research Object Crate](https://w3id.org/ro/crate)). 

This exporter produces JSON-LD objects similar to this [example](https://rawcdn.githack.com/biocompute-objects/bco-ro-example-chipseq/76cb84c8d6a17a3fd7ae3102f68de3f780458601/data/ro-crate-metadata.json). It is based on the [dataverse-transformer-exporter](https://github.com/ErykKul/dataverse-transformer-exporter/) with the usage of the values as provided by the internal Dataverse schema.org exporter. This exporter copies all of the values as produced by that schema.org exporter, ensuring the maximal coverage of schema.org fields. The fields are copied into RO-Crate structure using the transformations as specified in the [transformer.json](/transformer.json) file. You can customize this exporter by editing that file. However, if new fields should be added to this exporter and they are compliant with the schema.org, consider opening an issue at the [Dataverse project](https://github.com/iqss/dataverse), so that they can be added to the internal exporter first (they would be then automatically visible in this exporter after adding them there).

The configuration for this exporter can be found in the [config.json](/config.json) file. You can edit that file to change the display name of this exporter, media type, etc. See also the documentation of the [dataverse-transformer-exporter](https://github.com/ErykKul/dataverse-transformer-exporter/) for more details on the configuration file and the internal workings of this exporter, like available for transformations metadata, used JavaScript files, etc.

If you wish to edit the transformations of this exporter or make a new exporter, similar to this one, see the documentation of the [json-transformer](https://github.com/erykKul/json-transformer) library, as used by the [dataverse-transformer-exporter](https://github.com/ErykKul/dataverse-transformer-exporter/).

## Installation

If not yet configured, set the [dataverse-spi-exporters-directory](https://guides.dataverse.org/en/latest/installation/config.html#dataverse-spi-exporters-directory) configuration value first. Then `cd` into that directory and make the new `rocrate` directory:

```shell
mkdir rocrate
```

Download the [config.json](/config.json) and the [transformer.json](/transformer.json) files into that new directory:

```shell
wget -O rocrate/config.json https://raw.githubusercontent.com/gdcc/exporter-ro-crate/main/config.json
wget -O rocrate/transformer.json https://raw.githubusercontent.com/gdcc/exporter-ro-crate/main/transformer.json
```

Download the [dataverse-transformer-exporter](https://github.com/ErykKul/dataverse-transformer-exporter/) jar file from the [Maven Central repository](https://central.sonatype.com/artifact/io.github.erykkul/dataverse-transformer-exporter/versions) and save it under the same name (`rocrate.jar`) as the newly created directory (`rocrate`):

```shell
wget -O rocrate.jar https://repo1.maven.org/maven2/io/github/erykkul/dataverse-transformer-exporter/1.0.0/dataverse-transformer-exporter-1.0.0-jar-with-dependencies.jar
```

After restarting the Dataverse, you should be able to use the newly installed RO-Crate exporter:


