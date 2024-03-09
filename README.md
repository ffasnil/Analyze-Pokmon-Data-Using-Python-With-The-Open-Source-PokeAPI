# Extracting Pokémon API using Python

An Application Programming Interface, commonly referred to as API, acts as a intermediary connecting and facilitating communication between two servers. Its adaptable functions include serving as middleware for extracting Big Data from external sources, enabling real-time data updates, operating in a cloud-based environment, and more.

an API operates by having the client send a "request" to the server to fetch data, and upon receiving a response from the server, it sends the corresponding "response" back to the client.


![Add a subheading](https://github.com/ffasnil/Analyze-Pok-mon-Data-Using-Python-With-The-Open-Source-Pok-API/assets/89661712/b57dd1c6-e620-4921-b5aa-f2d6aa953320)


## HTTP Status Code
After the client sends the response back, it's possible to check the status code to determine whether the connection was successful or not. For instance, a status code like 404, a frequently encountered numbers, indicates an error depending on the system. ***For more on HTTP Status Codes, visit :*** [https://en.wikipedia.org/wiki/List_of_HTTP_status_codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

In Addition, in Python you can perform this check in Python using the provided syntax.
``` Python
requests.get("...URL/API endpoint...").status_code
```

## Project Resources
- Open Access PokéAPI : 
[https://pokeapi.co/](https://pokeapi.co/)
- PokéAPI Documentation : [https://pokeapi.co/docs/v2#pokemon-species](https://pokeapi.co/docs/v2#pokemon-species)
- Pokédex : [https://www.pokemon.com/us/pokedex](https://www.pokemon.com/us/pokedex)

## About This Project
An essential starting point for any project involves importing the required libraries to facilitate its functionality.
``` Python
import requests
import time
import pandas as pd
```
Next step involves extracting data through an APIs. This process will include extracting specific columns from two distinct endpoints, namely Pokémon and Pokémon Species.

- Pokémon url: ["https://pokeapi.co/api/v2/pokemon/"]("https://pokeapi.co/api/v2/pokemon/")
- Pokémon Species url: ["https://pokeapi.co/api/v2/pokemon-species/"]("https://pokeapi.co/api/v2/pokemon-species/")

The number of Pokémon will be extracted displaying only the initial 40 characters (from #0001 to #0040). You can find this information in the [Pokédex](https://www.pokemon.com/us/pokedex)

<br>

### Data Cleansing

In the Pokémon DataFrame section, we will clean and extract the <ins>Pokémon Type</ins> from the 'types' column, which has a format like _**[{'slot': 1, 'type': {'name': 'grass', 'url': ...]**_. This structure is a dictionary with an outer key-value pair. For example, the goal is to filter out only the 'grass' type.

``` Python
#Extract values associated with the key 'name' in the 'types' column
df_detail['types'] = df_detail['types'].apply(lambda x: [item['type']['name'] for item in x])

df_detail.head()
```
Moving on to the Pokémon Species DataFrame, cleaning and extraction will be conducted tasks on the 'color' and 'habitat' columns. This process mirrors the cleaning procedure used in the previous DataFrame. However, in this case, the structure is a simple dictionary without additional nesting.
``` Python
df_species['color'] = df_species['color'].astype(str).str.extract(r"'name': '(.*?)',")
df_species['habitat'] = df_species['habitat'].astype(str).str.extract(r"'name': '(.*?)',")

df_species.head()
```
