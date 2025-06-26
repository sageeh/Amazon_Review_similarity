# Amazon_Review_similarity
This project is developed as part of the "Algorithms for Massive Datasets" exam, focusing on detecting similar book reviews from a large dataset.

# Project Overview
The primary goal of this project is to implement a system for identifying pairs of similar book reviews from the Amazon Books Review dataset. This is achieved by leveraging approximate similarity detection techniques: Shingling, MinHashing, and Locality Sensitive Hashing (LSH).

# Setup and Configuration
To run this project, you will need to configure your Kaggle API credentials to download the dataset.

Kaggle API Authentication:
You must provide your Kaggle API username and key. These should be stored as environment variables or used directly in the code . In the provided Python code, it uses google.colab.userdata

 * Important Note: 
 Do not change the names of these secret keys as Kaggle's API may not work if changed:

KAGGLE_USERNAME

KAGGLE_KEY

~ Example of how they are used in the code:

import os
from google.colab import userdata
* os.environ["KAGGLE_USERNAME"] = userdata.get('KAGGLE_USERNAME')
* os.environ["KAGGLE_KEY"] = userdata.get('KAGGLE_KEY')

Dataset Download:
The project automatically downloads the mohamedbakhet/amazon-books-reviews dataset from Kaggle if it's not found locally.

# Global Variables
The project's behavior can be configured using the following global variables defined at the beginning of the project : 

* SUBSAMPLE_DATA: A boolean variable that determines whether to use a subsample of the data or the entire dataset.

True: The dataset will be subsampled, and SUBSAMPLE_SIZE will be used.

False: The entire filtered dataset will be processed.

* SUBSAMPLE_SIZE: An integer value that specifies the number of reviews to use if SUBSAMPLE_DATA is set to True.

* DATASET_LINK: The Kaggle identifier for the dataset to be downloaded (e.g., "mohamedbakhet/amazon-books-reviews").

* CSV_FILE_NAME: The name of the CSV file within the downloaded dataset that contains the reviews (e.g., "Books_rating.csv").

~ MinHash Parameters
 * NUM_PERMUTATIONS: The number of hash functions (permutations) used for MinHashing. A higher value leads to more accurate Jaccard similarity estimates but increases computation time and signature size.
Default: 128

* MINHASH_PRIME_MODULO: A large prime number used in the hash function calculations to ensure a good distribution of hash values. It should be smaller than 2 
32
 −1.

Default: 2**31 - 1

~ LSH Parameters
 * NUM_BANDS: The number of bands into which each MinHash signature is divided for LSH. This influences the trade-off between precision and recall in candidate pair generation.

Default: 32

* Constraint: NUM_PERMUTATIONS must be perfectly divisible by NUM_BANDS. An error will be raised if this condition is not met.

* ROWS_PER_BAND: The number of rows (MinHash values) in each band. This is automatically calculated as NUM_PERMUTATIONS // NUM_BANDS.

* SIMILARITY_THRESHOLD: A float value (between 0 and 1) that defines the minimum MinHash Jaccard similarity score required for two pairs to be considered "similar" and included in the final results.

Default: 0.6

* TOP_N_SIMILAR_PAIRS: The number of top similar pairs (sorted by similarity score) to display at the end of the execution.

Default: 10

* k_shingle_size: The size of the contiguous word sequences (k-shingles) used for text preprocessing. A value of 1 means individual words are used as shingles (unigrams).

Default: 1

