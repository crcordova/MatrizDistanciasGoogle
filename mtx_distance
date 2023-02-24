import googlemaps
import pandas as pd

# Inserta tu clave de API de Google Maps aquí
gmaps = googlemaps.Client(key='TU_CLAVE_API')

# Define las coordenadas de las ciudades
coords = {
    'Pichilemu': '-34.3960793,-72.0233316',
    'Santa Cruz': '-34.6324213,-71.3592116',
    'Boyeruca': '-34.6889976,-72.0545467',
    'Paredones': '-34.6519651,-71.9001448',
    'Palmilla': '-34.634583,-71.4971069',
    'Rengo': '-34.409114,-70.8719663',
    'San Fernando': '-34.5805483,-70.9903499'
}

# Calcula las distancias entre las ciudades
distances = {}
for i, (city1, c1) in enumerate(coords.items()):
    for j, (city2, c2) in enumerate(coords.items()):
        if j > i:
            result = gmaps.distance_matrix(c1, c2, mode='driving')
            distance = result['rows'][0]['elements'][0]['distance']['value']
            distances[(city1, city2)] = distance
            distances[(city2, city1)] = distance

# Crea un DataFrame de pandas con las distancias
df = pd.DataFrame(distances.values(), index=pd.MultiIndex.from_tuples(distances.keys()))
df = df.unstack(level=-1).fillna(0)
