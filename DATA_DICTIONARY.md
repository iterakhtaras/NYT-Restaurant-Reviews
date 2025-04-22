# Data Dictionary

This document describes the schema and transformations for each dataset used in this project.

## Raw Data (`data/raw`)

### nyt_reviews.csv
| Column               | Type    | Description                                         | Source      |
|----------------------|---------|-----------------------------------------------------|-------------|
| `review_id`          | integer | Unique identifier for each NYT restaurant review    | NYT Scraper |
| `restaurant_name`    | text    | Name of the reviewed restaurant                     | NYT Scraper |
| `address`            | text    | Street address of the restaurant                    | NYT Scraper |
| `borough`            | text    | NYC borough where the restaurant is located         | NYT Scraper |
| `publishing_date`    | date    | Date the review was published                       | NYT Scraper |
| `critics_pick`       | boolean | Whether the review was labeled a “Critics’ Pick”    | NYT Scraper |
| `full_review_text`   | text    | Complete text of the review                         | NYT Scraper |

### census_nyc_county.csv
| Column                       | Type    | Description                                                 | Source                  |
|------------------------------|---------|-------------------------------------------------------------|-------------------------|
| `county_name`                | text    | Name of the NYC county (e.g., New York, Kings, Queens)      | U.S. Census API        |
| `total_population`           | integer | Total county population                                      | U.S. Census API        |
| `south_asian_population`     | integer | Estimated South Asian population                             | U.S. Census API        |
| `median_household_income`    | integer | Median household income                                      | U.S. Census API        |

## Processed Data (`data/processed`)

### merged_reviews.csv
| Column               | Type    | Description                                                | Transformation                              |
|----------------------|---------|------------------------------------------------------------|---------------------------------------------|
| `review_id`          | integer | Unique review ID                                           | From `nyt_reviews.csv`                      |
| `restaurant_name`    | text    | Restaurant name                                            | From `nyt_reviews.csv`                      |
| `borough`            | text    | Borough                                                    | Standardized casing and spelling            |
| `publishing_date`    | date    | Publishing date                                            | Parsed using `pd.to_datetime()`             |
| `critics_pick`       | boolean | Critics’ Pick flag                                         | From `nyt_reviews.csv`                      |
| `full_review_text`   | text    | Raw review text                                            | From `nyt_reviews.csv`                      |
| `county_name`        | text    | Mapped county based on geocoded borough                   | Added via merge with census data            |
| `total_population`   | integer | County population                                         | From `census_nyc_county.csv`                |
| `median_household_income` | integer | Median household income                                | From `census_nyc_county.csv`                |

### modeling_dataset.csv
| Column               | Type    | Description                                                | Transformation                              |
|----------------------|---------|------------------------------------------------------------|---------------------------------------------|
| All columns from `merged_reviews.csv`                                            | Combined features                             |
| `review_sentiment`    | float   | Sentiment score for review text                           | Computed with an NLP pipeline (e.g., spaCy) |
| `word_count`         | integer | Number of words in the review                             | Text preprocessing                          |
| `critics_pick_flag`  | integer | Binary flag (1 if Critics’ Pick, 0 otherwise)             | Encoded boolean                             |

