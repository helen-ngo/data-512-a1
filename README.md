# A1: Data Curation Assignment

## Background and Goals
Wikipedia is a collection of free online encyclopedias in various languages, and perhaps the most well-known name in the encyclopedia market. Just how popular is English Wikipedia? To answer this question, a dataset of monthly traffic on English Wikipedia can be constructed, analyzed and published like below:

![Monthly EN Wikipedia Traffic from Jan 2008 - Sep 2021](https://github.com/helen-ngo/data-512-a1/blob/main/en-wikipedia_traffic_200712-202109.png?raw=true)

## Wikimedia Foundation REST API
In order to measure Wikipedia traffic, the data will need to be collected using the Wikimedia Foundation REST API, from two different API endpoints:

* The Legacy Pagecounts API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end)) provides access to desktop and mobile traffic data from December 2007 through July 2016.

* The Pageviews API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews), [endpoint](https://wikimedia.org/api/rest_v1/#!/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.

Before using the API endpoints, please review [Wikimedia Foundation REST API
terms of use](https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions). Note that the foundation asks users to set a unique `User-Agent` or `Api-User-Agent` header that allows them to contact the user quickly. 

```
# Customize these with your own information
headers = {
    'User-Agent': 'https://github.com/first-last',
    'From': 'first-last@uw.edu'
}
```
If you use the `hcds-a1-data-curation.ipynb` Jupyter notebook to reproduce the analysis, the info in the second code cell can be changed accordingly. 

## Reproducing the Analysis
This analysis can be reproduced and updated with the latest data using `hcds-a1-data-curation.ipynb`. To recreate the analysis with the same timeframe as above, please change the first code cell to `last_month = '202109'` for September 2021, otherwise the data collection and analysis will be conducted for January 1, 2008 to the "current" last month. 

### The Data
To gather page views from all access method and both APIs, 5 separate API calls will need to be made, resulting in 5 seperate JSON source data source files. Thus the headers in the second code cell will be to be updated. For the timeframe between January 2008 - September 2021, this data and the combined final data CSV can also be accessed in the `data` folder within this repository.

The final data file is structured with the following columns and values
1. `year` - YYYY
2. `month` - MM
3. `pagecount_all_views` - total views from `pagecount_desktop_views` and `pagecount_mobile_views`
4. `pagecount_desktop_views` - number of page views accessed via desktop; output from Legacy Pagecounts API
5. `pagecount_mobile_views` - number of page views accessed via mobile; output from Legacy Pagecounts API
6. `pageview_all_views` - total views from `pageview_desktop_views` and `pageview_mobile_views`
7. `pageview_desktop_views` - number of page views accessed via desktop; output from Pageviews API
8. `pageview_mobile_views` - total number of page views accessed via mobile (web and app); output from Pageviews API

### Special Considerations
The interest of this analysis is in organic (user) traffic. Since only results from the Pageviews API can be filter by `agent=user`, the data from the Pageview API excludes spiders/crawlers, while data from the Pagecounts API does not. In addition, the Pagecounts API did not include views accessed from mobile until Ocotber 2014, thus the `pagecount_all_views` is only reflective of `pagecount_desktop_views` until then. Although`NaN`s were replaced with zeros in the final data file, the graph only shows known data. This includes only displaying data from the Legacy Pagecounts API that show the aggreation of a complete month (January 2008 - July 2016).

### Outputs
Otherwise, the notebook can be ran as-is and will produce:
* The 5 source data files in JSON format that follow the specified naming convention.
* The final data file in CSV format that follows the specified naming convention.
* An image file of the final analysis graph in .png format.

## Project License
Please view the [MIT License](https://github.com/helen-ngo/data-512-a1/blob/main/LICENSE?raw=true) for details.
