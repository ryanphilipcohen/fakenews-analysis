### 9/30/25 - Ryan Cohen

- Designed project scaffolding

### 10/1/25 - Ryan Cohen

Work

- Created environment and instructions on how to use
- Outlined the preprocessing work to be done

Questions

- Half of our data has the articles and titles, while others only have the titles. How should we go about combining our datasets for training? I think that simply concatenating the title onto the text could work as long as we confirm that it doesn't associate length with truth or falsity.

### 10/1/25 - Ryan Cohen

- Wrote a script to scrape articles for the gossicop and politifact websites and attach them to their entries. I believe the proces to be too slow, as it made it through 300 articles in 18 minutes, making the full database of 20000 articles a serious endeavor to get through. We may try this in the future if our data is insufficient. For now, we'll continue with our plan of concatenating articles to their titles if the article is present.
- Continued work on preprocessing and the typical NLP data cleaning.
- Experimented more with scraping articles and concurrent fetches to increase efficiency. I'm fairly sure that retrieving about half of those 45k articles can be done in three or four hours, leaving us with only around 22k/78-ish-k that are only titles.

### 10/6/25 - Ryan Cohen

- Figured out that we have a lot of articles already with full article text along with the title. We're fetching article data from the gossipcop and politifact sources with a sucess rate of about 50%. This will result in a portion of our data having no detail beyond the title. Additionally, there are significantly more real articles that won't have data than false ones. It's possible that our model could create false association with being true and being shorter. We may choose to remove these entirely, and also want to train the model on even amounts of true and false data, so we may truncate the output anyways.
