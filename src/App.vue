<template>
  <div>
    <header class="header">
      <h1 class="header-title"><a href="/">Vue InstantSearch v2 starter</a></h1>
      <p class="header-subtitle">
        using
        <a href="https://github.com/algolia/vue-instantsearch">
          Vue InstantSearch
        </a>
      </p>
    </header>

    <div class="container">
      <ais-instant-search
          :search-client="searchClient"
          index-name="products"
      >
        <ais-index index-name="by-monthly-price">
          <div class="search-panel">
            <div class="search-panel__filters">
              <div class="search-panel__filters">
                <p>Collections</p>
                <ais-refinement-list attribute="attributes.collection" not_searchable/>
              </div>
              <div>
                <p>Categories</p>
                <ais-refinement-list attribute="product_categories" not_searchable/>
              </div>
              <div>
                <p>Monthly price</p>
                <ais-range-input attribute="pricing.monthly_price"/>
              </div>
              <div>
                <p>Ratings</p>
                <ais-rating-menu attribute="attributes.rating.stars"/>
              </div>
            </div>

            <div class="search-panel__results">
              <ais-search-box placeholder="Search here…" class="searchbox"/>
              <ais-infinite-hits>
                <template slot="item" slot-scope="{ item }">
                  <h1><a :href="item.url">
                    <ais-highlight :hit="item" attribute="name"/>
                  </a></h1>
                  <img :src="item.default_thumbnail"/>
                  <p>
                    <span>Monthly price: </span>
                    <ais-highlight :hit="item" attribute="monthly_price"/>
                  </p>
                  <p>
                    <ais-highlight :hit="item" attribute="description"/>
                  </p>
                </template>
              </ais-infinite-hits>

              <div class="pagination">
                <ais-pagination/>
              </div>
            </div>
          </div>
        </ais-index>
      </ais-instant-search>
    </div>
  </div>
</template>

<script>
import algoliasearch from 'algoliasearch/lite';
import 'instantsearch.css/themes/algolia-min.css';

export default {
  data() {
    return {
      searchClient: algoliasearch(
          'A8SGWMDCFY',
          'eb5df253ecb2f26cb02d394226e316bc'
      ),
    };
  },
};
</script>

<style>
body,
h1 {
  margin: 0;
  padding: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
  Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
}

.header {
  display: flex;
  align-items: center;
  min-height: 50px;
  padding: 0.5rem 1rem;
  background-image: linear-gradient(to right, #4dba87, #2f9088);
  color: #fff;
  margin-bottom: 1rem;
}

.header a {
  color: #fff;
  text-decoration: none;
}

.header-title {
  font-size: 1.2rem;
  font-weight: normal;
}

.header-title::after {
  content: ' ▸ ';
  padding: 0 0.5rem;
}

.header-subtitle {
  font-size: 1.2rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem;
}

.search-panel {
  display: flex;
}

.search-panel__filters {
  flex: 1;
  margin-right: 1em;
}

.search-panel__results {
  flex: 3;
}

.searchbox {
  margin-bottom: 2rem;
}

.pagination {
  margin: 2rem auto;
  text-align: center;
}
</style>
