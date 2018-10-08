# Avanti Search

## Install

1. `$ bower install avanti-search --save`.
2. Install [JS-Cookie](https://github.com/js-cookie/js-cookie).
3. Insert `avanti-search.js` in your store.
4. Insert `avanti-search.css` in your store.
5. Insert VTEX search result tag `<vtex.cmc:searchResult/>` in your template.
6. Insert below script in your template at the bottom. Inside `<body>` tag:
```html
<script>
    var scriptContent = $('.resultItemsWrapper').children('script').html();
    eval('window.'+ /(PageClick_)([0-9]+)/g.exec(scriptContent)[0] +' = function () {}');

    /**
     * Avoid VTEX animation
     */
    function goToTopPage() {}
</script>
```
7. Call plugin in your JavaScript:
```javascript
(function() {
    $('.resultItemsWrapper div[id^="ResultItems"]').avantiSearch();
})();
```

## Options

##### Elements

| Option | Type | Default
|--- |--- |--- |
| $resultItemsWrapper | Element | `$('.resultItemsWrapper')`
| $script | Element | `$('.resultItemsWrapper').children('script')`
| $totalItems | Element | `$('.searchResultsTime:first .resultado-busca-numero .value')`
| $selectOrder | Element | `$('#O')`
| $filters | Element | `$('.search-multiple-navigator label')`

##### Classes

| Option | Type | Default
|--- |--- |--- |
| classFilterActive | String | `filter--active`
| classItemPreLoad | String | `shelf-item--preload`
| classLoadBtnHide | String | `load-btn--hide`
| classLoadLess | String | `load-less`
| classLoadMore | String | `load-more`
| classPagination | String | `pagination`

##### Texts

| Option | Type | Default
|--- |--- |--- |
| textLoadLess | String | `Load less`
| textLoadMore | String | `Load more`
| textPaginationFirst | String | `First`
| textPaginationPrev | String | `Prev`
| textPaginationNext | String | `Next`
| textPaginationLast | String | `Last`
| textEmptyResult | String | `No product found`

##### Pagination

| Option | Type | Default
|--- |--- |--- |
| pagination | Boolean | `false`
| paginationRangeButtons | Number | `3`

##### Others

| Option | Type | Default
|--- |--- |--- |
| cookieName | String | `AvantiSearchQuery`
| defaultParams | Object | `{}` | Pass default params to request.<br>**Example:** `{ 'query': { 'O': 'OrderByPriceASC' } }` |
| attempts | Number | `1`

**Example:**

```javascript
(function() {
    $('.resultItemsWrapper div[id^="ResultItems"]').avantiSearch({
        cookieName: 'AvantiSearchQuery',
        defaultParams: {
            'query': {
                'O': 'OrderByPriceASC'
            }
        }
    });
})();
```

## Events

| Event name | Arguments
|--- |--- |
| avantisearch.init | event, options, request
| avantisearch.emptySearch | event, options (Note: this event is triggered at `body`)
| avantisearch.initWithCookie | event, options, request
| avantisearch.initWithoutCookie | event, options, request
| avantisearch.beforeSearch | event, options, request
| avantisearch.afterSearch | event, options, request
| avantisearch.beforeChangeOrder | event, options, request, element
| avantisearch.afterChangeOrder | event, options, request, element
| avantisearch.beforeFilter | event, options, request, element
| avantisearch.afterFilter | event, options, request, element
| avantisearch.beforeChangePage | event, options, request
| avantisearch.afterChangePage | event, options, request
| avantisearch.beforeShowItems | event, options, request, page
| avantisearch.afterShowItems | event, options, request, page

**Example:**
```javascript
(function() {
    var $resultItems = $('.resultItemsWrapper div[id^="ResultItems"]');

    $resultItems
        .on('avantisearch.init', function (event, options, request) {
            console.log(event);
            console.log(options);
            console.log(request);
        });

    $resultItems.avantiSearch();
})();
```

## Tips and Tricks

1. Call the events: `avantisearch.init`, `avantisearch.initWithCookie`, `avantisearch.initWithoutCookie` or `avantisearch.beforeSearch` before the plugin start.

## Dependencies

- [JS Cookie](https://github.com/js-cookie/js-cookie)

## Contributing

- [CONTRIBUTING.md](CONTRIBUTING.md)
