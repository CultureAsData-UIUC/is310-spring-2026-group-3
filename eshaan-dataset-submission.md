# Dataset Documentation

## Selected Dataset
Most Streamed Spotify Songs 2023  
https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023  

---

The dataset I chose to work with is a collection of the most popular songs from 2023, which is originally from Spotify but it includes not just basic metadata like track name, artist, and release date, but also streaming platform specific metrics such as Spotify streams, playlist appearances, chart rankings as well as Apple Music, Shazam, and Deezer which I have not heard of before. It also includes audio features like tempo, energy, and danceability. I chose this dataset because it strongly represents a kind of crossroad of culture and data. Music a huge part of culture where so many people use it as a means of expressing themselves, but platforms like Spotify reduce it into metrics, and rankings which makes it easier to use for analysis. The more people like a certain song the more it’ll have appearances or rankings within the datasets.

My approach was auditing rather than building from scratch. I did not collect the raw data myself, instead I worked on making the dataset something I wanted which means that it needed to be cleaned and formatted. 

---

## Tools and Process

To work with the dataset, I used Python on VS Code, primarily with pandas. This made it easier. I turned the CSV into a dataframe so I could look at the columns and apply any transformations that I wanted. One issue I ran into though was that the CSV wasn’t entirely in UTF-8 which I had to work around by using latin-1. For example, I filtered out non English songs using a basic ASCII filtering instead of a slower but more methodical full language library. 

These tools helped a lot in terms of efficiency. Things that would normally take forever, like filtering hundreds of rows or checking consistency across columns could be done instantly. But there were also limitations. For example, language detection is messy. Using ASCII for “English” is not perfect and definitely ends up removing a few valid songs while letting some non-English ones through. Also, platform metrics like “streams” or “playlist count” were strings so that could lead to inaccuracies but also they don’t really have a precise definition which leaves them ambiguous.

---

## Decisions and Challenges

One decision I had to make was filtering for English language songs to reduce extraneous songs and make comparisons more consistent. Another was deciding which columns actually mattered for analysis. The dataset includes a lot of features, but not all of them were useful to the data selection. Some are redundant, and others are unclear in how they’re measured which I had to clean. I had to decide what to keep based on whether it contributed to understanding popularity and I cut it down to the top 100 songs based on those popularity factors.

One challenge was dealing with inconsistent or unclear data definitions. For example, what exactly counts as a “playlist appearance”? Is it weighted by playlist size? Is it global or regional? The dataset doesn’t fully explain this, which made it kind of difficult to understand. I dealt with this by treating those metrics as relative indicators rather than absolute truths. Another issue was scale. At this size there were just way too many songs and would be obscuring patterns. Hence why I decided to trim it down.

---

## Observations

I noticed that there was a strong correlation between the popularity of a song and how often they showed up in playlist across platforms. It doesn’t always come down strictly to the amount of streams. On top of that, I had some questions about whether the was sort of positive feedback loop that pushed already popular songs back to users.

---

## Next Steps

For the next phase, I plan to scale my dataset using automation rather than auditing. The most direct way to do this is with the Spotify API to collect a larger sample of songs, maybe around 500 to 1,000 tracks. This would allow me to expand beyond the curated Kaggle dataset and capture a broader range of music with more flexibility.

This would involve using Python with libraries like requests to query the API and pandas to structure the results. If needed, web scraping could be used to supplement missing data from other platforms like Apple Music or Deezer. Formatting and cleaning this dataset could be a hassle depending on how the information is formatted when collected.

As the dataset scales, several interpretive decisions will need to be automated. For example, filtering for language will need a more reliable method than simple ASCII checks, for example using a proper language detection library. Decisions about which columns to keep would also need to be done before hand rather than handled manually. The definition of “popularity” may also need to be expanded into a more rounded and composite metric rather than relying solely on streams.

There are also a few technical challenges to consider. API rate limits will restrict how quickly data can be collected, which means requests will need to be batched. As well as the fact that I think Spotify’s API requires some sort of verification. Data consistency will become a bigger issue when merging information from multiple sources, especially if platforms define metrics differently. Additionally, if I plan on scraping I have to make sure that websites do not restrict scraping. 

Scaling changes how the data can be interpreted. With a small dataset, it is a lot easier to closely examine individual entries and understand their context. When taking things to a larger scale and stepping back, the analysis becomes more abstract and pattern based. While this allows for broader insights, it also increases the risk of overlooking nuances such as culture.