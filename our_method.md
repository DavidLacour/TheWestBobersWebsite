# Our Method

## Creating subsets

In the process of searching for Pivotal Movies, we need to extract smaller dataframes that can be handled more easily. In order to keep the probability of movies influencing one another high in a dataset (which is a required characteristic of a Pivotal Movie), we decided to group the movies by genre. This way, we were able to identify XX subsets, that contain at least 100 movies. Still the sets are not too big, so they can be handled easily and are suitable for the next steps. 

## Signal processing - extract the candidate sets

To find a set of possible Pivotal Movies (called the candidate set), we need to detect the trends which they created. We define a trend as a significant positive variation in the number of movies released in a particular genre compared to the rest of the market. This trend is characterized by a notably high increase in the volume of movies of a specific genre, indicating a rising popularity or interest relative to others. Trends should be caracterize by a high bump. 

We treat the function that describes the yearly percentual share of the subset (the genre) as a signal. Filtering this signal with a low-pass Butterworth filter (keeps the lower frequencies), returns a smoothed development of the fraction of the subset, minimizing the impact of short-term fluctuations. 

With this smoothed distribution, it is possible to detect the trends, that can be identified as local maxima (peaks). Peaks have to be higher than the average fraction over all time of the specific subset. We introduce an additional criteria to these peaks, which is that the point of inflexion before the peak (the point where the slope changes from getting steeper to getting less steep) has to yield a significantly lower fraction on the yearly market than the one at the peak. We call this metric the quality of a peak. It guarantees, that the peak is “high” enough to be showing a trend. 

From the peaks that are judged of sufficient quality, we can extract the candidate set for Pivotal Movies. All movies that have been released within a timeframe of ten years prior to the point of inflection before the peak are selected as candidates. It is important to choose a proper range so we don’t miss the pivotal movie (too short range), and we don’t predict a movie without relation to the trend (too big range). Recognizing that films that have been influenced by a trend wouldn’t be released immediately, as the time it takes to produce a movie from scratch is typically spanning 2-3 years ([1](https://nofilmschool.com/how-long-does-it-take-to-make-a-movie), [2](https://www.studiobinder.com/blog/how-long-does-it-take-to-make-a-movie/)). A range of 5 years prior to the point of inflexion seems therefore reasonable. This way, the movies in the candidate sets have all been released during the time, when the hype has started, and could therefore be the Pivotal Movie of this peak. 

IMAGES OF SUBSETS WITH CANDIDATE SETS
