# DOI usage for LSST Data Releases

```{abstract}
Each LSST Data Release has to be associated with dataset DOIs.
This document will describe the motivation and policy for issuing DOIs for Data Releases.
```

## Digital Object Identifiers in Publications

The AAS [strongly recommend](https://journals.aas.org/data-guide/) that all papers submitted to their journals follow the best practices outlined in {cite:t}`2022ApJS..260....5C`.
This includes the following exhortation (from section 5.4):

> Use DOIs to cite related content if available.
> This includes specific data sets, software, and services used to produce results in the published articles.
> Archive these in persistent repositories and link them to the article through DOIs minted by the repositories.
> The DOI links should be included in the bibliography to ensure proper citation, and also be put where the data are discussed to make it easier for readers to locate and access the data.

Furthermore, when submitting a paper the author is explicitly asked for dataset DOIs as part of the process.
This indicates that we should ensure that sufficient DOIs are created for LSST Data Releases to and that we are clear with the community that they should be used.
DOIs for datasets are extremely useful for citation tracking, if used properly, and will provide us with additional metrics on scientific output from the observatory over and above relying on citations for the data release papers: a citation of the data release dataset implies actual usage of the data whereas as a citation of the data release paper may simply be included as part of a discussion of the survey.

## Issuing DOIs

The [Department of Energy Office of Scientific and Technical Information](https://www.osti.gov) provides to DOE grant holders the ability to issue DOIs through their E-Link service.
Given that the NSF-DOE Vera C. Rubin Observatory is part-funded by the DOE we are allowed to use this mechanism to issue DOIs.
For instrument and dataset DOIs it was agreed that we are allowed to use `lsst.io` as the formal landing pages for each DOI.

## Instrument DOIs

OSTI allows instrumentation to be given DOIs.
Doing this allows us to reference all our data releases to the instrument that generated the data.
This is an extremely useful way to anchor the observatory outputs and science users should be encouraged to cite the instrument DOI explicitly.

## Data Release DOIs

Rubin Observatory plans to make annual data releases of the Legacy Survey of Space and Time {cite:p}`2019ApJ...873..111I`.
There will always be an umbrella DOI issued for each data release *as a whole*.
From a citation tracking perspective this is the minimum requirement, but we know that there will be very few papers published that really make use of the full set of imaging and catalog data.
Furthermore, Independent Data Access Centers (IDACs) {cite:p}`RTN-003` are not going to be taking copies of full data release and instead are likely to restrict their holdings to, for example, the object catalog and deep coadd images, or even a version of the object catalog with a subset of the columns
(sometimes called "Object Lite").
IDACs will be encouraged to create DOIs for their holdings that explicitly link back to the primary data release archive.
To enable this we intend to issue DOIs to every catalog (object, source, forced source, etc) and every Data Butler {cite:p}`2022SPIE12189E..11J` dataset type (visit images, difference images, co-adds).

An open question is whether to create DOIs for "virtual" Butler data products that can be regenerated on demand.

### Relationships

DOIs much more useful if relationships to other DOIs are specified in the metadata.
[DataCite](https://support.datacite.org/docs/connecting-to-works) and [Crossref](https://www.crossref.org/documentation/schema-library/markup-guide-metadata-segments/relationships/) specify how relationships between DOIs are specified and we will relate release, dataset, and instrument DOIs in the following ways:

* The data release dataset "isCollectedBy" the instrument.
* The catalog and dataset type component DOIs will be declared as "isPartOf" the main data release DOI.
* If an IDAC creates a DOI for their copy of a component they shall use "isVariantFormOF" the original dataset even if the copy is identical.[^identical]
  They shall not use "isPartOf".
* If an IDAC has a cut down version of a catalog (e.g., "object lite") then that version "isVariantFormOf" the original full catalog.
* If a data release includes Butler datasets that contain tabular data (for example in Parquet files) that are also available as catalogs in Qserv, then the catalog DOI "isVariantFormOf" the Butler dataset to indicate that they are almost, but not exactly, the same data and that the parquet files are the original form.
* A new data release "Obsoletes" a previous data release.[^dp1]
* A new release's catalog dataset (e.g., "Object") also "Obsoletes" the corresponding catalog dataset in the previous release.

## Data Preview 1

Data Preview 1 (DP1) {cite:p}`RTN-095,RTN-085` was released to the data rights holders on June 20th, 2025.
This was the first data release from Rubin and we created DOIs as outlined in this document.
DP1 consisted of data taken by the LSST Commissioning Camera and an instrument DOI was created for it {cite:p}`10.71929/rubin/2561361`.
We have subsequently created instrument DOIs for both LATISS {cite:p}`10.71929/rubin/2571930` and LSSTCam {cite:p}`10.71929/rubin/2571927` to prepare for future data releases.

For DP1 the following DOIs were created:

* [10.71929/rubin/2570308](https://doi.org/10.71929/rubin/2570308) (DP1) isCollectedBy [10.71929/rubin/2561361](https://doi.org/10.71929/rubin/2561361) (LSSTComCam)
* [10.71929/RUBIN/2570309](https://doi.org/10.71929/RUBIN/2570309) (butler-calibrations) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570313](https://doi.org/10.71929/RUBIN/2570313) (butler-deep_coadd) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570318](https://doi.org/10.71929/RUBIN/2570318) (butler-dia_object) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570320](https://doi.org/10.71929/RUBIN/2570320) (butler-dia_object_forced_source) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570316](https://doi.org/10.71929/RUBIN/2570316) (butler-dia_source) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570312](https://doi.org/10.71929/RUBIN/2570312) (butler-difference_image) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570324](https://doi.org/10.71929/RUBIN/2570324) (butler-object) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570326](https://doi.org/10.71929/RUBIN/2570326) (butler-object_forced_source) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570310](https://doi.org/10.71929/RUBIN/2570310) (butler-raw) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570322](https://doi.org/10.71929/RUBIN/2570322) (butler-source) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570334](https://doi.org/10.71929/RUBIN/2570334) (butler-ss_object) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570332](https://doi.org/10.71929/RUBIN/2570332) (butler-ss_source) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570315](https://doi.org/10.71929/RUBIN/2570315) (butler-survey-property) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570314](https://doi.org/10.71929/RUBIN/2570314) (butler-template_coadd) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570330](https://doi.org/10.71929/RUBIN/2570330) (butler-visit_detector_table) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570311](https://doi.org/10.71929/RUBIN/2570311) (butler-visit_image) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570328](https://doi.org/10.71929/RUBIN/2570328) (butler-visit_table) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570331](https://doi.org/10.71929/RUBIN/2570331) (tap-CcdVisit) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570319](https://doi.org/10.71929/RUBIN/2570319) (tap-DiaObject) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570317](https://doi.org/10.71929/RUBIN/2570317) (tap-DiaSource) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570327](https://doi.org/10.71929/RUBIN/2570327) (tap-ForcedSource) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570321](https://doi.org/10.71929/RUBIN/2570321) (tap-ForcedSourceOnDiaObject) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570325](https://doi.org/10.71929/RUBIN/2570325) (tap-Object) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570335](https://doi.org/10.71929/RUBIN/2570335) (tap-SSObject) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570333](https://doi.org/10.71929/RUBIN/2570333) (tap-SSSource) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570323](https://doi.org/10.71929/RUBIN/2570323) (tap-Source) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570329](https://doi.org/10.71929/RUBIN/2570329) (tap-Visit) isPartOf [10.71929/RUBIN/2570308](https://doi.org/10.71929/RUBIN/2570308) (DP1)
* [10.71929/RUBIN/2570316](https://doi.org/10.71929/RUBIN/2570316) (butler-dia_source) isOriginalFormOf [10.71929/RUBIN/2570317](https://doi.org/10.71929/RUBIN/2570317) (tap-DiaSource)
* [10.71929/RUBIN/2570318](https://doi.org/10.71929/RUBIN/2570318) (butler-dia_object) isOriginalFormOf [10.71929/RUBIN/2570319](https://doi.org/10.71929/RUBIN/2570319) (tap-DiaObject)
* [10.71929/RUBIN/2570320](https://doi.org/10.71929/RUBIN/2570320) (butler-dia_object_forced_source) isOriginalFormOf [10.71929/RUBIN/2570321](https://doi.org/10.71929/RUBIN/2570321) (tap-ForcedSourceOnDiaObject)
* [10.71929/RUBIN/2570322](https://doi.org/10.71929/RUBIN/2570322) (butler-source) isOriginalFormOf [10.71929/RUBIN/2570323](https://doi.org/10.71929/RUBIN/2570323) (tap-Source)
* [10.71929/RUBIN/2570324](https://doi.org/10.71929/RUBIN/2570324) (butler-object) isOriginalFormOf [10.71929/RUBIN/2570325](https://doi.org/10.71929/RUBIN/2570325) (tap-Object)
* [10.71929/RUBIN/2570326](https://doi.org/10.71929/RUBIN/2570326) (butler-object_forced_source) isOriginalFormOf [10.71929/RUBIN/2570327](https://doi.org/10.71929/RUBIN/2570327) (tap-ForcedSource)
* [10.71929/RUBIN/2570328](https://doi.org/10.71929/RUBIN/2570328) (butler-visit_table) isOriginalFormOf [10.71929/RUBIN/2570329](https://doi.org/10.71929/RUBIN/2570329) (tap-Visit)
* [10.71929/RUBIN/2570330](https://doi.org/10.71929/RUBIN/2570330) (butler-visit_detector_table) isOriginalFormOf [10.71929/RUBIN/2570331](https://doi.org/10.71929/RUBIN/2570331) (tap-CcdVisit)
* [10.71929/RUBIN/2570332](https://doi.org/10.71929/RUBIN/2570332) (butler-ss_source) isOriginalFormOf [10.71929/RUBIN/2570333](https://doi.org/10.71929/RUBIN/2570333) (tap-SSSource)
* [10.71929/RUBIN/2570334](https://doi.org/10.71929/RUBIN/2570334) (butler-ss_object) isOriginalFormOf [10.71929/RUBIN/2570335](https://doi.org/10.71929/RUBIN/2570335) (tap-SSObject)

although only the primary relationships are noted here.

## References

```{bibliography}
  :style: lsst_aa
```

[^dp1]: Data Preview 1 is not obsoleted by Data Preview 2 since they are completely distinct datasets.
[^identical]: "IsIdenticalTo" should only be used for cases where the DOIs point to the exact same resource, such as happens if two DOIs are issued by mistake.
