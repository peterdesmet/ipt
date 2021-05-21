
---

Copyright 2015 Global Biodiversity Information Facility Secretariat

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file
except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the
License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
either express or implied. See the License for the specific language governing permissions
and limitations under the License.

---

# Release Notes

**IPT Version: 2.2**



## Upgrade instructions

### A. Performing the upgrade

**Warning 1**: Be sure to backup the IPT data directory before performing an upgrade. It is highly recommended to run scheduled backups of the IPT data directory in general.

**Warning 2**: Once an IPT has been upgraded to 2.2, it will not be possible to downgrade to an earlier version due to changes to the IPT's configuration files.

**Warning 3**: Starting with 2.2, publishers are required to assign one of three machine-readable rights declarations to their data otherwise they will not be able to register their dataset with GBIF or make it globally discoverable through GBIF.org. If publishers cannot agree to publish their data under a [CC0 1.0](http://creativecommons.org/publicdomain/zero/1.0/legalcode), [CC-BY 4.0](http://creativecommons.org/licenses/by/4.0/legalcode) or [CC-BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/legalcode) declaration, it is recommend to continue to use the previous version of the IPT for now.

An upgrade can be performed in 3 steps:

  1. Replace the previous .war file with the latest edition
  1. Backup the existing data directory
  1. Reuse the existing data directory during setup

### B. Post-upgrade instructions

Once the upgrade is complete, resource managers should assign one of [CC0 1.0](http://creativecommons.org/publicdomain/zero/1.0/legalcode), [CC-BY 4.0](http://creativecommons.org/licenses/by/4.0/legalcode) or [CC-BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/legalcode) to each of their datasets and then republish them. GBIF will begin working with existing publishers across the network during 2015 to ensure all datasets are assigned one of these three licenses For background on GBIF's new licensing policy click [here](http://www.gbif.org/terms/licences).

Only applicable to **upgrades from 2.0.5**, resource managers should check the geographic coverage is correct for each resource (if applicable). A bug in all earlier versions of the IPT caused bounding boxes to reset to global coverage following server restart on some locales. This was due to a [bug](https://code.google.com/p/gbif-providertoolkit/issues/detail?id=1043) interpreting decimal coordinates, and was been fixed already in 2.1.

### C. New Features / Other

  * IPT 2.2 now supports assigning DOIs to resources. To enable this feature, the IPT administrator must configure the IPT with a DataCite or EZID account. Please see these [instructions](IPT2ManualNotes#Configure_Organisations.md) for help. To understand how the IPT assigns DOIs to datasets, refer to the [IPT's DOI workflows](IPT2DOIWorkflow.md) page in the IPT wiki.
  * IPT 2.2 supports automatic generation of the resource citation. Please see these [instructions](IPT2ManualNotes#Citations.md) for help.
  * IPT 2.2 performs [basisOfRecord](http://rs.tdwg.org/dwc/terms/#basisOfRecord) validation on all occurrence records. The implication is that each [Occurrence](http://rs.gbif.org/core/dwc_occurrence.xml) mapping must map the [basisOfRecord](http://rs.tdwg.org/dwc/terms/#basisOfRecord) term, and each [basisOfRecord](http://rs.tdwg.org/dwc/terms/#basisOfRecord) value must match the [Darwin Core Type vocabulary](http://rs.gbif.org/vocabulary/dwc/basis_of_record.xml).
  * IPT 2.2 publishes resource metadata using a new version of the [GBIF Metadata Profile (v1.1)](http://rs.gbif.org/schema/eml-gbif-profile/1.1/). Publishers can now take advantage of the following changes:
    * it is possible to enter multiple resource contacts, creators, metadata providers, and project personnel
    * it is possible to enter multiple collections and multiple specimen preservation methods
    * it is possible to enter an identifier and description for a project
    * it is possible to specify the update frequency of a dataset using a controlled vocabulary or providing a general description
    * it is possible to store a machine readable license (storing both the URL and title of the license)
  * IPT 2.2 fixes a longstanding [bug](https://code.google.com/p/gbif-providertoolkit/issues/detail?id=817) when running the IPT using an Apache Reverse Proxy. Please refer to the improved [Server Preparation](IPTServerPreparation.md) wiki page for assistance using a reverse proxy or virtual host name for your IPT instance.
  * A new [guide](IPT2ApplyingLicense.md) on how to apply a license to a dataset has been added to the IPT wiki.

## Dependency Notes

This new version has been tested and designed to work on Tomcat 6.0 and Tomcat 7.0. Since 2.1 the IPT no longer supports Java 5, and is designed to run on Java 6 or later. The IPT will end support for Java 6 in 2015, so please be proactive and plan a Java upgrade on your server soon.

## Viewing the IPT change log

This version addressed a total of 74 issues: 20 Defects, 26 Enhancements, 16 Won't fix, 6 Duplicates, 2 Other, 1 Task, and 3 that were considered as Invalid.
These are detailed in the [issue tracking system](https://code.google.com/p/gbif-providertoolkit/issues/list?can=1&q=Milestone=Release2.2&sort=type)

## When all else fails

See the [FAQ](FAQ.md), which continues to be updated with good questions.