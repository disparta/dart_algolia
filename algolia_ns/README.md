# Algolia Search (Dart Client)
**[UNOFFICIAL]** Algolia is a pure dart SDK, wrapped around Algolia REST API for easy implementation for your Flutter or Dart projects.

[![pub package](https://img.shields.io/pub/v/algolia.svg)](https://pub.dartlang.org/packages/algolia)

[Pub](https://pub.dartlang.org/packages/algolia) - [API Docs](https://pub.dartlang.org/documentation/algolia/latest/) - [GitHub](https://github.com/knoxpo/dart_algolia)

## Features
- Query / Search
- Get Object
- Add Object
- Add Objects
- Replace all objects in an Index
- Update Object
- Partial Update Object
- Delete Object
- Perform Batch Activities
- Add Index
- Delete Index
- Clear Index
- Copy Index
- Move Index
- Index Settings

## Version compatibility
See CHANGELOG for all breaking (and non-breaking) changes.

## Become Contributor
If you wish to contribute in our development process, refer to our [Contributing Guidelines](https://github.com/knoxpo/dart_algolia/blob/master/CONTRIBUTING.md)

## Getting started
You should ensure that you add the router as a dependency in your flutter project.
```yaml
dependencies:
 algolia: ^0.1.6+1
```
You should then run `flutter packages upgrade` or update your packages in IntelliJ.


## Example Project
There is a pretty sweet example project in the `example` folder. Check it out. Otherwise, keep reading to get up and running.


## Setting up
```dart
  ///
  /// Initiate static Algolia once in your project.
  ///
  class Application {
    static final Algolia algolia = Algolia.init(
      applicationId: 'YOUR_APPLICATION_ID',
      apiKey: 'YOUR_API_KEY',
    );
  }
  
  void main() async {
    ///
    /// Initiate Algolia in your project
    ///
    Algolia algolia = Application.algolia;

    ///
    /// Perform Query
    ///
    AlgoliaQuery query = algolia.instance.index('contacts').search('john');

    // Perform multiple facetFilters
    query = query.setFacetFilter('status:published');
    query = query.setFacetFilter('isDelete:false');

    // Get Result/Objects
    AlgoliaQuerySnapshot snap = await query.getObjects();

    // Checking if has [AlgoliaQuerySnapshot]
    print('Hits count: ${snap.nbHits}');

    ///
    /// Perform Index Settings
    ///
    AlgoliaIndexSettings settingsRef = algolia.instance.index('contact').settings;

    // Get Settings
    Map<String, dynamic> currentSettings = await settingsRef.getSettings();

    // Checking if has [Map]
    print('\n\n');
    print(currentSettings);

    // Set Settings
    AlgoliaSettings settingsData = settingsRef;
    settingsData = settingsData.setReplicas(const ['index_copy_1', 'index_copy_2']);
    AlgoliaTask setSettings = await settingsData.setSettings();

    // Checking if has [AlgoliaTask]
    print('\n\n');
    print(setSettings.data);
  }
```

## Search Parameters
Here is the list of parameters you can use with the search method (search scope).
We have managed to include most commonly used parameters for search functionality
and there many more to be added in future releases.

We have indicated counts of queryable parameters with their availability status
on official Algolia website and what we have managed to support it in this
version of the release. 

##### search (1/1)
- `.search(String value)`

##### attributes (2/2)
- `.setAttributesToRetrieve(List<String> value)`
- `.setRestrictSearchableAttributes(List<String> value)`

##### filtering (6/6)
- `.setFilters(String value)`
- `.setFacetFilter(dynamic value)` This can be used multiple times in a query.
- `.setOptionalFilter(String value)` This can be used multiple times in a query.
- `.setNumericFilter(String value)` This can be used multiple times in a query.
- `.setTagFilter(String value)` This can be used multiple times in a query.
- `.setSumOrFiltersScore(bool value)`

##### faceting (4/4)
- `.setFacets(List<String> value)`
- `.setMaxValuesPerFacet(int value)`
- `.setFacetingAfterDistinct({bool enable = true})`
- `.setSortFacetValuesBy(AlgoliaSortFacetValuesBy value)`

##### highlighting-snippeting (6/6)
- `.setAttributesToHighlight(List<String> value)`
- `.setAttributesToSnippet(List<String> value)`
- `.setHighlightPreTag(String value)`
- `.setHighlightPostTag(String value)`
- `.setSnippetEllipsisText(String value)`
- `.setRestrictHighlightAndSnippetArrays({bool enable = true})`

##### pagination (4/4)
- `.setPage(int value)`
- `.setHitsPerPage(int value)`
- `.setOffset(int value)`
- `.setLength(int value)`

##### typos (5/5)
- `.setMinWordSizeFor1Typo(int value)`
- `.setMinWordSizeFor2Typos(int value)`
- `.setTypoTolerance(dynamic value)`
- `.setAllowTyposOnNumericTokens(bool value)`
- `.setDisableTypoToleranceOnAttributes(List<String> value)`

##### geo-search (7/7)
- `.setAroundLatLng(String value)`
- `.setAroundLatLngViaIP(bool value)`
- `.setAroundRadius(dynamic value)`
- `.setAroundPrecision(int value)`
- `.setMinimumAroundRadius(int value)`
- `.setInsideBoundingBox(List<BoundingBox> value)`
- `.setInsidePolygon(List<BoundingPolygonBox> value)`

##### languages (0/3)

##### query-rules (0/2)

##### query-strategy (0/7)

##### advanced (0/11)

##### GET RESULT
- `.getObjects()`


## Settings Parameters
Here is the list of parameters you can use with the settings method (settings scope).
We have managed to include most commonly used parameters for settings functionality
and there many more to be added in future releases.

We have indicated counts of settings parameters with their availability status
on official Algolia website and what we have managed to support it in this
version of the release. 

##### attributes (4/4)
- `.setSearchableAttributes(List<String> value)`
- `.setAttributesForFaceting(List<String> value)`
- `.setUnretrievableAttributes(List<String> value)`
- `.setAttributesToRetrieve(List<String> value)`

##### ranking (3/3)
- `.setRanking(List<String> value)`
- `.setCustomRanking(List<String> value)`
- `.setReplicas(List<String> value)`

##### faceting (2/2)
- `.setMaxValuesPerFacet(int value)`
- `.setSortFacetValuesBy(AlgoliaSortFacetValuesBy value)`

##### highlighting-snippeting (6/6)
- `.setAttributesToHighlight(List<String> value)`
- `.setAttributesToSnippet(List<String> value)`
- `.setHighlightPreTag(String value)`
- `.setHighlightPostTag(String value)`
- `.setSnippetEllipsisText(String value)`
- `.setRestrictHighlightAndSnippetArrays({bool enable = true})`

##### pagination (2/2)
- `.setHitsPerPage(int value)`
- `.setPaginationLimitedTo(int value)`

##### typos (7/7)
- `.setMinWordSizeFor1Typo(int value)`
- `.setMinWordSizeFor2Typos(int value)`
- `.setTypoTolerance(dynamic value)`
- `.setAllowTyposOnNumericTokens(bool value)`
- `.setDisableTypoToleranceOnAttributes(List<String> value)`
- `.setDisableTypoToleranceOnWords(List<String> value)`
- `.setSeparatorsToIndex(List<String> value)`

##### languages (0/3)

##### query-rules (0/2)

##### query-strategy (0/7)

##### performance (0/2)

##### advanced (4/11)
- `.setAttributeForDistinct(String value)`
- `.setDistinct({dynamic value = 0})`
- `.setGetRankingInfo({bool enabled = true})`
- `.setClickAnalytics({bool enabled = false})`

##### GET Settings
- `.getSettings()`

##### SET Settings
- `.setSettings()`


<hr/>
Algolia [Unofficial SDK for Dart] is a Knoxpo original.
<br/>
<a href="https://knoxpo.com" target="_knoxpo"><img src="https://www.knoxpo.com/assets/logo.png" width="80"></a>
