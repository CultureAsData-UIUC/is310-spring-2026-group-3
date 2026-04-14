# Group Landscape Mapping

Inika: Intro + Full assignment coordination
In our particular assignment, our team was looking at the use of computational methods for cultural data, focusing specifically on applications in music. Each team member found and read through a peer reviewed article, where a computational approach was used to analyze something cultural like songs and playlists.
When analyzing the similarities between all of our papers, we found some common features especially with the computational methods. This includes their machine learning techniques, large and diverse datasets, emotional states, and overall music being a reflection of identity. We also note the possible limitations mainly including the lack of consideration of possible biases of researchers when collecting and analyzing data.

Raymond: Computation Mapping 

Overview of Critical Findings From Papers

“All of Me”: Mining Users' Attributes from their Public Spotify Playlists uses Spotify playlists to predict user attributes (ie. personality, gender, etc.) using DeepSet neural networks. The data used to train the model are playlists and survey responses from 739 users. The model works well but raises concern about reducing users’ music preferences and identity into listening patterns and how that reduces the dimensionality of cultural context. 

SONICS: Synthetic Or Not -- Identifying Counterfeit Songs is focused on the idea of detecting AI-generated songs, specifically, differentiating “bleeding-edge” fully AI-generated ones from fully human-made ones. The authors built a dataset with 97,000 songs and ended up proposing SpecTTTra, a transformer architecture with strong results (F1 = 0.94). Fundamentally, this is a classification model. 

Multimodal Deep Learning for Music Genre Classification classifies music into genres using audio, album, art, and text reviews through a multimodal neural network. The multimodality of the neural network could actually underperform compared to a unimodal comparison (due to the fact that genre can be subjective sometimes), and has tradeoffs in the department of model interpretability.

AVMeme Exam: A Multimodal Multilingual Multicultural Benchmark for LLMs' Contextual and Cultural Knowledge and Thinking benchmarks whether AI models can actually understand culturally embedded audio-visual memes. This paper is noticeably the most centered around the humanities, and makes the other papers look like “mad science” comparatively. The key finding is that models fail at deep cultural reasoning even though it appears that they do well on the surface level. 

Modeling Music Emotion Judgments Using Machine Learning Methods studies emotions and aims to predict them from music using physiological signals, audio features, and listener self-reports. Neural networks performed the best. The AI summary was shallow and didn’t quite capture the subjectivity, nuance, and complexity of human emotions and how that relates to a given song. 

Key Convergences / Divergences

	All papers have some sort of study involving datasets and training some sort of learning model, DNN or otherwise. Many papers tangle with the idea that music can be subjective in almost every way, and whether or not computation can capture it. Several use multimodal approaches and combine audio with other dtypes. An important theme that humanities and technology research tends to clash over is the idea that AI tends to oversimplify, especially around the complexity of cultures. 

	SONICs is an outlier in terms of purpose. Rather than trying to interpret music, it aims to perform almost a forensic classification. Papers also differ in how they treat music. Some treat it as a datapoint, observation, or signal to classify, while others treat it as a cultural artifact to interpret. Finally, the scale of datasets varies, ranging from 739 observations to 97,000 observations. 

Mapping the Role of Computation

Augmentation:

SONICS: The core contribution is building a dataset and a benchmark (SONICS)

AVMeme Exam: Core Contribution is creating a curated cultural dataset and eval framework. Analysis plays an important side-role to help validate the dataset, but doesn’t make any independent claims.

Analysis:

SONICS: Plays a double role and has important uses of computation for analysis, namely, the SpecTTTra transformer, which demonstrates formidable predictive performance for classification of fake (AI generated) vs real music, and provides a real foundation for future work in this field. 

All of Me: Computation is the primary “thing” of interest, and predicting user traits from playlists and survey responses. 

MM DL for Music Genre Classification: Pretty straightforward how computation is used to evaluate whether multimodal models are better than unimodal ones, and does somewhat of a negative analysis, finding that they are not necessarily better. 

Music Emotion: Computation being used to predict emotion is effective, but the deeper finding is that the analytical methods are not enough to capture how complex subjective experiences can be. 

Communication (no new interactive public tools, data viz, etc.)



Beau: Similarities between the papers
The most evident trend is shifting away from the standard statistical techniques used to analyse complex culture with advanced forms of machine learning called artificial intelligence, specifically neural networks.
Examples: As seen in Inika's article where she outlines her use of DeepSet models to process the unordered list of songs contained within playlists while also discussing how Beau implemented Multimodal Deep Learning that combined CNNs and feedforward networks; Raymond introduced SpecTTTra (a new type of Transformer architecture) in his research paper; and Rohan's research paper showed after conducting a series of experiments with neural networks, that they were indeed the best model for predicting emotion.

Importance: This shows a movement toward models that can capture nonlinear relationships and long-range structures present in audio and metadata.

All of the authors are going beyond basic audio analysis to aggregate a large number of diverse data into a "multimodal" representation of music.
Examples: Surprising enough, Raymond used nearly 97,000 songs paired with both lyrics and metadata in order to create his dataset; Eshaan has used over 1,000 annotated audio-visual clips (including context and emotion) and used them as part of his exploration into the AVMeme Exam; while Beau specifically fused the audio of music with the visual of album cover art and text that reviewed the album.

Importance: There is now widespread agreement that audio alone will not yield a complete understanding of music; therefore, it is necessary to include and appropriately blend the visual and textual "surrounds" of music in order to achieve maximum accuracy.

Predicting human characteristics as well as emotional states. At the foundation of many of these projects is to decode human experience computationally, that is, to convert musical patterns into personality-based or demographic-based profiles. For example, Inika’s paper uses playlists to determine characteristics, such as Openness and gender, as well as other demographic characteristics; and Rohan’s paper describes how to use musical elements and physiological parameters (e.g., heart rate) to predict human emotion. Taken together, these studies evaluate music as more than an auditory experience; they treat music as a form of involuntary biometric data or a psychological profile.

Music as a reflection of culture and identity. The underlying assumption in all articles is that digital music artifacts reflect culture in a complex form and, therefore, can be used as an accurate representation of culture. For example, Inika’s article claims that playlists represent the individual's "cultural expression" as well as their "individual identity," while Eshaan’s article states that memes and media are "culturally embedded texts," and Beau’s examines how integrating diverse types of data produces a "greater understanding of the formation of musical genres" from the perspective of social theory. This trend captures the digital humanities component of the work, by using technology (software) to reduce abstract concepts such as "humor," "culture," and "identity" into constructs that can be measured.

There is an accuracy issue with the AI-generated document in that there was a failure to capture nuance around how the authors emphasized the limitations and general failures of these models or systems (i.e., authors from the Inika, Eshaan, and Rohan papers separately warned that although there appears to be a trend of increasing complexity between/among models/systems, they also warned that these types of computational/algorithmic patterns may still miss meaningful depth of lived cultural experiences).

The AI was able to aggregate the broad similarities expressed across very different studies and identified the common trend of moving toward more multimodal data through its synthesis.



Eshaan: Differences in the papers
The most obvious difference about these papers is what exactly the computation is being used for. The SONICS paper is doing something similar to forensic work. It’s trying to figure out if a song is real or AI generated. It’s a yes or no question, and the music itself doesn't really need to "mean" anything for the model to work. Comparinh that to the Spotify playlists paper, which is trying to infer personal traits like personality and gender from what people listen to. These are two completely different goals, and they define how each paper handles its data. The AVMeme Exam paper goes a different direction because it's actually testing AI models on whether they can understand cultural meaning. In this case, computation is the tool that's being looked at. And then the emotion prediction paper is also doing its own thing. It’s trying to map something as subjective as how a song makes you feel into a predictable output. Each paper has a different answer to the question of "what is computation supposed to do here". 

The papers also look at music data differently. In the SONICS paper, a song is basically a waveform. The researchers don't care what the lyrics mean or what genre it falls into, they care about the signal and whether it was generated by a machine. The genre classification paper is kind of the opposite. It argues that you actually need album art and text reviews alongside audio to properly classify something into a genre, which implies genre is partly a visual and social thing. The Spotify paper treats playlists as behavioral data, but then depicts them as "cultural expression".
The papers also don't agree on how much data you actually need. The SONICS dataset has around 97,000 songs, while the Spotify paper only has 739 users. The AVMeme benchmark has about 1,000 clips, and the emotion paper works with direct human responses which are way harder to collect at scale. But the interesting part isn't just the numbers. It's that each paper has a different idea about what makes a dataset valuable. SONICS needed volume because it was training a binary classifier and more data means a better generalization. AVMeme is a lot smaller and very annotated because depth of cultural context matters more than just a quantity for what it was trying to test. The Spotify paper is somewhere in between, where it's large enough to train a neural network but small enough to the point where the self selection bias from survey participants becomes a pretty big concern.
Finally, there's disagreement about whether using multiple types of data actually helps. The genre classification paper makes the strongest case for multimodal approaches, fusing audio, images, text, and data together. But even that paper found cases where adding text actually made accuracy worse because of subjective reviewer bias, which makes the whole "more data types equals better results" idea more complex. The AVMeme paper is multimodal because it has to be since you can't separate a meme's audio from its visual component without destroying what makes it a meme. The emotion paper combines music features with physiological signals like heart rate, which is multimodal in a different sense since it's not combining different representations of the music, it's combining the music with the listener's body. And the Spotify paper is basically unimodal, working just with playlist composition. 


Rohan: Things all papers missed
After looking at all the papers from Inika, Raymond, Beau, and Eshaan, I noticed that there are some important things that none of the papers really talk about.
First, none of the papers clearly explain who decides the labels they use. For example, in my paper, emotions like “happy” or “sad” are used, and in Beau’s paper, genres are used. Inika’s paper predicts personality, and Raymond’s paper tries to detect if songs are real or fake. But in all of these cases, we don’t really question who created these labels or how accurate they are. These labels are treated like facts, but they are actually subjective and can change depending on culture or context.
Second, all the papers assume that data represents reality. For example, Inika’s paper uses Spotify playlists to understand identity, and my paper uses people’s responses to music. But just because data exists does not mean it fully represents real life. People’s playlists or responses may not capture everything about who they are or how they feel. This assumption is not really questioned.
Another important silence is cultural context. Eshaan’s paper talks about cultural understanding, but even then, most of the computational methods still reduce culture into something measurable. In Beau’s paper, music genres are classified using data like audio, images, and text, but the deeper cultural meaning behind genres is not fully explored. Overall, the papers focus more on patterns and numbers instead of real cultural experiences.
I also noticed that none of the papers really talk about bias in the data. For example, datasets might include certain types of music, languages, or groups of people more than others. This can affect the results, but it is not deeply discussed in any of the papers.
Finally, there are ethical issues that are mostly ignored. Inika’s paper tries to predict personality from playlists, and my paper predicts emotions from music. This can be risky because it can lead to wrong assumptions about people. Just because a model predicts something does not mean it is true or fair.
Overall, I think all the papers focus a lot on what computation can do, but they do not spend enough time thinking about its limits, risks, and impact. They show strong technical results, but they miss deeper questions about meaning, bias, and ethics.