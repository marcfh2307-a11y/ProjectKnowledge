# Spotify Music Tracks Ontology

An OWL 2 ontology developed for the **Ontology Engineering** course at the **Universitat Autònoma de Barcelona (UAB)**.

## Project Overview

This ontology formally conceptualizes the domain of recorded music tracks, musical releases, artists, genres, and psychoacoustic audio features based on the **Kaggle Spotify Tracks Dataset**.

* **Open Data Repository:** [Spotify Tracks Dataset (Maharshi Pandya)](https://www.kaggle.com/datasets/maharshipandya/spotify-tracks-dataset)
* **Dataset Scope:** 114,000 tracks across 114 musical genres with 20 metadata and acoustic features.
* **Format:** OWL 2 in RDF/XML syntax (`spotify_music_tracks_ontology.owl`).

## Repository Contents

* `spotify_music_tracks_ontology.owl`: The complete OWL 2 ontology ready to open in Protégé 5.6.9.
* `Ontology_Engineering_Assignment_Music_Spotify.md`: Complete assignment report, including:
  * 24 Competency Questions categorized across taxonomy, properties, pragmatics, and dataset-specific queries.
  * Class hierarchy and property definitions.
  * LLM-assisted methodology declaration and prompts.
* `class_hierarchy.txt`: ASCII tree representation of the class taxonomy.
* Course reference materials:
  * `2026-10-08 Ontology Engineering.pdf`: Lecture slides and assignment instructions.
  * `Protege 5 New OWL Pizza Tutorial V3.2.pdf`: Protégé 5 tutorial guide.

## How to Open in Protégé

1. Download or open [Protégé](https://protege.stanford.edu/) (version 5.6+).
2. Go to `File` > `Open...`.
3. Select `spotify_music_tracks_ontology.owl`.
4. Navigate to the **Entities** > **Classes** tab to inspect the hierarchy and disjointness axioms.
