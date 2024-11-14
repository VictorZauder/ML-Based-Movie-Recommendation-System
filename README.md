# ML-Based-Movie-Recommendation-System
We used the metadata "The Movies Dataset" from Kaggle, which contained over 45,000 
movies with 25 million ratings from over 270,000 users. The dataset was last updated in July 
2017 by the user Rounak Banik. From this data collection, the program extracted information 
from the movies_metadata file and the ratings file (Banik, Rounak, 2017).  
These two datasets were preprocessed separately before being implemented in the 
recommender system. As the ratings data was extensive, it was loaded in chunks, capturing only 
the first 1 million ratings. This subset was then converted into a user-item matrix, grouping users 
by identification, and retaining movie ID and rating data. Each entry in the user-item matrix 
represents a user's rating for a specific movie, with missing values indicating movies not watched 
filled with 0s.  
Only the title, IDs, and genre features were loaded and preprocessed for the movie data. 
To clean the movie data, we dropped duplicates with the same ID followed by the same title. We 
also addressed issues in leading and trailing whitespaces and having non-integer values in the ID 
columns. Lastly, both datasets were aligned to include only identifiable movies with ratings.   
The program has user interaction to prompt them to enter the movie title and, if found, 
enter the rating for said movie to generate a new user matrix. This matrix and the user-item 
matrix are then combined to calculate the cosine similarity for the shared movies between the 
previous and new users. The equation below illustrates the calculation between two user vectors, 
a and b, where a value closer to 1 indicates the two items as highly similar (Mana & Sasipraba, 
2021; Xia et al., 2015).  

c𝑜𝑠𝑖𝑛𝑒	𝑠𝑖𝑚𝑖𝑙𝑎𝑟𝑖𝑡𝑦	(𝑎,𝑏) =	(𝑎 ∙𝑏)
 |𝑎| ∙ ||𝑏||
 
 Following the calculation of cosine similarity scores, the program proceeds to identify 
similar users and their movie ratings. It aggregates the ratings from similar users with weighted 
ratings using their corresponding cosine similarity values and compiles a list of movies with 
preferences given to the most similar users. However, before sharing these recommendations 
with the new user, we applied content-based filtering to consider the genres. 
In content-based filtering, each recommended movie's weighted rating was adjusted 
based on the average rating for the movie genre of the new user's input movies. If a genre's 
average rating fell below three, the recommendation's weighted rating was penalized, reducing 
its priority. Conversely, if the average rating for a genre exceeded three, the recommendation's 
weighted rating was boosted, increasing its priority in the recommendation list. 
This adjustment process was achieved by iterating through each recommended movie and 
accessing its genre information. For each genre associated with the movie, the program retrieved 
the average rating for that genre from the new user's input movies. The recommendation's 
weighted rating was adjusted accordingly depending on whether the average rating was above or 
5 
below three. Finally, the list of recommended movies was sorted based on their adjusted 
weighted ratings to generate the final recommendation list for the new user. 
This recommender system uses collaborative and content-based filtering to personalize 
movie recommendations for the user. The program emphasizes the need to find similar users 
who have watched and rated similarly to how the new user rated their movie choice. The 
program further investigates the movies these similar users watch to identify those most akin to 
the new user's genre preferences. With this approach, the system highlights what others liked and 
structures the recommendations to weigh the movies similar in content higher than the other 
recommendations.  
The Python frameworks used were Pandas, NumPy, and Scikit-Learn to execute the 
program. Pandas and NumPy were primarily used to handle the data analysis and manipulation 
of the ratings and movie data frames and to sort the recommendations(Harris et al., 2020; The 
pandas development team, 2024). In contrast, sci-kit-learn included the math function cosine 
similarity used to compute the similarity scores amongst the users. We also used the library 
Fuzzywuzzy for user interaction to find approximate string matches in title input to enhance the 
user experience without putting the exact title.  
