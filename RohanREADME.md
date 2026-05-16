# Spotify Listening Dataset – Culture as Data Project

## Overview

This project explores how my personal music listening behavior can be turned into structured data. Instead of only focusing on technical data like song name or artist, I tried to capture more human aspects of listening, such as mood, energy, time of day, and whether I skipped a song.

The goal of this project is to understand what happens when something personal and emotional, like music, is converted into data. This dataset reflects both my individual listening habits and the influence of the Spotify platform.

---

## Dataset Structure

The dataset is stored as a CSV file and each row represents one song. The columns are:

- **Song** – name of the track  
- **Artist** – performer of the song  
- **Genre** – general music category  
- **Mood** – my interpretation of how the song feels  
- **Energy** – relative intensity (low to high)  
- **Time** – when I usually listen (morning, afternoon, night)  
- **Skip** – whether I tend to skip the song  
- **Source** – how the song was found (search or playlist)  
- **Popularity** – platform-based popularity indicator  
- **Data_Type** – manual or scaled  

This structure combines objective data (artist, popularity) with subjective interpretation (mood, energy).

---

## Manual Dataset (Bespoke Data)

I first created a manual dataset of 75 songs that were popular . For each song, I manually assigned values like mood, energy, and time of day.

This step required careful thinking because categories like mood are not fixed. The same song can feel different depending on context, which made me realize that I was not just collecting data, but actively shaping it.

The manual dataset is more detailed and personal, but also more subjective.

---

## Computational Scaling (Spotify API)

To expand the dataset, I added around 75 more songs from my personal Spotify playlist using the Spotify API. This allowed me to scale the dataset and work with a larger number of songs.

Compared to the manual data, the scaled dataset is:
- more consistent  
- easier to organize  
- less detailed in personal interpretation  

This shows how computation helps with scale but reduces nuance.

---

## Key Observations

While working with the dataset, I noticed a few patterns:

- I tend to listen to calmer or sadder music at night  
- Higher-energy songs appear more during the day  
- Songs from my own playlists are skipped less often  

However, these patterns are not always consistent, which shows that listening behavior is more complex than the data suggests.

---

## Platform Influence

Although this dataset is based on my personal listening, it is strongly influenced by Spotify.

Many songs come from:
- playlists  
- recommendations  
- trending music  

This means my listening behavior is shaped not only by my choices but also by the platform’s algorithms. The dataset reflects both personal and system-driven patterns.

---

## Limitations

There are several important limitations:

- Mood and energy are subjective and may change over time  
- Music can have multiple meanings, but the dataset simplifies it into single categories  
- The dataset only represents my listening habits  
- Platform influence is present but not fully visible  

Because of this, the dataset should be seen as a simplified representation, not a complete picture.

---

## Ethical Considerations

This dataset includes personal listening behavior, so I made sure to avoid collecting sensitive information.

- No location data included  
- No personal identifiers  
- Focus only on music-related behavior  

This keeps the dataset useful while protecting privacy.

---

## Conclusion

This project shows that turning music into data is not just a technical process. It involves interpretation, simplification, and decisions at every step.

While the dataset helps reveal patterns in listening behavior, it also hides the complexity of music as a cultural experience. Understanding this balance is the key takeaway from this project.

