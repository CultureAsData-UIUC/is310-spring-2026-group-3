# IS 310 - Group Dataset

## Potential Datasets:
- https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset  
- https://www.kaggle.com/datasets/solomonameh/spotify-music-dataset  
- https://www.kaggle.com/datasets/yashdev01/spotify-tracks-dataset  

---

## Initial Dataset (~50-100 items)

Your bespoke dataset in a structured format of your choice. You should have a rationale for how you have organized your data.

- Selected Dataset Link

---

## Initial Documentation

Your first attempt at documentation that you think best reflects your process, interpretative choices, and explains the dataset. Some questions you might want to address include:

### What cultural materials are you working with and why? What approach did you take (from scratch or auditing)?

The data for this project is made up of music and audio features derived from the Spotify Web API in addition to metadata about the digital track. This data is an example of how streaming music is being quantified as music is being turned into data points in a way that allows us to assign a numeric value for aspects of a song like its “danceability”, “energy”, or “valence”.

Our approach was primarily through audits. Rather than building our own data set from scratch, we chose instead to audit existing large datasets of Spotify music already on Kaggle to assess their representativeness and if they covered a wide enough breadth of the contemporary music landscape.

We decided to choose this dataset over other datasets due to the standardized set of 20 features for every track, which simplifies the nature of comparing each track among genres. Similarly, it differs from most playlists datasets which were more messy and subjective.

This specific dataset includes the “track-genre” column with 125 distinct categories that allows for a more nuanced cultural breakdown and analysis compared to a Solomon Ameh “Top 50” lists on Kaggle which lacked precise row indexing and had many unnamed columns.

---

### What computational tools did you use to assist your work? How did they help? What were their limitations?

We used pandas in Python to clean, filter, and sample the dataset, along with Kaggle as the main platform to access the data. Pandas made it easy to quickly understand the structure of the dataset and check for missing values.

We also used it to generate a random sample of around 100 songs from the 114,000, which became the basis for our smaller, annotated dataset. This helped us move from a large, abstract dataset to something smaller and manageable we could analyze. One thing we had to deal with was simplifying the dataset into an English only dataset. A lot of the songs did come from a multitude of cultural backgrounds which would be hard to run analysis on.

These tools were helpful in organizing and scaling down the data, but they also came with limitations. Most importantly, they only helped with structural and numerical aspects of the dataset, not with interpretation. For example, while we could easily sort songs by “valence” or “energy,” these labels were defined by Spotify’s internal systems in the first place, so we do not actually know how they are calculated. This means that even though the data appears clean and standardized, it still carries some hidden initial assumptions that we cannot fully verify just by using computational tools.

Another limitation is that tools like Pandas are very quantitative. It turns things like “danceability” or “energy” as numbers, when in reality these types of values are quite subjective interpretations. Because of this, we have to be careful not to rely solely only on the computational outputs and inspect the data carefully.

---

### What decisions did you make about what to include, exclude, or how to categorize? Why? What challenges did you encounter? How did you address them? What patterns, questions, or tensions emerged from working closely with this data?

The main decision we made was to limit our dataset to a smaller random sample of 100 songs. We wanted it to be random primarily because we wanted a range of genres and features so that we were not looking at one type of music.

With regards to what to include, we decided to include the fundamental audio features provided by Spotify, such as danceability, energy, valence, tempo, and popularity. However, we did choose to look at only English music because we assumed that different languages would have vastly different values. We also wanted our data to be easily comparable.

One of the challenges we faced, as previously mentioned, is that many of the features provided by Spotify are not entirely transparent. For example, while “valence” is supposed to represent how positive a song sounds, it does not necessarily reflect our emotional interpretation of the song. This made it difficult to determine whether our results were due to our interpretation or due to the limitations of the Spotify system.

Another challenge we faced was that many songs have mixed signals, such as a fast tempo but sad lyrics.

From working with the data, something that we found was that the numeric features provided by Spotify don’t necessarily convey the meaning or context of a song, but rather the sound of it. This was a conflict between what the data was telling us and what the actual experience of the song was like. This also made us think about the extent to which meaning and emotion are being lost when a song is translated into numbers. This process demonstrated that even with structured data, interpretation is necessary, and there are multiple ways to interpret music.

---

## Next Steps

After creating this bespoke dataset, after Spring Break, you will work on scaling or expanding your dataset with computation. This plan should outline how you will address the following questions:

- How will you generate more data computationally (Option 1: scale up to 500-1,000+ items using automation)? Or will you combine your bespoke data with an existing large dataset (Option 2: audit, merge, and analyze)? What computational methods will you use? (APIs, web scraping, LLMs, pattern matching, etc.)

- What will change when you scale? What interpretive decisions will you try to automate? What technical challenges do you anticipate?

- This plan is your roadmap for understanding how scale transforms data work. You don’t need to implement it yet—but you should be thinking critically about what happens when you move from 75 carefully crafted items to 1,000 algorithmically generated ones. Your initial dataset should be submitted in your group’s GitHub repository and you should update any collective documentation to help users navigate the files and folders.

---

### Next Steps (Plan)

We will be merging our curated dataset with an existing large dataset. This will likely be done through obtaining data on Spotify using their API, which appears to be quick to set up. We’ve decided that webscraping for music on any platform aside from streaming platforms is impractical, especially when so much data is easily accessible through an API. However, there may be some discussions on platforms like TikTok or Instagram about songs that we miss out on through Spotify’s API rather than scraping.

An important consideration for our data is that most variables in it are calculated or estimated by a computer. Things like time signatures are noted as “estimated”, which implies that an algorithm was applied to songs. This can apply to basically all the variables. That being said, since it’s being calculated by Spotify, it might have more merit than some algorithm written by a guy in a basement.

With 100 songs, having a world renowned expert on music to review all our songs would take an hour or two. When we scale up to a thousand songs, listening to all of them and verifying 10+ variables for each one would take a long time. As such, we aren’t able to verify our dataset as it grows large anymore, at least in the traditional manual sense.

However, we anticipate that having more data means that our dataset will be more representative of our target population than the one with only 100 observations. Additionally, by manually checking all 100 songs, we can be sure that they are all representative of our population. With 1000, we can’t manually check anymore, and therefore introduces the risk of introducing a “bad song”.