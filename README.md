# CryptoClustering

## Prepare the Data
1) Use the ```StandardScaler()``` module from ```scikit-learn``` to normalize the data from the CSV file.
2) Create a DataFrame with the scaled data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.
    - The first five rows of the scaled DataFrame should appear as follows:
    <div style="text-align:center;" width=80%>
        <img src='images/scaled_df.png' width=70% align='middle'>
    </div>


## Find the Best Value for k Using the Original Scaled DataFrame
Use the elbow method to find the best value for ```k``` by completing the following steps:
1) Create a list with the number of k values from 1 to 11.
2) Create an empty list to store the inertia values.
3) Create a ```for``` loop to compute the inertia with each possible value of ```k```.
4) Create a dictionary with the data to plot the elbow curve.
5) Plot a line chart with all the inertia values computed with the different values of ```k``` to visually identify the optimal value for ```k```.
6) Answer the following question in your notebook: What is the best value for k?
    ```
    After K=4 the rate of decrease in inertia slows down noticeably.
    Based on this observation, the elbow point is at K=4. Therefore, the optimal number of clusters, 
    K, is likely to be 4
    ```

## Cluster Cryptocurrencies with K-Means Using the Original Scaled Data
Use the following steps to cluster the cryptocurrencies for the best value for ```k``` on the original scaled data:
1) Initialize the K-means model with the best value for ```k```.
2) Create an instance of K-means, define the number of clusters based on the best value of ```k```, and then fit the model using the original scaled DataFrame.
3) Predict the clusters to group the cryptocurrencies using the original scaled DataFrame.
4) Create a copy of the original data and add a new column with the predicted clusters.
5) Create a scatterplot using pandas’ ```plot``` as follows:
    - Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d".

## Optimize Clusters with Principal Component Analysis
1) Using the original scaled DataFrame, perform a PCA and reduce the features to three principal components.
2) Retrieve the explained variance to determine how much information can be attributed to each principal component and then answer the following question in your notebook:
    - What is the total explained variance of the three principal components?
        ```
        The total explained_variance_ratio_ of the three principal components is approximately 0.895 (or 89.5%). This means that the 3 principal components together account for 89.5% of the variance in the dataset, indicating that these components capture a significant portion of the data's variability
        ```
3) Create a new DataFrame with the PCA data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.
    - The first five rows of the PCA DataFrame should appear as follows:
    <div style="text-align:center;" width=80%>
        <img src='images/PCA_top5.png' width=30% align='middle'>
    </div>


## Find the Best Value for k Using the PCA Data
Use the elbow method on the PCA data to find the best value for ```k``` using the following steps:
1) Create a list with the number of k-values from 1 to 11.
2) Create an empty list to store the inertia values.
3) Create a ```for``` loop to compute the inertia with each possible value of ```k```.
4) Create a dictionary with the data to plot the elbow curve.
5) Plot a line chart with all the inertia values computed with the different values of ```k``` to visually identify the optimal value for ```k```.
6) Answer the following questions in your notebook:
    - What is the best value for ```k``` when using the PCA data?
        ```
        After ```K=4``` the rate of decrease in inertia slows down noticeably.
        Based on this observation, the elbow point is at ```K=4```. Therefore, the best value of K is 4.
        ```
    - Does it differ from the best k-value found using the original data?
        ```
        -- The optimal elbow point using a scaled model analysis was found to be 4. 
        -- The optimal elbow point using a Principal Component Analysis is found to be 4.
        Both analysis methods bring us to the came result value for K=4
        ```
## Cluster Cryptocurrencies with K-Means Using the PCA Data
Use the following steps to cluster the cryptocurrencies for the best value for ```k``` on the PCA data:
1) Initialize the K-means model with the best value for ```k```.
2) Create an instance of K-means, define the number of clusters based on the best value of ```k```, and then fit the model using the PCA data.
3) Predict the clusters to group the cryptocurrencies using the PCA data.
4) Create a copy of the DataFrame with the PCA data and add a new column to store the predicted clusters.
5) Create a scatter plot using pandas’ ```plot``` as follows:
    - Set the x-axis as "PC1" and the y-axis as "PC2".
6) Answer the following question:
    What is the impact of using fewer features to cluster the data using K-Means?
    ```
    The second scatter plot shows a more defined ans simplified cluster 

    The impact of using fewer features to cluster data using K-Means can be significant and can manifest in several ways:
        1. Simplification of the Model
        Pros: Reducing the number of features simplifies the model, making it easier to interpret and understand. It also reduces the computational complexity and can speed up the clustering process.
        Cons: Oversimplification can lead to a loss of important information, potentially reducing the quality and accuracy of the clustering.
        2. Dimensionality
        Pros: In high-dimensional spaces, the distance between points becomes less meaningful. Reducing the number of features can mitigate this issue, leading to more meaningful clusters.
        Cons: If the reduction in features removes critical information, the clusters may not accurately represent the underlying data structure.
        3. Improved Cluster Separation
        Pros: Using relevant features can improve the separation between clusters, making the clusters more distinct and easier to identify.
        Cons: If important features are omitted, clusters may become less distinct and more overlapping, leading to poorer clustering performance.
        4. Noise Reduction
        Pros: Reducing the number of features can help eliminate noise, which can improve clustering performance. Irrelevant or redundant features can confuse the clustering algorithm.
        Cons: If noise is reduced too much, meaningful variability in the data may also be lost.
        5. Overfitting and Generalization
        Pros: Fewer features can help prevent overfitting, where the model becomes too tailored to the training data and performs poorly on new, unseen data. A simpler model with fewer features is likely to generalize better.
        Cons: If important features are discarded, the model may underfit, failing to capture the underlying patterns in the data.
        
        Practical Considerations
        Feature Selection: Carefully selecting the most relevant features (using techniques like PCA) can help retain the most important information while reducing dimensionality.
        Domain Knowledge: Leveraging domain knowledge to select features can be very beneficial. Experts in the field can often identify which features are likely to be most relevant for clustering.

    ```
## Determine the Weights of Each Feature on Each Principal Component
1) Create a DataFrame that shows the weights of each feature (column) for each principal component by using the columns from the original scaled DataFrame as the index.
2) Which features have the strongest positive or negative influence on each component?
    ```
    Larger absolute values indicate a stronger contribution of the feature to that principal component.
    - PCA1: This component is influenced most by 
        - Positively: price_change_percentage_200d and price_change_percentage_1y  
        - Negatively: price_change_percentage_24h 
    - PCA2: This component is influenced most by 
        - Positively: price_change_percentage_30d and price_change_percentage_14d 
        - Negatively: price_change_percentage_1y 
    - PCA3: This component is influenced most by 
        - Positively: price_change_percentage_7d
        - Negatively: price_change_percentage_60d
    ```