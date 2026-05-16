# Dataset Documentation - Underground Spotify Songs

## 1. Dataset Information

| Field | Value |
|---|---|
| **Dataset name** | Underground Spotify Songs - IS310 Scaled Dataset |
| **Output file** | `scaledDataset.csv` (in this directory) |
| **Author** | Raymond Zhang |
| **Date created** | May 2026 |
| **Source dataset** | Kaggle - "Spotify Tracks Dataset" by Maharshi Pandya |
| **Source URL** | https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset |
| **Source size** | 114,000 rows × 22 columns |
| **Final dataset size** | ~52,651 rows × 21 columns |

My bespoke initial dataset (`smallDataset.csv`, ~100 songs) is also included for reference.

---

## 2. Purpose and Scope

The original focus in my initial dataset submission was to try and find "dark horses" among charted songs, but this was difficult as I didn't have a good way to get chart data. Additionally, it would be difficult for even small scale data, as I'm not super familiar with many songs, so it would be unfair to ask me to judge a song's "dark horse value". Furthermore, it would be difficult to scale, since now we need a computational method that's able to tell a dark horse apart from regular charted songs. As such, I made the decision to pivot to something more computationally friendly. 

This dataset is a curated sample of "underground" songs from Spotify, which are tracks that have a meaningful listener base but have not broken into mainstream popularity. My working definition of "underground" for this project is a Spotify popularity score between **5 and 60** (inclusive).

A score of 5 corresponds roughly to a song that has been discovered and played by real listeners a decent amount, but still remains largely unknown to a layperson audience. A score of 60 represents songs that may be known to several million people but are not chart-level hits. This range was chosen to capture songs in approximately the 10,000 to a few million streams range, songs that matter culturally to their audiences but have not achieved mass commercial success.

This boundary is somewhat arbitrarily picked after some rough EDA visualization, not a cultural fact. A song at popularity 61 is not meaningfully more "mainstream" than one at 60; the threshold is merely to set a boundary.

The dataset was created using an auditing approach: rather than creating new data from scratch, it filters an existing publicly available dataset that was originally collected using the Spotify Web API.


---

## 3. Column Descriptions

| Column | Type | Description | Notes |
|---|---|---|---|
| `track_id` | string | Spotify track URI - unique identifier for each song | Primary key; used for deduplication |
| `artists` | string | Artist name(s) | Multiple artists are semicolon-separated |
| `album_name` | string | Name of the album the track appears on | |
| `track_name` | string | Song title | |
| `popularity` | integer | Spotify popularity score, 0-100 | Computed by Spotify; higher = more popular; time-stamped snapshot |
| `duration_ms` | integer | Track duration in milliseconds | Divide by 60,000 for minutes |
| `explicit` | boolean | Whether the track has explicit lyrics | True/False |
| `danceability` | float (0–1) | How suitable a track is for dancing | Spotify proprietary MIR feature; higher = more danceable |
| `energy` | float (0–1) | Perceptual measure of intensity and activity | Spotify proprietary; fast, loud, noisy tracks score high |
| `key` | integer (0–11) | Estimated musical key using pitch class notation | 0 = C, 1 = C#/Db, 2 = D, … 11 = B; -1 = no key detected |
| `loudness` | float (dB) | Overall loudness of the track | Typically –60 to 0 dB; values closer to 0 are louder |
| `mode` | integer (0 or 1) | Modality of the track | 1 = Major, 0 = Minor |
| `speechiness` | float (0–1) | Presence of spoken words | >0.66 = likely spoken word; 0.33–0.66 = mix; <0.33 = music |
| `acousticness` | float (0–1) | Confidence that the track is acoustic | 1.0 = high confidence acoustic |
| `instrumentalness` | float (0–1) | Predicts whether a track has no vocals | Values >0.5 suggest instrumental; closer to 1.0 = more likely instrumental |
| `liveness` | float (0–1) | Detects presence of a live audience | >0.8 = strong likelihood of live recording |
| `valence` | float (0–1) | Musical positiveness conveyed by the track | High valence = sounds happy/cheerful; low = sounds sad/angry |
| `tempo` | float (BPM) | Estimated beats per minute | Estimated by Spotify's algorithm |
| `time_signature` | integer | Estimated time signature | Estimated meter; ranges from 3 to 7 (e.g., 4 = common time) |
| `track_genre` | string | Spotify genre tag assigned to the track | One genre per row in source; duplicates removed during deduplication |

**Note:** All audio features (danceability, energy, valence, etc.) are computed by Spotify's proprietary algorithms. Their exact methodologies and training data are not publicly disclosed, and it would be very nice if they were more transparent about how they obtained completely subjective metrics like "instrumentalness". 

---

## 4. Filtering Criteria

The following three filters were applied in sequence using the notebook `is310final.ipynb`:

### Step 1 Popularity Filter
Kept only rows where `5 ≤ popularity ≤ 60`.

- Removes tracks with essentially no listener activity (popularity 0–4)
- Removes mainstream/chart-level hits (popularity 61–100)
- Starting pool after this filter: approximately 80,000 rows

### Step 2 English-Language Genre Filter
Excluded rows where `track_genre` matched any of the following 28 tags (case-insensitive):

```
k-pop, cantopop, mandopop, latin, latino, salsa, turkish, samba, tango,
mpb, pagode, sertanejo, forro, romance, french, german, spanish, iranian,
j-pop, j-dance, j-idol, j-rock, malay, reggaeton, brazil, swedish, indian, anime
```

This filter is a **proxy for language**, not a guarantee. Some English-language songs may appear in these genres and were excluded; some non-English songs may appear in genres not on this list and were retained. The filter reduces non-English content but does not eliminate it.

Genres such as `afrobeat`, `reggae`, `world-music`, `opera`, `british`, and `bluegrass` were intentionally kept as predominantly English-language or English-adjacent genres.

- Pool after this filter: approximately 52,000 rows

### Step 3: Deduplication
In the source dataset, the same track may appear in multiple rows under different genre labels. Duplicate `track_id` values were removed, keeping the first occurrence.

- Pool after deduplication: approximately 52,000 unique tracks

---

## 5. Limitations

1. **Popularity is a snapshot.** Spotify popularity scores are recalculated continuously based on recent streaming activity. The scores in this dataset reflect the state of the platform at the time the Kaggle dataset was collected, not the present day. Popularity can rise and fall, and it would be unfair to compare a newer song on its rise to Gangnam Style, both with popularity snapshots taken at the same time. 

2. **Audio features are opaque.** All numeric audio features (danceability, energy, valence, etc.) are somewhat of a black box from Spotify. Their precise definitions, training data, and computational methods are not publicly available. The data appears clean and standardized but carries hidden assumptions that cannot be fully verified. For popularity, we cannot verify how they actually computed the values. For the betterment of research and human knowledge, Spotify should open up their methods. 

3. **The genre filter is imperfect as a language proxy.** Genre tags are assigned by Spotify's classification system, which categorizes by musical style, not language. This means the filter is a reasonable approximation but not a rigorous linguistic filter.

4. **The "underground" threshold is arbitrary.** The popularity range 5–60 is an (almost) arbitrary decision made for this project based on EDA. Different thresholds would produce materially different datasets, and there is no universally agreed definition of what makes a song "underground" asides from one's own knowledge and beliefs that positions a song as "underground". 

6. **Source dataset provenance.** The Kaggle dataset was assembled and cleaned by a third party using the Spotify Web API. The exact collection date, API version, and cleaning procedures are not fully documented by the original author, and there's no real good way to verify that this data hasn't been tampered with before the author posted it. In the future, we should get the data ourselves from the API. 

---

## 6. How Computation Shaped This Dataset

### Role of Computation

The central computational contribution of this project is the transformation of a 114,000-row dataset into a focused ~52,000-song corpus through automated filtering. Applying three sequential filters in pandas: a popularity threshold, a genre-based language proxy, and deduplication on track identifiers reduced the source data by roughly 54% in seconds. This is a task that would be practically impossible through manual review alone, and is generally impossible scaling farther. However, the speed and scale of computation also introduces a form of opacity, which is the genre filter used to approximate Englishl anguage content relies entirely on Spotify's own genre taxonomy, which is itself an output of Spotify's classification algorithms rather than a human editorial system (Eriksson et al., 2019). In other words, the "English-language" filter is built on a classification that was already computational before we touched it.

### How Scale Changes the Dataset

The initial bespoke dataset of approximately 100 songs was small enough that a researcher could plausibly listen to every track and verify its inclusion. Scaling to ~52,000 songs eliminates that possibility entirely. This represents a fundamental epistemological shift: at 100 songs, the dataset is "known" in a direct, empirical sense. At 52,000, it is known only statistically - through distributions, means, and correlations rather than individual familiarity. The correlation heatmap and feature distributions in the notebook are precisely the tools that replace individual track-level knowledge at scale. Tzanetakis and Cook (2002) identified this tradeoff early in the music information retrieval literature: computational feature extraction gains breadth at the cost of interpretive depth.

---

## 8. Limitations, Ethics, and Privacy

### Limitations and Qualifications

1. **The popularity threshold is analytical, not culturally meaningful.** A song with a popularity score of 61 is not meaningfully more "mainstream" than one at 60. The 5–60 range was chosen to represent an approximate listener count range (roughly 10,000 to a few million streams) but this boundary is a methodological convenience, not a cultural fact.

2. **Spotify's audio features are proprietary and opaque.** Danceability, valence, energy, and other features are computed by Spotify's internal algorithms, whose training data, weightings, and definitions are not publicly disclosed. What "valence" means precisely - and whether it measures what we intuitively think of as musical positivity — cannot be independently verified. As the initial documentation noted, Pumped Up Kicks illustrates this: an energetic-sounding song can carry deeply un-energetic content that the algorithm cannot detect.

3. **The genre filter is a language proxy, not a guarantee.** Some songs in ostensibly English genres (e.g., "indie", "pop") are performed in other languages, and some English-language songs may have been excluded because their genre tag was on the exclusion list. The filter reduces non-English content; it does not eliminate it.

4. **Popularity scores are time-stamped snapshots.** The Kaggle dataset was collected at a specific point in time. A song's popularity score on Spotify fluctuates continuously, so the dataset represents one moment rather than a stable property of each track.

### Ethical and Privacy Considerations

All data used in this project is publicly available through the Spotify Web API and was accessed via an existing Kaggle dataset. No personally identifying information about listeners is included; popularity scores are aggregated metrics, not individual listener records. The primary ethical concern is not privacy but representation: by relying on Spotify's genre taxonomy and popularity metrics, this dataset inherits the platform's structural biases. Artists and genres that Spotify's algorithm systematically undervalues or miscategorizes will be underrepresented or misclassified in this dataset, independent of any choices made in curation. Drott (2018) describes this dynamic in detail, arguing that streaming platforms' recommendation and classification systems actively shape which cultural works receive attention, whih a a process that is especially consequential for the "underground" artists this dataset aims to center.

---

## 9. Situating the Work in Scholarship

This project sits at the intersection of three bodies of peer-reviewed scholarship:

### Music Information Retrieval (MIR)

The audio features used throughout this dataset: tempo, danceability, energy, valence, originate in MIR research. Tzanetakis and Cook (2002) established the foundational framework for computationally extracting rhythm, timbre, and pitch class from raw audio signals in their influential IEEE paper on musical genre classification. The Spotify feature set is an industrial-scale application of these same techniques. Engaging with this dataset therefore requires acknowledging that every numeric feature is a computational estimate of a perceptual quality, not an objective measurement.

> Tzanetakis, G., & Cook, P. (2002). Musical genre classification of audio signals. *IEEE Transactions on Speech and Audio Processing, 10*(5), 293–302. https://doi.org/10.1109/TSA.2002.800560

### Platform Studies

Eriksson et al. (2019) in *Spotify Teardown* conducted an extensive critical examination of Spotify's internal systems, documenting how the platform's recommendation engine, genre taxonomy, and data collection practices shape listener exposure in ways that are not transparent to users, artists, or researchers. This project's genre filter is a direct encounter with the limits described in that book: we are forced to use Spotify's categories to approximate a cultural distinction (English vs. non-English) that Spotify's system was not designed to capture.

> Eriksson, M., Fleischer, R., Johansson, A., Snickars, P., & Vonderau, P. (2019). *Spotify Teardown: Inside the Black Box of Streaming Music.* MIT Press.

### Data Ethics in Music

Drott (2018), writing in the peer-reviewed *Twentieth-Century Music*, examines the cultural and ethical stakes of streaming data collection and algorithmic recommendation. He argues that the aggregation of listening behavior into popularity metrics and recommendation scores is not a neutral act but a form of cultural curation that has measurable consequences for which artists and genres receive sustained listener attention. This dataset, by focusing on songs in the popularity range of 5–60, explicitly tries to work against the homogenizing pressure that Drott describes, but it cannot escape the platform's underlying infrastructure.

> Drott, E. (2018). Why the next song matters: Streaming, recommendation, interdependence. *Twentieth-Century Music, 15*(3), 325–357. https://doi.org/10.1017/S1478572218000269
