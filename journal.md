### 9/30/25 - Ryan Cohen

- Designed project scaffolding

### 10/1/25 - Ryan Cohen

Work

- Created environment and instructions on how to use
- Outlined the preprocessing work to be done

Questions

- Half of our data has the articles and titles, while others only have the titles. How should we go about combining our datasets for training? I think that simply concatenating the title onto the text could work as long as we confirm that it doesn't associate length with truth or falsity.

### 10/1/25 - Ryan Cohen

- Wrote a script to scrape articles for the gossicop and politifact websites and attach them to their entries. I believe the process to be too slow, as it made it through 300 articles in 18 minutes, making the full database of 20000 articles a serious endeavor to get through. We may try this in the future if our data is insufficient. For now, we'll continue with our plan of concatenating articles to their titles if the article is present.
- Continued work on preprocessing and the typical NLP data cleaning.
- Experimented more with scraping articles and concurrent fetches to increase efficiency. I'm fairly sure that retrieving about half of those 45k articles can be done in three or four hours, leaving us with only around 22k/78-ish-k that are only titles.

### 10/6/25 - Ryan Cohen

- Figured out that we have a lot of articles already with full article text along with the title. We're fetching article data from the gossipcop and politifact sources with a sucess rate of about 50%. This will result in a portion of our data having no detail beyond the title. Additionally, there are significantly more real articles that won't have data than false ones. It's possible that our model could create false association with being true and being shorter. We may choose to remove these entirely, and also want to train the model on even amounts of true and false data, so we may truncate the output anyways.

### 10/6/25 - Sid Jain

- Tried pulling the repository and was running into a issue where it wasnt liking one of the imports.
- Turns out we are both are on different versions Sid-3.11.9 Ryan 3.13.5.
- Both on same version 3.13.5

### 10/11/25 - Ryan Cohen and Sid Jain

- Plan for the next week
  - first, we have to finish up the preprocessing. compile all sources into one dataset, text, truth boolean, and source columns (gossipcop/politifact/isot). we want to include the source because we may want to pull equally from all sources, which will require us to have info about which articles are from which sources.
  - after we have the reduced dataset, we're going to research how to train both the TF-IDF and BERT models, seeing if there's overlap in the way they tokenize. (there is not, so we have to tokenize separately)
  - after tokenization research, we'll split the work into TF-IDF training (Ryan) and BERT model training (Sid)
  - For the milestone report, we'd like initial testing done on both models, and even more ideally have some of the reverse engineering done to show the most important words affecting truth. That may have to wait.
- Preprocessing work
  - ran into issue where articles reached the csv cell character limit of around 32k. We opted to remove them from the dataset since there weren't many of them causing the problem
  - reduced the dataset down, ran into potential issue where random sequences from websites (https...) that could interact weirdly with the dataset.
  - ran into max file size limit for github, so we're not including those specific processed files in our pushes. We'll just run the same code to locally store it and gitignore those to prevent issues.

### 10/15/2025 - Sid Jain

- Successfully implemented BERT fake news classification model
  Data Manipulation:
- Added dataset size selector feature with simple variable (DATASET_SIZE = 300) to control the amount of time needed to train model
  - Created balanced sampling to ensure equal representation of fake and real news articles (150 fake + 150 real) instead of training on imbalanced data
  - Discovered during testing that initial sampling resulted in all 300 samples being truth news so made sure that for whatever number of articles there was a equal split.
- Initially faced 31+ hour training estimates due to GPU memory buffer. Switched to CPU training which reduced training time to ~5 minutes for 300 samples while maintaining stability

Initial Run 300 samples

- Training completed successfully in approximately 5 minutes on CPU
- Loss progression showed good learning: started at 0.7060 (epoch 1), improved to 0.6775 (epoch 2), and ended at 0.5101 (epoch 3)
- Model showed learning capability with 28% loss reduction over 3 epochs

Run after 1000 samples
Epoch 1 of 3
33%|███▎ | 100/300 [03:14<06:22, 1.91s/it]
Average Loss: 0.6553
Epoch 2 of 3
67%|██████▋ | 200/300 [06:29<03:15, 1.95s/it]
Average Loss: 0.4866
Epoch 3 of 3
100%|██████████| 300/300 [09:45<00:00, 1.92s/it]
Average Loss: 0.2891

### 10/16/25 - Ryan Cohen

Made quick updates to the gitignore to avoid uploading files exceeding github's upload limit

### 10/19/25 - Ryan Cohen

Work

- Designed the TF-IDF model tokenization and linear regression training loop
- Began comparing configurations of the model by comparing output like precision and accuracy of different input, like a maximum word count per article and testing the ability of a model trained on one dataset to predict the authenticity of another dataset's article.
- Designed output to display the "explanation" of the truth result based on each word and it's truth vector

Thoughts

- From my preliminary results, using a relatively straightforward TF-IDF model trained on every source and without word limit (the combination that led to solid metrics), it's clear that things like proper nouns have a heavy impact on the outcome. The best example is that names like Joe Biden or Donald Trump are labeled as extremely likely to be false, and those contributions weigh more heavily than other words do. It's possible that removing names could be a path forward.

To-do

- I'll run some tests to see what words out of the whole dataset have the heaviest magnitudes in both directions.
- I'll have to do some research on how other people have dealt with this issue generally.
