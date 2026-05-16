{\rtf1\ansi\ansicpg1252\cocoartf2869
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 ArialMT;\f1\froman\fcharset0 Times-Roman;\f2\fswiss\fcharset0 Arial-BoldMT;
\f3\froman\fcharset0 Times-Bold;}
{\colortbl;\red255\green255\blue255;\red0\green0\blue0;\red109\green109\blue109;}
{\*\expandedcolortbl;;\cssrgb\c0\c0\c0;\cssrgb\c50196\c50196\c50196;}
\margl1440\margr1440\vieww29700\viewh18540\viewkind0
\deftab720
\pard\pardeftab720\sa320\partightenfactor0

\f0\fs30 \cf0 \expnd0\expndtw0\kerning0
Reinterpreting Culture through Algorithms: Developing Custom Music Recommendations
\f1 \

\f0 Introduction: The Exit
\f1 \

\f0 In an era of music streaming, music recommendation systems are generally designed to create ongoing usage, or "stickiness," to the service that delivers music. By providing continued access to music containing elements similar to the music you already enjoy, these systems create an environment where musical genres will become repetitive (i.e., "taste loops"). As a result, the chance of discovering new music with cultural significance or historical relevance becomes non-existent. This study aims to analyse the relationship between algorithms that are highly structured, and fluid cultural consumption of musical genres through the creation of music metadata that has been transformed into a unique framework created to facilitate new taste connections, making it the direct alternative to bulky commercial music recommendations, and "safety first" directives of commercial music recommendation systems.
\f1 \
\pard\pardeftab720\partightenfactor0
\cf3 \
\pard\pardeftab720\sa240\partightenfactor0
\cf0 \
\pard\pardeftab720\sa320\partightenfactor0

\f0 \cf0 The Creation of the Database: Formation of Data from Close Listening to Data That Can Be Used to Model Algorithmic Behaviour
\f1 \

\f0 The process of creating this database occurred in two distinct phases, one where interpretive curation was performed on an individual level and a second phase where the interpretive curation was transformed into an algorithmically derived method of curation for the purpose of providing music recommendations that extended beyond an individual level.
\f1 \
\pard\pardeftab720\partightenfactor0

\f0 \cf0 [Phase 1: Bespoke Curation] \uc0\u9472 \u9472 > [Phase 2: Computational Scaling]
\f1 \

\f0 \'a0\'a0\'a0- 75 Track Core \'a0 \'a0 \'a0 \'a0 \'a0 \'a0 \'a0 \'a0 - 1,000+ Item API Expansion
\f1 \

\f0 \'a0\'a0\'a0- Manual Vibe Mapping \'a0 \'a0 \'a0 \'a0 \'a0 - Automated Feature Extraction
\f1 \

\f0 \'a0\'a0\'a0- Contextual Logic\'a0 \'a0 \'a0 \'a0 \'a0 \'a0 \'a0 - Vector-Based Pattern Matching
\f1 \
\
\pard\pardeftab720\sa320\partightenfactor0

\f0 \cf0 I created a custom base reference dataset (i.e., 75 connected audio tracks from three popular styles of music: hip-hop, R&B and pop) that consists of an evenly distributed set of three tracks (i.e., 25 tracks from each of the three styles of music). In constructing the foundation of the base reference dataset through the process of listening to each of the three parts of the base reference dataset critically, I added two pieces of qualitative metadata (two different types of human data) to each individual track to provide additional layers of meaning and definition for all 75 tracks.\'a0
\f1 \

\f0 Next, after the Completion of Spring Break, I used computational methods to scale the base reference dataset up over 1,000 (1000+) individual pieces of media using the Spotify Web API (through the use of the Python Spotipy library) to collect more data about each individual piece of audio media through the use of high-dimensional acoustic features (i.e., danceability (the strength of the rhythm)/energy (the perceptual intensity and activity of the music)/valence (the musical positivity or the emotion conveyed through each individual piece of audio media)). Finally, by integrating all this data (i.e., quantitative and qualitative data collected) I developed and automated all steps of the process of identifying acoustically similar pieces of music from different genres by using various pattern/algorithm analysis techniques to discover the similarities among all of the pieces of audio media that I identified.
\f1 \

\f0 By merging these real-world data points with my curated data, I constructed an automated pipeline that uses pattern-matching algorithms to discover acoustic overlaps between distinct genres.
\f1 \
\pard\pardeftab720\partightenfactor0
\cf0 \
\pard\pardeftab720\partightenfactor0
\cf3 \
\pard\pardeftab720\sa240\partightenfactor0
\cf0 \
\pard\pardeftab720\sa106\partightenfactor0

\f2\b \cf0 What the Data Reveals and Conceals
\f3 \
\pard\pardeftab720\sa320\partightenfactor0

\f0\b0 \cf0 The datasets themselves can be described as acts of translation. Given that any act of translation includes some measure of loss.
\f1 \

\f0 This dataset demonstrates the common mathematical qualities which exist between similarly classed (either socially or commercially) genres of music.
\f1 \

\f0 For example, through a visual representation of the vector-space intersection of Danceability and Energy, the data shows us very clearly how high-EBM Modern Hip-Hop has a structural profile so similar to Electronic Pop as to be practically indistinguishable from one another (excluding tempo differences). Therefore, this numerical relationship provides a clear "algorithmic path" or "roadmap" for what a recommendation engine may use to expand a listener's taste beyond their current taste limitations by providing the engine with the necessary information to determine the precise "acoustic bridge" a given track uses to take the listener from an easily recognizable genre and cross over into an unknown territory (musically speaking).
\f1 \

\f0 Conversely, this collection of data avoids, and even actively conceals all of the lived, messy historical context associated with various musical genres. In fact, by translating everything to floating-point values (where 0.0 = lowest rating and 1.0 = highest rating), the system completely strips away the lyrical storyline (i.e. "narrative"), political questionings (i.e. "subversive" lyrics) and the sociocultural geographic constructs (i.e. subcultures) that are a part of all variations of Hip-Hop and R&B music. For example, the valence score of a song (based solely on the song's positive chord progression) could present the track as being more "emotionally positive," thus completely masking the story of a sad lyric under a major chord progression or the ironic nature associated with the lyric narrative found within the lyrics of the song.
\f1 \
\pard\pardeftab720\partightenfactor0
\cf0 \
\pard\pardeftab720\partightenfactor0
\cf3 \
\pard\pardeftab720\sa240\partightenfactor0
\cf0 \
\pard\pardeftab720\ri800\sa320\partightenfactor0

\f0 \cf0 Computational Technology Influences Interpretation: a Change in Scale
\f1 \

\f0 The role played by computation within this project was not just as an administrative tool, but an agent that changed the way I interpreted the data about culture. In my early work at a small scale, interpretation was very personal and qualitative, but once the number of items exceeded a thousand, the number of items necessitated automating the categorization, destroying the way I interacted with the cultural objects.
\f1 \

\f0 In order to deal with this level of scale, I needed to formalize the logic of how I listen to cultural objects into rule-based computational structures. I established an automated pipeline to automate the grouping of tracks based on their Euclidean distances across their acoustic feature dimensions.
\f1 \

\f0 While scaling was a necessary step in order to achieve data consistency and provide valid patterns across a broad musical landscape, the act of scaling creates an inherent loss of the qualitative nature of the initial data set. The evaluation of the "feel" of a track, became the evaluation of the mathematical distance of that track from a cluster centroid, demonstrating how the use of scale creates an inherent homogenization of the cultural nuance for processing efficiency.
\f1 \
\pard\pardeftab720\partightenfactor0
\cf0 \
\pard\pardeftab720\partightenfactor0
\cf3 \
\pard\pardeftab720\sa240\partightenfactor0
\cf0 \
\pard\pardeftab720\sa320\partightenfactor0

\f0 \cf0 Ethical Concerns, Privacy Issues, and Platform Considerations\'a0
\f1 \

\f0 When working with commercial streaming data, platform neutrality has to be critically considered. The acoustic metrics used in this project - while many data scientists treat these as objective and empirical truth - were in reality developed, algorithmically abstract based on proprietary engineering by Spotify to effect sonic dampening and optimize passive listening.
\f1 \

\f0 Because the project used public metadata only, and does not use any form of direct human tracking, there are no individual privacy infringements. However, there is still an ethical risk of algorithmic gatekeeping through the use of platform generated metrics to create an expansion engine. This risk comes from the possible inheriting, and ultimate reinforcing, of the structural biases that are built into the Spotify ecosystem; those that consistently favour the distribution of major label pipelines and Anglo-centric musical structures over the distribution of independent / non-Western musical forms.
\f1 \
\pard\pardeftab720\partightenfactor0
\cf0 \
\pard\pardeftab720\partightenfactor0
\cf3 \
\pard\pardeftab720\sa240\partightenfactor0
\cf0 \
\pard\pardeftab720\sa320\partightenfactor0

\f0 \cf0 Contextualizing the Research in the Scholarly Literature
\f1 \

\f0 This project relates to topics in the realm of Computational Social Science and Music Information Retrieval (MIR). More specifically, it is based on the methodology described by Oramas et al. (2018) in their study titled "Multimodal Deep Learning for Music Genre Classification." In this study, the authors argue that typical classification of music genres through only one type of data (typically acoustic and/or instrumental) does not provide a complete representation of the cultural aspects of music. They propose using Convolutional Neural Networks (CNNs) to combine cacular audio tracks with additional data types (e.g., reviews and cover art) to illustrate that music is a collection of complementary qualities\'97its genre cannot be completely defined by a single attribute.
\f1 \

\f0 This study's research is based on their methods in terms of using a limited scope of the theory of multimodal classification to help music consumers make smarter choices by expanding their appreciation and enjoyment of music. So while Oramas et al. used a multimodal approach to improve the accuracy of music classification for archive creation, this study will use the HVT (Human Vibe Tag) to create a more intelligent way to recommend music to listeners. By combining the use of qualitative human-tagged data with quantitative data from APIs, this project will create a hybrid model for how to evaluate music culturally, confirming Oramas et al.'s conclusion that in order to understand how to evaluate how music is valued by humans, it is essential to merge the objective, computational data generated by computers with the subjective, experiential qualities of music experienced by humans.
\f1 \
\pard\pardeftab720\partightenfactor0
\cf0 \
}