
<img src="jackstitel.png" style="width:100%; height:auto;">

## Definition
We defines movies that serve as wellsprings of inspiration and set the trends. This are movies that are so innovative that they changed the cinematic worlds forever. These are movies that are not only successful but also films that get heavily imitated, even parodied, and, most importantly, act as a construction basis for future movies.

We focus on american movies and genres that have more than 10 movies. 


## Methods ⚙️

### Step 1 we need to find the highest trends:
To find the best trends we smooth the number of movies released each year. Smoothing data from different years allows for a more direct comparison by minimizing the impact of short-term fluctuations.
We first applies a low-pass Butterworth filter to the input signal for smoothing. It then identifies the local maxima (peaks) and inflection points in the smoothed signal. A peak is considered significant if it is higher than a given fraction ('frac') of the maximum value in the signal. Additionally, the 'quality' of a peak is assessed based on its prominence over the nearest inflection point, relative to 'frac'. Only peaks meeting both criteria (height and quality) are returned.


### Step 1: Pre-processing
Pre-processing consist in formatting the data in a way that facilitate further analysis and computations. We will handle missing data and outliers, and normalize the data. We will also enrich the data with additionnal datasets, by merging informations.

We will also filter the dataset, to be more precise on the data covered. We decided to focus on the movies in English and produced by the US. We could introduce more filtering later if needed…

### Step 2: Subsets
There are several ways to create a subset. It has to be relevant enough to analyze a trend. The easier approach is to use genres of movies, but other methods could be interesting to investigate. For example, we could extract vocabulary from a summary (ex: spaceships). Also, our dataset provides us very interesting substance : processed NLP which extracts tropes from summaries (type of character in a movie). Thus, we could analyze occurrences of tropes over time, and possibly draw trends.

We will start by creating simple subsets of genres. Then we will explore other ideas as extra.

We have to be careful when creating subsets to get meaningful results, because a too large one would group movies with not much in common together, and a too small one would group too few movies to draw interesting conclusions.

### Step 3: Shape analysis
We noticed that the number of movies over time has exploded in early 2000's (Fig. 1), then a rough analysis of the distribution wouldn’t be robust. To get more interesting results, we’d like to compare and visualize the evolution of fraction of movies from a specific subset. By plotting this curve, we are seeking an unusual shape, such as a bump or high variation. We typically recognize an unusual shape (of a subset) if it differs from the baseline (whole dataset).

A nice visualization would be a stacked plot to combine both number of releases and fractions of subsets. Here, a problem we might encounter is the high number of genres, because that would require too many colors and overload the graph. An idea to solve this issue is to group genres into 5-10 main categories, and have a more readable plot. For example the genre “airplanes and airport” isn’t that representative yet for a first visualization, however it could be that this category reveals a peak of trend with further analysis…

### Step 4: Range selection of prior movies
Once the unusual shape(s) has been identified, we will select a range prior to the trend peak, assuming the pivotal movie lies inside of it. It is important to choose a proper range so we don't miss the pivotal movie (too short range), and we don't predict a movie without relation (too big range). Recognizing that films influencing a trend wouldn't be released immediately, we acknowledge the time it takes to produce a movie from scratch, typically spanning 2-3 years in 2006 ([1](https://nofilmschool.com/how-long-does-it-take-to-make-a-movie)),([2](https://www.studiobinder.com/blog/how-long-does-it-take-to-make-a-movie/)). Then, the first approach is to select a range of 5 prior years, which seems reasonable. Otherwise, a more precise method that requires more work and hypothesis would be to identify a bump as a roughly (skewed) gaussian curve. Then we could select a range of 1-2 standard deviations prior to the mean/median/mode.

### Step 5: Pivotal Score
Finally, we will elect the most probable pivotal movie of the selected range, which maximizes a score. From our definition of pivotal movie, the score would be based on money generated (which reflects how many people watched the movie) and public advise (how was the movie recieved). The metrics used here would be box-office and review score. Then if several movies reached the top score within a certain threshold, our intuition is to prefer the earliest movie released, because it would be the most likely to influence later releases.

We might investigate further metrics, such as differentiating public and press review score. We’re also thinking of the impact of inflation on the revenue (Fig. 2). It would be interesting to adapt the box-office to the real value of money according to its release year. Then observe if this changes the pivotal movie selected.

### Further steps: ML approach
We’d like to introduce a ML approach to automate the research of pivotal movies. By selecting features that capture the “trend”, with a training set of movies identified as pivotal and not (from the previous approach). Then we’ll fine tune weights to have a robust model, and possibly reveal more pivotal movies. To reduce computations, we could analyze the dataset only by a 10-year tranche.




Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](./another-page.html).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# Header 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
--- layout: default ---
--- 
layout: default
---





# ADA Template Website
## Usage
1. Fork (copy) this repository by clicking the "Fork" button on the top right corner.
2. Go to "Settings" -> "Pages" in your forked repository. Under "Branch" change "None" to "master" and click "Save".
3. Edit the `_config.yml` file in your forked repository to change the site title (after `title:`) and description (after `description:`).
4. Build your own page by editing this `README.md` (home page) and creating new `.md` files (other pages), formatting is done with standard [GitHub Markdown syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax), we provide an example file `example.md` in the repository.
**Important**: Please include ```--- layout: default ---``` (the first three line in `example.md`) at the beginning of your every newly created `.md` file.
5. Add your new `.md` files to the site by editing the `_config.yml` file in your forked repository. Under `navigation:` add a new pair of `- title:` and `url:`, and fill their value with your page name and `.md` file name. Remember to remove the `- title:` and `url:` pair for the example page.
6. Go back to "Settings" -> "Pages" to find your website link.
