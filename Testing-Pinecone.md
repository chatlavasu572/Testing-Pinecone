# Testing-Pinecone in Service Catalog 
### What is Pinecone?
Pinecone is a vector database — it’s designed to store and search through vector embeddings efficiently and at scale.

### What are Vectors?
In AI/ML, when we process text, images, audio, etc., models (like OpenAI or Sentence Transformers) convert them into numerical representations called embeddings (vectors). These are just lists of numbers that represent semantic meaning.

![1_sAJdxEsDjsPMioHyzlN3_A](https://github.com/user-attachments/assets/76e1ccfa-4c79-4940-b966-22033079a12e)

### Why Use Pinecone?
Traditional databases (like MySQL or MongoDB) aren’t optimized for vector similarity search — they work with exact matches, not “closest meaning”.

#### Pinecone allows you to:

- Search by meaning (semantic search)

- Find similar items fast (e.g., similar texts, images, products)

- Store millions of embeddings

- Scale automatically with cloud-native performance

- Secure and production-ready
![image](https://github.com/user-attachments/assets/564ffae1-1912-49d4-82c8-61b2e5f6a63d)


  
### Firstly Creating a DUMMY-INSTANCE named DUMMMY_PINECONE in the AWS_CONSOLE.

![Screenshot from 2025-06-22 10-47-13](https://github.com/user-attachments/assets/3abfbc08-da04-4f28-9420-3e9f6465c01e)

### Next iam taking Ubutu OS AMI for launching an instance 

![Screenshot from 2025-06-22 10-47-34](https://github.com/user-attachments/assets/e89e208c-d62b-4077-9b19-8836aebd5480)


### Instance Type :t2.micro


![Screenshot from 2025-06-22 10-47-13](https://github.com/user-attachments/assets/25b75a29-a6fb-41f0-987a-f80793fed556)

### KeyPair Login 
create a key pair for connecting ssh-clinet to the local terminal 
![Screenshot from 2025-06-22 10-49-29](https://github.com/user-attachments/assets/e1faadd2-0fdf-4e35-a936-36dbade6c3dd)


### Network Settings 
allowing all HTTP,HTTPs,SSH traffic

![Screenshot from 2025-06-22 10-50-19](https://github.com/user-attachments/assets/9b3c46b8-807f-4709-88c0-38371c2cef87)

### Now launch an instance click on connect for conecting to the terminal in your local-machine with he help of ssh-clinet.


![Screenshot from 2025-06-22 11-02-18](https://github.com/user-attachments/assets/17312c8d-7f64-4777-8028-eca192708d5d)

### Now connect to the instance using browser based client

![Screenshot from 2025-06-22 11-02-31](https://github.com/user-attachments/assets/c06f1145-046a-45ab-b839-6c7cb136f917)

```
ssh -i "pineconekeypair.pem" ubuntu@ec2-13-233-98-208.ap-south-1.compute.amazonaws.com
```
![Screenshot from 2025-06-22 11-30-45](https://github.com/user-attachments/assets/f6adff91-29ee-49f3-8006-7b9de70a99fc)


### Now open browser search for PINECONE web ui : https://app.pinecone.io/ 

###  Why Do You Need a Pinecone API Key?
#### The Pinecone API key is required to:

- Authenticate your app or script

- Authorize access to your Pinecone account and indexes

- Track usage (read/write units) and billing

- Ensure security — so no one else can access your data without permission

![Screenshot from 2025-06-22 11-11-12](https://github.com/user-attachments/assets/3f4d8dab-d5c8-46de-8610-d06ced903c17)

now Iam Creating a pinecone API KEY :

![Screenshot from 2025-06-22 11-16-55](https://github.com/user-attachments/assets/628eb936-24a4-42b5-a6c9-18beefcf017e)

### Step-by-Step Guide to Install and Use Pinecone on Ubuntu

#### 1. Install Python (if not installed)
```
sudo apt update
sudo apt install python3 python3-pip -y
```
#### 2. Create and Activate a Virtual Environment
```
python3 -m venv pinecone-env
source pinecone-env/bin/activate
```
#### 3.Install the SDK for your preferred language
```
pip install pinecone
```
#### 4.Create an Index in Pinecone,
There are two types of indexes for storing vector data:Dense indexes store dense vectors for semantic search, and sparse indexes store sparse vectors for lexical/keyword search.

For this quickstart, create a dense index that is integrated with an embedding model hosted by Pinecone. With integrated models, you upsert and search with text and have Pinecone generate vectors automatically.

```
# Import the Pinecone library
from pinecone import Pinecone

# Initialize a Pinecone client with your API key
pc = Pinecone(api_key="{{YOUR_API_KEY}}")

# Create a dense index with integrated embedding
index_name = "quickstart-py"
if not pc.has_index(index_name):
    pc.create_index_for_model(
        name=index_name,
        cloud="aws",
        region="us-east-1",
        embed={
            "model":"llama-text-embed-v2",
            "field_map":{"text": "chunk_text"}
        }
    )
```
#### 5.Upsert text
Prepare a sample dataset of factual statements from different domains like history, physics, technology, and music. Model the data as as records with an ID, text, and category.
```

records = [
    { "_id": "rec1", "chunk_text": "The Eiffel Tower was completed in 1889 and stands in Paris, France.", "category": "history" },
    { "_id": "rec2", "chunk_text": "Photosynthesis allows plants to convert sunlight into energy.", "category": "science" },
    { "_id": "rec3", "chunk_text": "Albert Einstein developed the theory of relativity.", "category": "science" },
    { "_id": "rec4", "chunk_text": "The mitochondrion is often called the powerhouse of the cell.", "category": "biology" },
    { "_id": "rec5", "chunk_text": "Shakespeare wrote many famous plays, including Hamlet and Macbeth.", "category": "literature" },
    { "_id": "rec6", "chunk_text": "Water boils at 100°C under standard atmospheric pressure.", "category": "physics" },
    { "_id": "rec7", "chunk_text": "The Great Wall of China was built to protect against invasions.", "category": "history" },
    { "_id": "rec8", "chunk_text": "Honey never spoils due to its low moisture content and acidity.", "category": "food science" },
    { "_id": "rec9", "chunk_text": "The speed of light in a vacuum is approximately 299,792 km/s.", "category": "physics" },
    { "_id": "rec10", "chunk_text": "Newton's laws describe the motion of objects.", "category": "physics" },
    { "_id": "rec11", "chunk_text": "The human brain has approximately 86 billion neurons.", "category": "biology" },
    { "_id": "rec12", "chunk_text": "The Amazon Rainforest is one of the most biodiverse places on Earth.", "category": "geography" },
    { "_id": "rec13", "chunk_text": "Black holes have gravitational fields so strong that not even light can escape.", "category": "astronomy" },
    { "_id": "rec14", "chunk_text": "The periodic table organizes elements based on their atomic number.", "category": "chemistry" },
    { "_id": "rec15", "chunk_text": "Leonardo da Vinci painted the Mona Lisa.", "category": "art" },
    { "_id": "rec16", "chunk_text": "The internet revolutionized communication and information sharing.", "category": "technology" },
    { "_id": "rec17", "chunk_text": "The Pyramids of Giza are among the Seven Wonders of the Ancient World.", "category": "history" },
    { "_id": "rec18", "chunk_text": "Dogs have an incredible sense of smell, much stronger than humans.", "category": "biology" },
    { "_id": "rec19", "chunk_text": "The Pacific Ocean is the largest and deepest ocean on Earth.", "category": "geography" },
    { "_id": "rec20", "chunk_text": "Chess is a strategic game that originated in India.", "category": "games" },
    { "_id": "rec21", "chunk_text": "The Statue of Liberty was a gift from France to the United States.", "category": "history" },
    { "_id": "rec22", "chunk_text": "Coffee contains caffeine, a natural stimulant.", "category": "food science" },
    { "_id": "rec23", "chunk_text": "Thomas Edison invented the practical electric light bulb.", "category": "inventions" },
    { "_id": "rec24", "chunk_text": "The moon influences ocean tides due to gravitational pull.", "category": "astronomy" },
    { "_id": "rec25", "chunk_text": "DNA carries genetic information for all living organisms.", "category": "biology" },
    { "_id": "rec26", "chunk_text": "Rome was once the center of a vast empire.", "category": "history" },
    { "_id": "rec27", "chunk_text": "The Wright brothers pioneered human flight in 1903.", "category": "inventions" },
    { "_id": "rec28", "chunk_text": "Bananas are a good source of potassium.", "category": "nutrition" },
    { "_id": "rec29", "chunk_text": "The stock market fluctuates based on supply and demand.", "category": "economics" },
    { "_id": "rec30", "chunk_text": "A compass needle points toward the magnetic north pole.", "category": "navigation" },
    { "_id": "rec31", "chunk_text": "The universe is expanding, according to the Big Bang theory.", "category": "astronomy" },
    { "_id": "rec32", "chunk_text": "Elephants have excellent memory and strong social bonds.", "category": "biology" },
    { "_id": "rec33", "chunk_text": "The violin is a string instrument commonly used in orchestras.", "category": "music" },
    { "_id": "rec34", "chunk_text": "The heart pumps blood throughout the human body.", "category": "biology" },
    { "_id": "rec35", "chunk_text": "Ice cream melts when exposed to heat.", "category": "food science" },
    { "_id": "rec36", "chunk_text": "Solar panels convert sunlight into electricity.", "category": "technology" },
    { "_id": "rec37", "chunk_text": "The French Revolution began in 1789.", "category": "history" },
    { "_id": "rec38", "chunk_text": "The Taj Mahal is a mausoleum built by Emperor Shah Jahan.", "category": "history" },
    { "_id": "rec39", "chunk_text": "Rainbows are caused by light refracting through water droplets.", "category": "physics" },
    { "_id": "rec40", "chunk_text": "Mount Everest is the tallest mountain in the world.", "category": "geography" },
    { "_id": "rec41", "chunk_text": "Octopuses are highly intelligent marine creatures.", "category": "biology" },
    { "_id": "rec42", "chunk_text": "The speed of sound is around 343 meters per second in air.", "category": "physics" },
    { "_id": "rec43", "chunk_text": "Gravity keeps planets in orbit around the sun.", "category": "astronomy" },
    { "_id": "rec44", "chunk_text": "The Mediterranean diet is considered one of the healthiest in the world.", "category": "nutrition" },
    { "_id": "rec45", "chunk_text": "A haiku is a traditional Japanese poem with a 5-7-5 syllable structure.", "category": "literature" },
    { "_id": "rec46", "chunk_text": "The human body is made up of about 60% water.", "category": "biology" },
    { "_id": "rec47", "chunk_text": "The Industrial Revolution transformed manufacturing and transportation.", "category": "history" },
    { "_id": "rec48", "chunk_text": "Vincent van Gogh painted Starry Night.", "category": "art" },
    { "_id": "rec49", "chunk_text": "Airplanes fly due to the principles of lift and aerodynamics.", "category": "physics" },
    { "_id": "rec50", "chunk_text": "Renewable energy sources include wind, solar, and hydroelectric power.", "category": "energy" }
]
```
#### 6.Upsert the sample dataset into a new namespace in your index.

Because your index is integrated with an embedding model, you provide the textual statements and Pinecone converts them to dense vectors automatically.
```
# Target the index
dense_index = pc.Index(index_name)

# Upsert the records into a namespace
dense_index.upsert_records("example-namespace", records)
```
![Screenshot from 2025-06-22 12-20-08](https://github.com/user-attachments/assets/2d8e4479-b639-472a-bfd2-3842773a0707)

#### 7.Status of an Index 
Pinecone is eventually consistent, so there can be a slight delay before new or changed records are visible to queries. You can view index stats to check if the current vector count matches the number of vectors you upserted (50):
``` 

# Wait for the upserted vectors to be indexed
import time
time.sleep(10)

# View stats for the index
stats = dense_index.describe_index_stats()
print(stats)
```
you will see the ouput like this :

![Screenshot from 2025-06-22 12-17-53](https://github.com/user-attachments/assets/556c211e-45ac-441a-baca-8404e14e5f21)

#### 8.Semantic search
Search the dense index for ten records that are most semantically similar to the query, “Famous historical structures and monuments”.

Again, because your index is integrated with an embedding model, you provide the query as text and Pinecone converts the text to a dense vector automatically.

```
# Define the query
query = "Famous historical structures and monuments"

# Search the dense index
results = dense_index.search(
    namespace="example-namespace",
    query={
        "top_k": 10,
        "inputs": {
            'text': query
        }
    }
)

# Print the results
for hit in results['result']['hits']:
        print(f"id: {hit['_id']:<5} | score: {round(hit['_score'], 2):<5} | category: {hit['fields']['category']:<10} | text: {hit['fields']['chunk_text']:<50}")
```
you will see the output like this:

![Screenshot from 2025-06-22 12-39-39](https://github.com/user-attachments/assets/ded75206-9406-40b0-902d-fafa6a07a976)

The Final Ouput for "FOUR MONITORS" are:

#### 1.Connectivity check monitor in pinecone:

- Purpose: Verifies that the Pinecone endpoint is reachable and responsive.

- Status: Active – Ensures that the service is online and accessible from the environment.



```
#!/usr/bin/env python3
"""
Pinecone Connectivity Check

This script checks whether the Pinecone service is reachable and the API key is valid.

Environment Variables:
    PINECONE_API_KEY - Your Pinecone API key
    PINECONE_ENVIRONMENT - (Optional) Pinecone environment (e.g., us-west4-gcp)

Exit Codes:
    0 - Success (Pinecone is reachable)
    1 - Failure (Pinecone is unreachable)
"""

import logging
import os
import sys

from pinecone import Pinecone

# Setup logging
logging.basicConfig(
    level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s"
)

PINECONE_API_KEY = os.getenv("PINECONE_API_KEY","pcsk_239Y5A_739p25f8ZKU1s1cAXWbaokeN2eBkExxEsfi2QTWxy6Xa7YquJ2XqeqiMEsTXKKr")
if not PINECONE_API_KEY:
    logging.error("Missing required environment variable: PINECONE_API_KEY")
    sys.exit(1)

try:
    pc = Pinecone(api_key=PINECONE_API_KEY)
    indexes = pc.list_indexes().names()
    logging.info(f"Connected to Pinecone. Indexes available: {indexes}")
    sys.exit(0)
except Exception as e:
    logging.error(f"Failed to connect to Pinecone: {e}")
    sys.exit(1)
```
![Screenshot from 2025-06-22 12-49-01](https://github.com/user-attachments/assets/15c04ff5-30b2-4174-9161-884c88fec077)

#### 2.Index count monitor

- Purpose: Monitors the total number of vectors stored in the index.

- Status:  Active – Helps detect unusual growth patterns or unexpected deletions
```
#!/usr/bin/env python3
"""
Pinecone Index Count Check

This script verifies the number of indexes in a Pinecone environment.

Environment Variables:
    PINECONE_API_KEY - Your Pinecone API key (required)
    MAX_INDEX_COUNT - Maximum allowed number of indexes (default: 5)

Exit Codes:
    0 - Success (index count within limits)
    1 - Failure (index count exceeded or error occurred)
"""

import logging
import os
import sys

from pinecone import Pinecone

# Configure logging
logging.basicConfig(
    level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s"
)

API_KEY = os.getenv("PINECONE_API_KEY","pcsk_239Y5A_739p25f8ZKU1s1cAXWbaokeN2eBkExxEsfi2QTWxy6Xa7YquJ2XqeqiMEsTXKKr")
MAX_INDEX_COUNT = int(os.getenv("MAX_INDEX_COUNT", 5))

if not API_KEY:
    logging.error("PINECONE_API_KEY is required.")
    sys.exit(1)

try:
    pc = Pinecone(api_key=API_KEY)
    index_list = pc.list_indexes().names()

    index_count = len(index_list)
    logging.info(f"Found {index_count} indexes: {index_list}")

    if index_count > MAX_INDEX_COUNT:
        logging.warning(f"Index count exceeded: {index_count} > {MAX_INDEX_COUNT}")
        sys.exit(1)

    sys.exit(0)

except Exception as e:
    logging.error(f"Error fetching index list: {e}")
    sys.exit(1)
  ```
![Screenshot from 2025-06-22 12-55-00](https://github.com/user-attachments/assets/8c4ea73d-60c2-4981-8516-4e367cb35ca3)


#### 3.Index Stats Monitor

- Purpose: Retrieves and tracks index metadata like dimensions, size, and namespace usage.

- Status: Active – Confirms index configuration and growth are stable.

```
#!/usr/bin/env python3
"""
Pinecone Index Stats Monitor


This script fetches statistics for a specific Pinecone index.

Environment Variables:
    PINECONE_API_KEY - Pinecone API key (required)
    PINECONE_INDEX_NAME - Name of the index to check (required)

Exit Codes:
    0 - Success (stats retrieved)
    1 - Failure (index not found or error occurred)
"""

import logging
import os
import sys

from pinecone import Pinecone

# Logging config
logging.basicConfig(
    level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s"
)

API_KEY = os.getenv("PINECONE_API_KEY","pcsk_239Y5A_739p25f8ZKU1s1cAXWbaokeN2eBkExxEsfi2QTWxy6Xa7YquJ2XqeqiMEsTXKKr")
INDEX_NAME = os.getenv("PINECONE_INDEX_NAME","quickstart-py")
if not API_KEY or not INDEX_NAME:
    logging.error(
        "Environment variables PINECONE_API_KEY and PINECONE_INDEX_NAME are required."
    )
    sys.exit(1)

try:
    pc = Pinecone(api_key=API_KEY)
    index = pc.Index(INDEX_NAME)
    stats = index.describe_index_stats()
    logging.info(f"Index stats for '{INDEX_NAME}': {stats}")
    sys.exit(0)

except Exception as e:
    logging.error(f"Failed to fetch index stats: {e}")
    sys.exit(1)
```
![Screenshot from 2025-06-22 12-54-10](https://github.com/user-attachments/assets/ee4e6609-4872-4a88-8638-e13dcd520dea)
#### 4.Query Latency Monitor

- Purpose: Measures the time taken to execute vector similarity queries.

- Status:  Active – Ensures query performance remains within acceptable limits.
```
#!/usr/bin/env python3
"""
Pinecone Query Latency Check

This script measures latency of a basic vector search query against a Pinecone index.

Environment Variables:
    PINECONE_API_KEY - Pinecone API key
    PINECONE_INDEX_NAME - The name of the index to query
    PINECONE_ENVIRONMENT - Cloud region/environment (e.g., aws, gcp)
    PINECONE_REGION - Region (e.g., us-east-1)

Exit Codes:
    0 - Success (query completed within acceptable latency)
    1 - Failure (query failed or took too long)
"""

import logging
import os
import sys
import time

from pinecone import Pinecone

# Configure logging
logging.basicConfig(
    level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s"
)

API_KEY = os.getenv("PINECONE_API_KEY","pcsk_239Y5A_739p25f8ZKU1s1cAXWbaokeN2eBkExxEsfi2QTWxy6Xa7YquJ2XqeqiMEsTXKKr")
INDEX_NAME = os.getenv("PINECONE_INDEX_NAME","quickstart-py")
MAX_LATENCY = float(os.getenv("MAX_QUERY_LATENCY_SEC", 2.0))  # in seconds

if not API_KEY or not INDEX_NAME:
    logging.error("PINECONE_API_KEY and PINECONE_INDEX_NAME must be set.")
    sys.exit(1)

try:
    pc = Pinecone(api_key=API_KEY)
    index = pc.Index(INDEX_NAME)

    query_vector = [0.1] * 1024  # use appropriate dimension
    start = time.time()
    result = index.query(vector=query_vector, top_k=5, include_values=False)
    latency = time.time() - start

    logging.info(f"Query latency: {latency:.4f} seconds")
    if latency > MAX_LATENCY:
        logging.warning(f"Latency exceeded threshold: {latency:.2f} > {MAX_LATENCY}")
        sys.exit(1)

    sys.exit(0)

except Exception as e:
    logging.error(f"Query failed: {e}")
    sys.exit(1)
  ```
![Screenshot from 2025-06-22 12-56-13](https://github.com/user-attachments/assets/bc1be05f-94e7-4745-94c9-0cfe3ac7f12e)

the overall output of all the monitors is :
![Screenshot from 2025-06-22 12-45-02](https://github.com/user-attachments/assets/a7023b06-d3eb-418b-9d89-738213082f5e)

### Conclusion:
All monitoring scripts are running smoothly and providing continuous insight into Pinecone's health and performance. No disruptions or failures were detected in the current cycle. The system is stable and under proactive observation.






