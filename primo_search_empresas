import pandas as pd
import googlemaps
import time

gmaps = googlemaps.Client(key='ALTERAR_PRIMO_KEY')

locations = [

    {'lat': -24.00653, 'lng': -46.43088},   # Guilhermina  
    {'lat': -24.01537, 'lng': -46.45296},   # Tupi
    {'lat': -24.03475, 'lng': -46.50911},   # Entre Tupi e Mirim
    {'lat': -24.01893, 'lng': -46.47230},   # Maracanã
    {'lat': -24.04253, 'lng': -46.52514},   # Vila Caiçara
    {'lat': -24.06202, 'lng': -46.55941},   # Ribeiropolis
    {'lat': -24.07095, 'lng': -46.58155}    # Florida 

]

dados = []

def primo_search(location):
    search_results = gmaps.places_nearby(location=location, radius=2000, keyword='academia')
    while True:
        for result in search_results['results']:
            place_id = result['place_id']
            place_details = gmaps.place(place_id=place_id)['result']

            nome = place_details.get('name', 'Não disponível')
            endereco = place_details.get('formatted_address', 'Não disponível')
            telefone = place_details.get('formatted_phone_number', 'Não disponível')
            site = place_details.get('website', 'Não disponível')

            dados.append([nome, endereco, telefone, site])

        if 'next_page_token' in search_results:
            time.sleep(2)
            search_results = gmaps.places_nearby(page_token=search_results['next_page_token'])
        else:
            break

for loc in locations:
    primo_search(loc)

df = pd.DataFrame(dados, columns=['Nome', 'Endereço', 'Telefone', 'Site'])
df.to_excel('primo.xlsx', index=False)
print("Dados salvos com sucesso em 'primo.xlsx'.")
