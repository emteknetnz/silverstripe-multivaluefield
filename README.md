# Silverstripe MultiValueField module

[![CI](https://github.com/symbiote/silverstripe-multivaluefield/actions/workflows/ci.yml/badge.svg)](https://github.com/symbiote/silverstripe-multivaluefield/actions/workflows/ci.yml)
[![Silverstripe supported module](https://img.shields.io/badge/silverstripe-supported-0071C4.svg)](https://www.silverstripe.org/software/addons/silverstripe-commercially-supported-module-list/)

A database field type that allows the storage of multiple discrete values in
a single database field. This also provides form fields for entering multiple
values in a simple manner

* MultiValueTextField - displays a text field. When data is entered, another
  text field is displayed directly beneath. Subsequent data entry triggers
  more text fields to appear
* MultiValueDropdownField - displays a dropdown field. When a value is selected
  another dropdown field is displayed.

Within templates, the field can be iterated over as per a data object set.
The property $Value is available as a Varchar type, and other typical
properties such as $FirstLast etc are inherited from ViewableData.

Data is stored in the database in a serialized PHP format. While this is not
ideal for searching purposes, some external indexing engines (eg the Solr
module) are aware of the field type and will index accordingly.

## Installation

```sh
composer require symbiote/silverstripe-multivaluefield
```

## Basic Usage

As with all DB fields

```php
private static $db = [
    'Keywords' => 'MultiValueField',
];
```

To make use of the field on the frontend, you can loop over the Items property

```html
<% loop $Keywords.Items %>
    <p>$Key $Value</p>
<% end_loop %>
```

In this case, `$Value` is a Varchar object, so you can call all relevant string field methods on it, such as `$Value.Raw`, `$Value.LimitWordCount` etc etc.

Note that to have the `$Key` value available as something other than an integer, use the `KeyValueField` field type to populate the field.

You can set the key and value placeholder values of the KeyValueField in your field like this:

```php
$kvf = KeyValueField::create(
    'MultiChoiceAnswer',
    'Multiple Choice Answers'
);
$kvf->setValueFieldPlaceholder('Value');
$kvf->setKeyFieldPlaceholder('Label');
```

## Maintainer Contacts

* Marcus Nyeholt <marcus@symbiote.com.au>

## Contributing

### Thanks

* [Ingo's initial work](https://github.com/symbiote/silverstripe-multivaluefield/pull/44) to getting this SS4 ready
* [muskie9's work](https://github.com/muskie9) on updating UI fields

### Translations

Translations of the natural language strings are managed through a third party translation interface, transifex.com. Newly added strings will be periodically uploaded there for translation, and any new translations will be merged back to the project source code.

Please use [https://app.transifex.com/silverstripe/silverstripe-multivaluefield/](https://app.transifex.com/silverstripe/silverstripe-multivaluefield/) to contribute translations, rather than sending pull requests with YAML files.

## License

This module is licensed under the BSD license at https://silverstripe.org/BSD-license

## Project Links
* [GitHub Project Page](https://github.com/nyeholt/silverstripe-multivaluefield)
* [Issue Tracker](https://github.com/nyeholt/silverstripe-multivaluefield/issues)

