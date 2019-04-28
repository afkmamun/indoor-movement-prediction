# Indoor Movement Prediction

Prediction of user movements from data aggregated via Radio Signal Strength(RSS) measurement system.

## Dataset Description

### Summary
This dataset represents a real-life benchmark in the area of Ambient Assisted Living applications. The binary classification task consists in predicting the pattern of user movements in real-world office environments from time-series generated by a Wireless Sensor Network (WSN). 

Input data contains temporal streams of radio signal strength (RSS) measured between the nodes of a WSN, comprising 5 sensors: 4 anchors deployed in the environment and 1 mote worn by the user. Data has been collected during user movements at the frequency of 8 Hz (8 samples per second). In the provided dataset, the RSS signals have been rescaled to the interval [-1,1], singly on the set of traces collected from each anchor.

Target data consists in a class label indicating whether the user's trajectory will lead to a change in the spatial context (i.e. a room change) or not. In particular, the target class +1 is associated to the location changing movements, while the target class -1 is associated to the location preserving movements.

The measurement campaign involved a number of 3 different environmental settings, each of which comprises 2 rooms (containing typical office furniture) separated by a corridor. A sketch of the common setup considered is provided by the Figure in file **MovementAAL.jpg**.

Each file in the provided dataset contains data pertaining to one temporal sequence of input RSS data (1 user trajectory for each file). The dataset contains 314 sequences, for a total number of 13197 steps. The dataset can be found [here](https://archive.ics.uci.edu/ml/datasets/Indoor+User+Movement+Prediction+from+RSS+data). For more information on the dataset, visit this [link](http://wnlab.isti.cnr.it/paolo/index.php/dataset/6rooms). 

### Attribute Information
Data is provided in comma separated value (csv) format. 

* **Input:** Input RSS streams are provided in files named **MovementAAL_RSS_SEQID.csv**. Here, *IDSEQ* is the progressive numeric *sequence ID*. In each file, each row corresponds to a time step measurement (in temporal order) and contains the following information:
*RSS_anchor1, RSS_anchor2, RSS_anchor3, RSS_anchor4*.

* **Target:** Target data is provided in the file **MovementAAL_target.csv**. Here, each row in this file contains:
*sequence_ID*, *class_label*.

* **Dataset Grouping:** Data is grouped in 3 sets. File **MovementAAL_DatasetGroup.csv**, provides information about such data grouping. Each row in this file contains: 
*sequence_ID*, *dataset_ID*.

* **Path Grouping:** Users' movements are divided in 6 prototypical paths. File **MovementAAL_Paths.csv** provides information about data grouping based on path type. Here, each row in this file contains:
*sequence_ID*, *path_ID*.

## Project Organization 

### Folder Structure
```
.
├── data/
    ├── MovementAAL/
        ├── dataset/
            ├── MovementAAL_RSS_1.csv
            ├── MovementAAL_RSS_2.csv
            ...........
        ├── groups/
            ├── MovementAAL_DatsetGroup.csv
            ├── MovementAAL_Paths.csv
            
    ├── notebooks/
        ├── Indoor User Movement Prediction from RSS Data Set .ipynb
 
    ├── processed_data/
        ├── indoor_movement.csv
        ├── indoor_movement_red.csv
        
        
    ├── LICENSE
    ├── requirements.txt
         
 ```

### Workflow
```
Dataset
      - Preprocessing
                - Concatenating Target Column with the Inputs
                - Adding Ids to Each Row
                - Adding Groups to Each Row
                - Adding Time based on 8Hz Sampling Frequency
                    
      - Exploratory Data Analysis
                - Time Series Visualization
                - Histogram Plots
                - Dimensionality Reduction 
                         - PCA (Principle Component Analysis)
                         - UMAP (Uniform Manifold Approximation and Projection)
                                                         
      - Movement Classification & Prediction
               - Baseline Model
                        - Classification
                                - 75-25% Train-Test Split
                                - Classification via Random Forest
                                - Training
                        - Evaluation
                                - Validation
                        
               - Ensemble Method for Improving Prediction
                        - Feature Extraction
                                - Tsfresh feature extraction
                                - Important feature selection
                        - Classification 
                                - 75-25% Train-Test Split
                                - Classifier Ensembling Via Soft Voting (Decision Tree, KNN, Gradient Boosting,
                                                                         Random Forest, Adaboost) 
                                - 10-fold Stratified Cross Validation
                                - Training
                         - Evaluation
                                - Validation 
                                - UMAP of the Extracted Features
                                - Decision Boundary Plotting
 ```
