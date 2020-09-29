---
title: Synonyms
description: Defines the file format and structure for synonym data in MAKES
ms.topic: reference
ms.date: 8/5/2020
---

# Synonym files

Synonyms map equivalent terms that implicitly expand the scope of a query, without users having to know canonical terms. For example, given an entity with a string attribute "pet_type" having the canonical value of "canine" we could define the synonyms "dog" and "puppy" which would allow queries containing any of the terms "canine", "dog" or "puppy" to match the entity.

## Synonym data file format

Synonyms are defined on a per-entity attribute basis, with the schema attribute "synonyms" value representing the name of the synonym data file. The data file is simply a list of string tuples, with the first item representing a canonical value the second item a synonymous value:

``` JSON
["canonical_value1", "synonymous_value1"]
["canonical_value2", "synonymous_value1"]
["canonical_value2", "synonymous_value2"]
["canonical_value3", "synonymous_value3"]
```

> [!NOTE]
> Synonym mappings are many-to-many, meaning a single canonical value can have multiple synonymous values and conversely a single synonymous value can have multiple canonical values.

> [!NOTE]
> A single synonym data file can be used for multiple *different* entity attributes. A common use case for this are full-text attributes, where word stems are used as canonical values and [lemmatized forms](https://en.wikipedia.org/wiki/Lemmatisation) of the stem are used as synonyms.

## Example

### Academic author name synonyms

Person names are a great use case for synonyms, as they can have a variety of transformations (i.e. abbreviation, reversal, truncation, etc.) applied to them.

This is especially true for the academic space, where different bibliographic styles can use significantly different author naming schemes. The following is an example of synonyms for the [academic author "David S Rosenblum"](https://academic.microsoft.com/search?q=David%20S%20Rosenblum&f=&orderBy=0&skip=0&take=10).

``` JSON
["david s rosenblum", "david rosenblum"]
["david s rosenblum", "rosnblum david"]
["david s rosenblum", "d rosenblum"]
["david s rosenblum", "rosenblum d"]
["david s rosenblum", "d s rosenblum"]
["david s rosenblum", "rosenblum d s"]
```