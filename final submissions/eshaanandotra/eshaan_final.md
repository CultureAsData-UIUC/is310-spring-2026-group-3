# Data Essay Final Submission

Eshaan Andotra - IS 310 - May 15, 2026

## The question and the dataset

My dataset started off as a Kaggle file of the most-streamed Spotify songs of 2023, which I cleaned and trimmed down to a curated set of 100 tracks (top_100_songs.csv). On top of that I built two layers of augmentation. The first was computational. I took the cross-platform playlist and chart counts that were already merged into the source schema and treated Spotify, Apple Music, Deezer, and Shazam as four sibling datasets, then produced composite metrics from them. The second layer is the one that ended up mattering most. It was a cross period merge against two extra datasets similar to what Professor LeBlanc suggested. Those datasets being Spotify's all time top 100 most streamed songs (updated to March 2026) and the Wrapped 2025 top 50 global songs. That merge is what final-augmented-top100.csv represents.

The research question changed from what it was originally as the project went on. I started off asking why a song gets added to a playlist. After spending hours bashing my head against my laptop from Spotify's Web API being stubborn(more on that below), I pivoted the question into something I could actually answer with the data I had. Of the songs that were dominant in 2023, which ones are still here in 2025, and what keeps the ones that stay relevant compared from the songs that aged out?

## How I made it (and what computation actually did)

The first phase was a manual audit of the Kaggle source. I worked in pandas and filtered to English only tracks using a basic ASCII test, which is blunt. It drops songs with stylized punctuation and lets through some transliterated non English ones. I knew this at the time and accepted that. After that I trimmed to the top 100 by streams. The original CSV wasn't a clean UTF-8 either, which is why a few rows in top_100_songs.csv still have weird artifacts in the artist names (the "Beggin" / "Seï¿½ï¿½o" rows). Morris (2015) describes formatting a cultural object for a platform as something that's never neutral. Every encoding choice carries cultural assumptions. Mine assumed English meant ASCII, which it doesn't. I then took the top 100 songs of those.

Then came the computational augmentation. I made a python script that produced nine derived columns including total_playlists (Spotify and Apple and Deezer summed), total_charts (all four chart sources), cultural_footprint (a z score composite of streams, playlists, and charts), and era_normalized_streams (streams divided by years since release). I wanted to hammer the idea of a cross platform view rather than just sticking to one. The z-score composite is the part that does the work. It weighs platform-singular hits the same as cross-platform saturators, so a song that's big on Spotify but only on Spotify doesn’t stand above the rest. 

The merge became the focus of this project in the end because it shows the change over time. It joins my 2023 anchor against the two newer reference lists using a normalized artist + title key. The matcher strips parenthetical noise like "(feat. ...)", "(Remastered 2011)", and "- Spider-Man: Into the Spider-Verse" before comparing, which is how "Sunflower - Spider-Man: Into the Spider-Verse" in my anchor matched "Sunflower" in the all-time list. For each anchor song, the script flags in_alltime_top100, in_wrapped_2025_top50, and a binary is_persistent (true if either flag is true). Then it runs correlations, a linear probability regression, and a comparison of the groups.

Now here’s what happened to my original plan. My original idea was using Spotify's Web API to pull playlists, either through gathering direct names/links or anything else the API offered, to compare how songs ended up on playlists. None of many pipelines and scripts I tried to make worked. Spotify's November 2024 API changes for developer apps strip the popularity field, the audio features endpoint, the artist genre and follower fields, and the available markets list from any application that hasn't been approved for "Extended Quota Mode," a manual review process that takes weeks. By Spotify's classification it was a "Development Mode" app, and the Development Mode tier returns track objects with most useful fields blanked out. I confirmed this by running it. The /search and /tracks endpoints returned identifiers and titles, but null popularity, null genres, and null followers. So I pivoted to the more accessible merge described above using a Kaggle dataset. The wall is itself a finding, and I come back to it in the limitations section.

## What the dataset reveals

Three findings, in order of how much they reorganized the way I think about "popularity."

### Less than half of the 2023 top 100 made it through.

Out of 100 anchor songs, only 47 appear in either the all-time top 100 (through March 2026) or the Wrapped 2025 top 50. The other 53 fizzled out in the three years which seems most normal to be honest. However, that included some songs I would have expected to stay like, "Bohemian Rhapsody" (1975), "All of Me", "Take Me To Church", "Wake Me Up", and "HUMBLE." by Kendrick Lamar. Streaming popularity tends to shift unexpectedly. Even songs with two billion plus streams can fall off after a few years. Even songs that have been consistently popular such as “Bohemian Rhapsody” which has been relevant for many many years.

### Audio features barely predict persistence.

I fit a linear probability model regressing is_persistent on every audio feature plus release year and 2023 streams, with all predictors standardized so the coefficients are directly comparable. The R^2 is 0.26, which means 26 percent of the variation in which songs persisted can be explained by the model. The strongest predictor is 2023 stream count (std_coef = 0.211), which is partly mechanical as you could probably guess. Songs that were bigger had more cushion. The more interesting result is which audio features moved the needle and which didn't. Valence, the "happy versus sad" feature has a standardized coefficient of 0.007. Danceability is also flat. The feature that does help is liveness (std_coef = 0.107), which Spotify defines as the algorithm's estimate that a track was performed live or contains audience noise. Moreover, persistent songs were slower than faded ones (118.5 vs 126.2 BPM) and a bit less energetic (mean energy of 62.8 vs 66.3). Whatever sorting Spotify's recommendation algorithms are doing, mood as encoded in valence is not what carries a song into year three. Maybe this has to do with a trend of tiktok songs boosting to be really popular then falling off really quickly. 

### Pop is the genre that stays the most relevant, but the pop is the slower, less produced kind.

Among the 47 persistent songs, the genre tags (inherited from the merged sources) skew heavily toward Pop and Indie Pop. I understand that pop is if not the most popular genre for music. One thing to note is that EDM adjacent tracks barely appear. "Don't Start Now" (Dua Lipa, 2019), "Wake Me Up" (Avicii, 2013), and "Can't Hold Us" (Macklemore, 2011) were all top streamed in 2023 and all fell out. The slow, sparse tracks held on. Songs like "Someone You Loved," "Heat Waves," "Adore You," "Easy On Me." This lines up with what Drott (2018) calls the recommendation’s preference for "ambient" listening contexts. A song that works as background tends to play in any context, so it stays in rotation across moods and years. The ones built for one peak emotional moment tend to age faster since people tend to listen to them for a specific reason and more times, burning through them.

## What the dataset conceals

It still conceals listeners. The all time and Wrapped 2025 datasets are aggregate measurements that say nothing about who streams what or in what context. Two billion streams of "Someone You Loved" could be one billion personal sad moments and one billion algorithmic background songs in a Target playlist, and the dataset cannot tell the difference. As Eriksson et al. argue in Spotify Teardown (2019), the apparent "fact" of a stream count is the output of an opaque pipeline that includes algorithmic gatekeeping, and label platform partnerships that dilute the meaning of those numbers.

It also conceals the source of the merged datasets themselves. The alltime and Wrapped 2025 files I pulled from Kaggle are curated, and there's no clear methodology document explaining how their authors handled the boundary between a "song" and its remixes, or what counted as a "2025 stream." Working across these sources means trusting them, and I've tried to be explicit about how I made the joins (normalized artist + title with a fallback to title only matching) so anyone reading this can have an idea of where these things are coming from.

And the dataset conceals what Spotify, the platform itself, would not let me, as a researcher, to see. The API gating I ran into. To restate the point, a researcher can't freely audit a streaming platform's catalog using its own API, even for the public popularity and metadata fields that the platform itself surfaces in its own interface. Anything you want to do at scale has to be approved for. That's itself a cultural fact about who gets to participate in studying music as data, and it falls heavily on student researchers without institutional API allowances. Prey (2018) is explicit about the asymmetry of access that platforms construct around their data. This hinders how people can have access to this information and limit what we can do and discover with cultural objects as data. 

## Scale, and how it changed the work

When the dataset was 953 rows, I was making decisions song by song. I then switched to the top 100 "English songs". But more over it was affected by my filtering rules and normalization choices that I had to defend in code rather than in commentary. The clearest example is my matching. Take, for example,  "Bohemian Rhapsody - Remastered 2011" against an all time list that just calls it "Bohemian Rhapsody." It's a one second judgment call when you can see both rows on the same screen. It's a regex problem when you have 100 tracks and a 100 track reference. My matcher strips a fixed vocabulary of post title qualifiers ("remastered," "radio edit," "live," "version," "bonus track," "soundtrack," "spider man") before comparing. That works for this dataset, but it wouldn't generalize and work for everything. The choice of vocabulary in that regex is the analysis at scale. Think about how we were combining book titles and how there were different versions as we saw in class. It's similar to that. There's no neutral merge.

## Limitations

The 2025 Wrapped list is only 50 songs and the all time list is 100, so the intersection with my 100 song anchor produces a sample of 47 persistent versus 53 faded. That's enough to run a regression but not enough for confident inference of anything. Genre tags themselves only attach to the songs that matched the merged datasets, which means faded songs are mostly tagless in the merged file and I can't cleanly compare genre distributions across cohorts.

The "persistence" definition is binary, which throws away information. A song that's #2 on the all time list and a song that's 97th are both is_persistent = True here. I do report the rank columns so the downstream analysis could use a continuous outcome, but I used the binary for interpretability.

I also want to be honest that what I'm calling longevity is a three year window which some may argue isn’t enough time to see a difference. My 2023 anchor was already a top 100 list and I'm comparing it against 2025 and early 2026 lists. That's the short window in which streaming numbers may be more random, and not reflect some deeper measure of long term cultural significance. A song that fell out by 2025 could come back. A song that's still in could fall out next year.

The API constraints I described above are also a methodological limitation, and probably the most important one. I planned to use my own pulled data from the Spotify API. However, I couldn’t and had to use an already curated and supplemented dataset to create my own by combining multiple. 

## Ethics

The data here is aggregate and preanonymized, so no individual listener is identifiable from this data. But every stream count and playlist appearance was built from individual listening behavior, pulled by platforms whose users didn't give meaningfully informed consent. Using this data for academic analysis is defensible. I just don't want to launder that surveillance into something that looks like neutral cultural data. Prey (2018) is direct about this asymmetry. Streaming platforms extract behavioral data from users under conditions of structural power, and the resulting datasets, including the ones I used, are downstream of that extraction.

## Lessons learned

The choice of metric is the analysis itself. Choosing is_persistent over raw streams reorganized the whole question. There's no such thing as neutral popularity.

Audio features are weak predictors of longevity, and that's very interesting. It tells me that whatever keeps a song in cultural rotation mostly isn't encoded in the features Spotify exposes or in general. The reason lives in social context, algorithmic exposure, cultural media (such as Tiktok), and unseen factors. The model's R² of 0.26 is the size of the audio features story. The other 74 percent is the cultural story the dataset cannot see.

## Situating the work

This project sits kind of at the center of music streaming studies and a discussion that's been going since the late 2010s that streaming metrics can't be read as transparent windows onto cultural preference. Eriksson et al's Spotify Teardown (MIT Press, 2019) is the book everyone in this field cites first. They argue that the platform is a black box that produces the very data we then try to interpret. Prey (2018) takes that argument and pushes it into algorithmic individuation, looking at how the system sees the listener. Morris's Selling Digital Music, Formatting Culture (UC Press, 2015) goes further back, into the longer history of how digital formats shape what even counts as a "song" in the first place. Drott (2018) argues that recommendation systems impose a scarcity logic that ranks otherwise comparable songs against each other. My project takes those critical ideas seriously and tries to put numbers behind them. Most of this scholarship critiques platform metrics in theory. I'm using them against each other in practice. Across time periods and across platforms, where I then report what the comparison shows. The finding that 53 percent of 2023's most streamed tracks fell off the 2025/2026 lists, and that audio features only explain about a quarter of the variance in which songs survived, is itself empirical evidence for the platform mediation argument the field has been making theoretically. The platforms shape what stays popular. The audio features themselves only carry about a quarter of the story.

The wall I hit with Spotify's API is worth situating too. Drott (2018) and Prey (2018) both write about the challenge of access that platforms construct around their data. Until I tried to study that data myself, those ideas felt like theoretical dead ends I’d never hit. Then, I spent five hours getting 401, 403, and empty field responses from every endpoint I needed. By the end of it, the asymmetry stopped feeling theoretical. Critical studies of platforms is something I've actually felt now. 

## Dataset Links

https://www.kaggle.com/datasets/alitaqishah/spotify-wrapped-2025-top-songs-and-artists

https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023

## References

Drott, Eric. “Why the Next Song Matters: Streaming, Recommendation, Scarcity.” Twentieth-Century Music, vol. 15, no. 3, Oct. 2018, pp. 325–57. EBSCOhost, https://doi-org.proxy2.library.illinois.edu/10.1017/S1478572218000245

Eriksson, Maria (1988-)., et al. Spotify Teardown: Inside the Black Box of Streaming Music. MIT Press, 2019. EBSCOhost, research.ebsco.com/linkprocessor/plink?id=ebf56dd2-1c39-31aa-b5a2-ee65fb28ff8a

Jeremy Wade Morris. Selling Digital Music, Formatting Culture. University of California Press, 2015. EBSCOhost, research.ebsco.com/linkprocessor/plink?id=29f71e2f-2d17-3750-86ba-874e843fd5ee

Prey, Robert. “Nothing Personal: Algorithmic Individuation on Music Streaming Platforms.” Media, Culture & Society, vol. 40, no. 7, Oct. 2018, pp. 1086–100. EBSCOhost, https://doi-org.proxy2.library.illinois.edu/10.1177/0163443717745147.