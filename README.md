# Investigating-Netflix-Movies
# Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

# import the netflix csv file
netflix_df = pd.read_csv('netflix_data.csv', index_col = 0)
print(netflix_df[0:5])

# Subset netflix_df with only rows where type is a movie and store in netflix_subset
netflix_subset = netflix_df.loc[netflix_df['type'] == 'Movie']
print(netflix_subset)

# Subset netflix_subset to keep only the columns title, country, genre, release_year, and duration. Store in netflix_movies
netflix_movies = netflix_subset.loc[:, ['title', 'country', 'genre', 'release_year', 'duration']]
print(netflix_movies)

# Filter netflix_movies for movie duration less than 60 minutes. Store in short_movies
short_movies = netflix_movies.loc[netflix_movies['duration'] <  60]
print(short_movies[0:20])

# Initialize an empty list called colors to store different color values
colors = []

# Use a for loop to iterate through netflix_movies rows and append colors to list based on genres
for index, row in netflix_movies.iterrows():
    if row['genre'] == 'Children':
        colors.append('Yellow')
    elif row['genre'] == 'Documentaries':
        colors.append('Red')
    elif row['genre'] == 'Stand-up':
        colors.append('Green') 
    else:
        colors.append('Purple')
# print(colors)

# Initialize a figure object called fig
fig = plt.figure(figsize=(12, 8))

# Plotting the scatter plot
plt.scatter(netflix_movies['release_year'], netflix_movies['duration'], c=colors)

# Adding labels to plots
plt.xlabel('Release year')
plt.ylabel('Duration (min)')
plt.title('Movie Duration by Year of Release')

# Display the plot
plt.show()

# Are the movies getting shorter?
answer =  'No'
