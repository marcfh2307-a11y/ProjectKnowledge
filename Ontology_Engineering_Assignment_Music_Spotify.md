# Ontology Engineering Assignment: Spotify Music Tracks Ontology

**Course:** Ontology Engineering  
**Academic Institution:** Universitat Autònoma de Barcelona (UAB)  
**Submission Deadline:** 21st October 2026, 23:59 h  
**Domain:** Music (Audio Tracks, Releases, Artists, Genres & Acoustic Features)  
**Deliverable File:** `spotify_music_tracks_ontology.owl` (OWL 2 RDF/XML)

---

## 1. Selected Open Data Repository

* **Dataset Name:** Spotify Tracks Dataset (by Maharshi Pandya)
* **Repository URL:** [https://www.kaggle.com/datasets/maharshipandya/spotify-tracks-dataset](https://www.kaggle.com/datasets/maharshipandya/spotify-tracks-dataset)
* **Format:** Tabular CSV / Open Dataset
* **Size & Scope:** 114,000 recorded audio tracks spanning 114 diverse musical genres, annotated with 20 acoustic, musical, and editorial metadata features.
* **Key Columns:**
  * **Metadata:** `track_id`, `artists`, `album_name`, `track_name`, `popularity`, `duration_ms`, `explicit`
  * **Acoustic & Perceptual Features:** `danceability`, `energy`, `key`, `loudness`, `mode`, `speechiness`, `acousticness`, `instrumentalness`, `liveness`, `valence`, `tempo`, `time_signature`, `track_genre`

---

## 2. Ontology Engineering Methodology

Following the 7-step ontology development methodology presented in the course:

### Step 1: Determine Domain and Scope
* **Domain:** Music recordings, commercial releases, musical artists, genre taxonomies, and acoustic/perceptual features of sound recordings.
* **Purpose:** To formally represent, classify, and query musical tracks and their acoustic profiles, enabling automated classification (e.g., distinguishing live vs. studio recordings, danceable vs. low-energy music, explicit vs. clean tracks) and semantic reasoning over music libraries.
* **Target Users:** Musicologists, streaming platform recommendation engines, automated playlist curation systems, and audio data engineers.

### Step 2: Consider Reusing Existing Ontologies
The design is informed by established Semantic Web vocabularies:
* **The Music Ontology (`mo:`)**: For foundational concepts (`mo:Track`, `mo:MusicArtist`, `mo:Record`).
* **Dublin Core (`dc:`)**: For bibliographic metadata (`dc:title`, `dc:creator`, `dc:date`).
* **Friend of a Friend (`foaf:`)**: For artist and group modeling (`foaf:Person`, `foaf:Group`).

### Step 3: Enumerate Important Terms
* *Entities:* AudioTrack, StudioRecordingTrack, LiveRecordingTrack, AcousticTrack, SynthesizedTrack, InstrumentalTrack, VocalTrack, ExplicitTrack, CleanTrack, HighEnergyTrack, LowEnergyTrack, DanceableTrack, MusicRelease, AlbumRelease, SingleRelease, EPRelease, CompilationRelease, MusicContributor, SoloArtist, MusicGroup, MusicalGenre, PopGenre, RockGenre, ElectronicGenre, HipHopGenre, ClassicalGenre, JazzGenre, LatinGenre, FolkGenre, MetalGenre, AmbientGenre, AudioFeature, RhythmFeature, PerceptualFeature, Tempo, TimeSignature, Danceability, Energy, Valence, Loudness, Acousticness, Speechiness, Instrumentalness, Liveness, MusicalKey, MusicalModality, MajorMode, MinorMode.

### Step 4: Define Classes and Class Hierarchy
Formal `IS-A` taxonomy implemented in OWL 2 with `rdfs:subClassOf` and disjointness axioms (`owl:AllDisjointClasses`, `owl:disjointWith`).

### Step 5 & 6: Define Properties of Classes and Characteristics
* **Object Properties:**
  * `hasArtist` (AudioTrack $\rightarrow$ MusicContributor)
  * `isArtistOf` (MusicContributor $\rightarrow$ AudioTrack, inverse of `hasArtist`)
  * `belongsToRelease` (AudioTrack $\rightarrow$ MusicRelease, Functional)
  * `hasTrack` (MusicRelease $\rightarrow$ AudioTrack, inverse of `belongsToRelease`)
  * `hasGenre` (AudioTrack $\rightarrow$ MusicalGenre)
  * `hasModality` (AudioTrack $\rightarrow$ MusicalModality, Functional)
  * `hasMusicalKey` (AudioTrack $\rightarrow$ MusicalKey, Functional)
* **Data Properties:**
  * `spotifyTrackId` (xsd:string)
  * `trackTitle` (xsd:string)
  * `albumTitle` (xsd:string)
  * `artistName` (xsd:string)
  * `durationMs` (xsd:integer)
  * `isExplicit` (xsd:boolean)
  * `popularityScore` (xsd:integer, 0-100)
  * `danceabilityScore` (xsd:float, 0.0-1.0)
  * `energyScore` (xsd:float, 0.0-1.0)
  * `loudnessDecibels` (xsd:float)
  * `speechinessScore` (xsd:float, 0.0-1.0)
  * `acousticnessScore` (xsd:float, 0.0-1.0)
  * `instrumentalnessScore` (xsd:float, 0.0-1.0)
  * `livenessScore` (xsd:float, 0.0-1.0)
  * `valenceScore` (xsd:float, 0.0-1.0)
  * `tempoBpm` (xsd:float)
  * `timeSignatureValue` (xsd:integer)

---

## 3. List of 24 Competency Questions (CQs)

Following the 4 categories established on Slide 4 of the lecture slides:

### Category A: CQs about the Taxonomy of Music Tracks and Entities
1. **CQ 1.1:** Is an `InstrumentalTrack` considered a subclass of `AudioTrack`?
2. **CQ 1.2:** What are the primary types of `MusicRelease` distinguished in the ontology (e.g., Album, Single, EP, Compilation)?
3. **CQ 1.3:** Is an `ExplicitTrack` categorized as a specialized subtype of `VocalTrack`?
4. **CQ 1.4:** Can a musical contributor be both a `SoloArtist` and a `MusicGroup` at the same time, or are they declared disjoint?
5. **CQ 1.5:** What are the broad parent genre families into which specific musical genres are grouped (e.g., Rock, Electronic, Classical, Pop, Latin)?
6. **CQ 1.6:** How are acoustic features taxonomically structured between rhythm-based features (`RhythmFeature`) and psychoacoustic perceptual features (`PerceptualFeature`)?

### Category B: CQs about Music Track Properties
7. **CQ 2.1:** What data type and allowable range are specified for `danceabilityScore` and `energyScore` (e.g., `xsd:float` between 0.0 and 1.0)?
8. **CQ 2.2:** Can an `AudioTrack` belong to more than one `MusicRelease` under functional property constraints?
9. **CQ 2.3:** What object properties link an `AudioTrack` to its performing `MusicContributor` and its inverse?
10. **CQ 2.4:** What property defines whether a track has radio-safe or advisory explicit lyrical content (`isExplicit` as `xsd:boolean`)?
11. **CQ 2.5:** Which musical modality types (`MajorMode` vs `MinorMode`) can be associated with an audio track via `hasModality`?
12. **CQ 2.6:** What is the unit of measurement and data property used for track speed (`tempoBpm` measured in beats per minute)?

### Category C: CQs about the Pragmatics of Music Tracks
13. **CQ 3.1:** Which tracks should be recommended for a fitness workout playlist based on having high energy ($\ge 0.7$) and high tempo ($> 125$ BPM)?
14. **CQ 3.2:** Which tracks require parental advisory warnings or restriction in child-friendly radio broadcasts based on explicit status?
15. **CQ 3.3:** Which tracks qualify as relaxing or meditation ambient music based on high acousticness ($\ge 0.7$), low energy ($< 0.3$), and absence of vocals?
16. **CQ 3.4:** How can a live concert performance recording be automatically distinguished from a polished studio take based on audience presence (`livenessScore` $\ge 0.8$)?
17. **CQ 3.5:** Which tracks are optimal for dance club venues according to high danceability ($\ge 0.7$) and a regular 4/4 time signature?
18. **CQ 3.6:** Which musical tracks convey an uplifting or positive emotional tone based on high valence ($\ge 0.7$)?

### Category D: CQs Relevant to the Particular Spotify Dataset
19. **CQ 4.1:** How many tracks in the dataset have an explicit flag (`explicit == True`)?
20. **CQ 4.2:** Which artist has the highest number of distinct track recordings in the dataset?
21. **CQ 4.3:** What percentage of tracks in the dataset are composed in a Major mode compared to a Minor mode?
22. **CQ 4.4:** What is the average tempo (BPM) and loudness (dB) of tracks categorized under the "electronic" and "metal" genres?
23. **CQ 4.5:** Which tracks have a `popularityScore` greater than 90 out of 100?
24. **CQ 4.6:** What is the average duration in seconds for tracks across different release types?

---

## 4. Class Hierarchy (IS-A Taxonomy)

The ontology structure implemented in `spotify_music_tracks_ontology.owl`:

```text
owl:Thing
└── MusicEntity
    ├── AudioTrack
    │   ├── AcousticTrack
    │   ├── SynthesizedTrack
    │   ├── StudioRecordingTrack   [Disjoint with LiveRecordingTrack]
    │   ├── LiveRecordingTrack
    │   ├── InstrumentalTrack
    │   ├── VocalTrack
    │   │   ├── CleanTrack         [Disjoint with ExplicitTrack]
    │   │   └── ExplicitTrack
    │   ├── DanceableTrack
    │   ├── HighEnergyTrack        [Disjoint with LowEnergyTrack]
    │   └── LowEnergyTrack
    ├── MusicRelease               [AllDisjoint: Album, Single, EP, Compilation]
    │   ├── AlbumRelease
    │   ├── SingleRelease
    │   ├── EPRelease
    │   └── CompilationRelease
    ├── MusicContributor           [Disjoint: SoloArtist, MusicGroup]
    │   ├── SoloArtist
    │   └── MusicGroup
    ├── MusicalGenre               [AllDisjoint: across distinct genre families]
    │   ├── PopGenre
    │   ├── RockGenre
    │   ├── ElectronicGenre
    │   ├── HipHopGenre
    │   ├── ClassicalGenre
    │   ├── JazzGenre
    │   ├── LatinGenre
    │   ├── FolkGenre
    │   ├── MetalGenre
    │   └── AmbientGenre
    ├── AudioFeature               [Disjoint: RhythmFeature, PerceptualFeature]
    │   ├── RhythmFeature
    │   │   ├── TempoFeature
    │   │   └── TimeSignatureFeature
    │   └── PerceptualFeature
    │       ├── DanceabilityFeature
    │       ├── EnergyFeature
    │       ├── ValenceFeature
    │       ├── AcousticnessFeature
    │       ├── InstrumentalnessFeature
    │       ├── LivenessFeature
    │       ├── SpeechinessFeature
    │       └── LoudnessFeature
    ├── MusicalKey
    └── MusicalModality            [Disjoint: MajorMode, MinorMode]
        ├── MajorMode
        └── MinorMode
```

---

## 5. Declaration of Models and Prompts Used (LLM-based Methodology)

Following the specification of Slide 13 and Slide 15 of `2026-10-08 Ontology Engineering.pdf`:

### Model Declaration
* **AI Model:** Google Gemini 3.8 Flash
* **Platform:** Antigravity IDE (Agentic Coding Environment)
* **Date of Generation:** October 2026

### Main Prompt Used

```text
Role: You are an expert Ontology Engineer specialising in the domain of music information retrieval and semantic audio representation.

Objective: Develop a formal taxonomy of music tracks, releases, artists, musical genres, and acoustic features as an IS-A class hierarchy, written in OWL 2 in RDF/XML syntax, as the first step of an ontology engineering process based on the Kaggle Spotify Tracks Dataset.

Scope & Domain:
• Domain: The taxonomy covers musical tracks, commercial releases, musical artists, genre families, and the acoustic/perceptual features defined in the Kaggle Spotify Tracks Dataset (114k tracks across 114 genres).
• Key Entities: The class hierarchy must be rooted in MusicEntity, containing AudioTrack, MusicRelease, MusicContributor, MusicalGenre, AudioFeature, MusicalKey, and MusicalModality. Subclasses must model specific track types (AcousticTrack, SynthesizedTrack, LiveRecordingTrack, StudioRecordingTrack, ExplicitTrack, CleanTrack, DanceableTrack, HighEnergyTrack, LowEnergyTrack), release types (AlbumRelease, SingleRelease, EPRelease, CompilationRelease), artist types (SoloArtist, MusicGroup), genre families, and audio features.
• Boundaries: Focus on the musical and audio feature metadata present in the Spotify dataset. Do not include unrelated physical distribution details or retail e-commerce inventory.

Competency Questions: When developing the taxonomy, ensure the ontology can answer competency questions across:
1. Taxonomy of music tracks and entities
2. Music track properties and value ranges
3. Pragmatics of playlist curation and content advisory
4. Dataset-specific quantitative questions

Structural Requirements: 
• Add disjointness axioms (owl:AllDisjointClasses and owl:disjointWith) to keep mutually exclusive concepts separate (e.g. SoloArtist vs MusicGroup, ExplicitTrack vs CleanTrack, MajorMode vs MinorMode, AlbumRelease vs SingleRelease).
• Provide rdfs:label and rdfs:comment for all classes and properties.
• Include object properties (hasArtist, belongsToRelease, hasGenre, hasModality, hasMusicalKey) and data properties (spotifyTrackId, trackTitle, albumTitle, artistName, durationMs, isExplicit, popularityScore, danceabilityScore, energyScore, loudnessDecibels, tempoBpm, valenceScore).

Output Format: Generate the ontology in strictly valid OWL 2 RDF/XML syntax compatible with Protégé 5.6.9.
```
