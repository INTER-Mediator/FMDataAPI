# FMDataAPI Ver.25 [![Build Status](https://github.com/msyk/FMDataAPI/actions/workflows/php.yml/badge.svg)](https://github.com/msyk/FMDataAPI/actions/workflows/php.yml)

by Masayuki Nii (nii@msyk.net)

FMDataAPI is a class developed in PHP to access FileMaker database
with Claris FileMaker Data API.

## Contributers

They created pull requests. Thanks for cooperating.

- Atsushi Matsuo
- darnel
- Craig Smith
- Bernhard Schulz
- montaniasystemab
- Rickard Andersson
- Julien @AnnoyingTechnology
- Tom Kuijer

## At a Glance

The FileMaker database named "TestDB.fmp12" is hosted on localhost, and
it set the "fmrest" as access privilege. The account to connect with REST API is "web"
and "password". This database has the layout named "person_layout", and you
can use the layout name as a property of the FMDataAPI instance. The return
value of the "query" method is Iterator and can repeat in foreach statement
with each record in the query result. This layout has the field named
"FamilyName" and "GivenName", and can use the field name as a property.

```
$fmdb = new FMDataAPI("TestDB", "web", "password");
$result = $fmdb->person_layout->query();
foreach ($result as $record) {
    echo "name: {$record->FamilyName}, {$record->GivenName}";
}
```

For more details, I'd like to read codes and comments in file samples/FMDataAPI_Sample.php.

API Document is here:
https://inter-mediator.info/FMDataAPI/packages/INTER-Mediator-FileMakerServer-RESTAPI.html
## What's This?

The FileMaker Data API is the new feature of FileMaker Server 16,
and it's the API with REST-based database operations.
Although the Custom Web Publishing is the way to access the database
for a long while, FileMaker Inc. has introduced the modern feature to operate
the database. The current version of FMDataAPI works on just FileMaker 18 and 19 platform.

For now, I'm focusing to develop the web application framework "INTER-Mediator"
(https://inter-mediator.com/ or https://github.com/INTER-Mediator/INTER-Mediator.git)
which can develop the core features of database-driven web application
with declarative descriptions. INTER-Mediator has already supported the Custom
Web Publishing with FX.php, and I develop codes here for support REST APIs.

Bug reports and contribution are welcome.

## Installing to Your Project

FMDataAPI has "composer.json," so you can add your composer.json file in your project as below.

```
...
"require": {
  ...
  "inter-mediator/fmdataapi":"25"
} ...
```

## About Files and Directories

- src/FMDataAPI.php
    - The core class, and you just use this for your application.
     This class and supporting classes are object-oriented REST API
     wrappers.
- src/Supporting/*.php
    - The supporting classes for the FMDataAPI class. Perhaps you don't need to create these classes, but you have to handle methods on them.
- composer.json, composer.lock
    - Composer information files.
- Sample_results.ipynb
    - Sample program and results with Jupyter Notebook style. Sorry for slight old version results.
- samples/FMDataAPI_Sample.php and cat.jpg
    - This is the sample program of FMDataAPI class, and shows how to
    use FMDataAPI class. It includes rich comments,
    but Sample_results.ipynb is more informative.
- README.md, .gitignore
    - These are for GitHub.
- test
    - Some files for unit testing.
- .github, docker-compose.yml, Dockerfile
    - For the GitHub action with testing.

## Licence

MIT License

## Acknoledgement

- Thanks to Atsushi Matsuo. Your script is quite helpful to implement the "localserver" feature.
(https://gist.github.com/matsuo/ef5cb7c98bb494d507731886883bcbc1) Moreover thanks for updating and fixing bugs.
- Thanks to Frank Gonzalez. Your bug report is brilliant, and I could fix it quickly.
- Thanks to base64bits for coding about container field.
- Thanks to phpsa for bug fix.
- Thanks to Flexboom for bug fix.
- Thanks to schube for bug fix.
- Thanks to frankeg for bug fix.

## History

- April 2017: Start to create these classes and codes.
- 2017-05-05: README.md added.
- 2017-05-26: [Ver.2] Support the "localserver" as host name.
- 2017-05-31: [Ver.3] The query() method of FileMakerLayout class fixed.
'Offset' and 'range' parameters could not set as an integer value.
- 2017-11-06: [Ver.4] The getFieldNames() and getPortalNames() methods added.
- 2018-02-03: [Ver.5] Bug fix of sorting parameters in query method.
- 2018-02-18: [Ver.6] Bug fix of creating record with no default value.
- 2018-03-25: [Ver.7] getSessionToken method added. OAuth handling implemented but not well debugged.
- 2018-05-09: The Version 7 is the last version which supports FileMaker 16-based Data API.
---
- 2018-05-15: [Ver.8] Update for FileMaker 17. FileMaker Data API v1 is supported from this version.
   The preview version of FileMaker Data API doesn't support anymore.
- 2018-05-27: [Ver.9] composer.json is added, and can install "inter-mediator/fmdataapi".
   FMDataAPITrial directory deleted because it's already discontinued api.
   Add the "samples" directory and move sample files into it.
- 2018-06-22: [Ver.10] Added the getContainerData method (Thanks to base64bits!),
   bug fix (Thanks to phpsa!).
- 2018-07-22: [Ver.11] Global field methods bug fixed and were available in FMDataAPI class (Tanks to Mr.Matsuo).
   The script errors and results can get from methods in FMLayout class.
- 2018-07-29: [Ver.12] Bug fix for UUID Supporting (Thanks to Mr.Matsuo).
   Unit tests implemented but now for limited methods, als integrating Travis CI.
- 2018-11-13: [Ver.13]
    Added getDebugInfo method (Thanks to Mr.Matsuo),
    modified and fixed the getFieldNames method (Thanks to phpsa),
    fixed handling portal object name (Thanks to Mr.Matsuo)
    fixed the getModId method (Thanks to Flexboom)
- 2018-11-17: [Ver.15]
    Jupyter Notebook style sample and results.
- 2019-05-19: [Ver.16]
    This is the final version for FileMaker 17 platform, and bug fix (Thanks to darnel)
---
- 2019-05-20: [Ver.17]
    Support the FileMaker 18 platform.
    Add getMetadataOld() and getMetadata() to FileMakerLayout class.
    Add getProductInfo(), getDatabaseNames(), getLayoutNames() and getScriptNames() to FMDataAPI class.
- 2019-05-27: [Ver.18]
    Add getTargetTable(), getTotalCount(), getFoundCount(), getReturnedCount() to FileMakerRelation class.
    Add getTargetTable(), getTotalCount(), getFoundCount(), getReturnedCount() to FMDataAPI class.
- 2019-09-12: [Ver.19]
    Add the duplicate() method to the FileMakerLayout class. Thanks to schube.
- 2019-09-16: [Ver.20]
    The default values  of limit and range parameters changed to 0 and both just applied for over 0 values. Thanks to schube.
- 2020-08-23: [Ver.21]
    Bug fix about the field referencing of a related field without any portals. Thanks to frankeg.
    Checked on the FileMaker Server 19.
- 2021-02-10: [Ver.22]
    Setting the timeout value about cURL. Thanks to @montaniasystemab. Also thanks to @AnnoyingTechnology for correcting.
- 2021-02-10: [Ver.23]
  File structure is updated for PSR-4. Thanks to tkuijer.
- 2021-12-23: [Ver.24]
  Bug fix for portal limit parameter. Thanks to tkuijer.
- 2022-03-24: [Ver.25]
  Add methods(getFirstRecord, getLastRecord, getRecords) to the FileMakerRelation class.

## API Differences between ver.8 and 7.
### FMDataAPI class
The setAPIVersion method added. This is for a future update of FileMaker Data API.
As far as FMDataAPI Ver.8 goes, This isn't required.
- public function __construct($solution, $user, $password, $host = NULL, $port = NULL, $protocol = NULL, [New]$fmDataSource = null)
- [New]public function setAPIVersion($vNum)

### FileMakerRelation class
The following methods added to script parameters. See the query method's document for specifying it.
Twe methods added to portal parameter.

- public function query($condition = NULL, $sort = NULL, $offset = -1, $range = -1, $portal = null, [New]$script = null)
- public function getRecord($recordId, $portal = null, [New]$script = null)
- public function create($data = null, [New]$portal = null, [New]$script = null)
- public function delete($recordId, [New]$script = null)
- public function update($recordId, $data, $modId = -1, [New]$portal = null, [New]$script = null)
- [New]public function uploadFile($filePath, $recordId, $containerFieldName, $containerFieldRepetition = null, $fileName = null)
