# Hyvä Themes - GraphQL ViewModel module

**Note: This module is currently experimental and might be removed or changed without notice**

[![Hyvä Themes](https://repository-images.githubusercontent.com/300568807/f00eb480-55b1-11eb-93d2-074c3edd2d07)](https://hyva.io/)

## hyva-themes/magento2-graphql-view-model

![Supported Magento Versions][ico-compatibility]

This module adds a GraphQL ViewModel to allow GraphQL queries and mutations to be customized before they are rendered in the output.

Compatible with Magento 2.3.4 and higher.

## What does it do?

It adds:
 - `\Hyva\GraphqlViewModel\ViewModel\GraphqlViewModel`, to be accessed via the view model registry.
   The method `GraphqlViewModel::toAst` and `GraphqlViewModel::query` can be used as plugin targets.
- `\Hyva\GraphqlViewModel\Model\GraphqlQueryEditor` which can be used to add fields and arguments to GraphQL queries.
 - The event `hyva_graphql_query_before_render`
   Event observers receive the parsed query that can be manipulated with the `GraphqlQueryEditor`

## Usage

In a `.phtml` template, to make a query customizable, wrap it in the `GraphqlViewModel::query()` method:
```
$query = $gqlViewModel->query("product_query", "
products(filter: {} pageSize: 20) {
  items {
    {$type}_products {
        sku
        id
        small_image {
          url
        }
    }
  }
}");
<?= $query ?>
```
The first argument is used to identify a query in event observers or plugins.

## Installation
  
1. Install via composer
    ```
    composer config repositories.hyva-themes/magento2-graphql-view-model git git@github.com:hyva-themes/magento2-graphql-view-model.git
    composer require hyva-themes/magento2-graphql-view-model
    ```
2. Enable module
    ```
    bin/magento setup:upgrade
    ```
## Configuration
  
No configuration needed.

## License

The MIT License (MIT). Please see [License File](LICENSE.txt) for more information.

[ico-compatibility]: https://img.shields.io/badge/magento-%202.3%20|%202.4-brightgreen.svg?logo=magento&longCache=true&style=flat-square
