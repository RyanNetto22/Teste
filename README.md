import pandas as pd

# Carregar o arquivo CSVfile_path = 'billboard200.csv'data = pd.read_csv(file_path)

# Corrigir os tipos de dados na coluna 'Weeks in Charts'data['Weeks in Charts'] = pd.to_numeric(data['Weeks in Charts'], errors='coerce')

# Saída 1: top100faixas.csv
# Obter as 100 melhores músicas por semanas nas paradastop100_songs = data.sort_values(by='Weeks in Charts', ascending=False).head(100)top100_songs = top100_songs[['Rank', 'Song', 'Artist', 'Peak Position', 'Weeks in Charts']]top100_songs.to_csv('top100faixas.csv', index=False)

# Saída 2: top10artistas_p.csv
# Filtrar artistas que começam com 'P'artists_p = data[data['Artist'].str.startswith('P', na=False)]

# Calcular pontos para cada artistaartist_points = artists_p.groupby('Artist')['Weeks in Charts'].sum().reset_index()artist_points.columns = ['Artist', 'Pontos']

# Obter os 10 melhores artistas por pontostop10_artists_p = artist_points.sort_values(by='Pontos', ascending=False).head(10).reset_index(drop=True)top10_artists_p['Rank'] = top10_artists_p.index + 1top10_artists_p = top10_artists_p[['Rank', 'Artist', 'Pontos']]top10_artists_p.to_csv('top10artistas_p.csv', index=False)

print("Saídas geradas com sucesso: 'top100faixas.csv' e 'top10artistas_p.csv'")
