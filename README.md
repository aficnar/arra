# ARRA

This is a project I'm working on in collaboration with the team from the Center for Technology and Behavioral Health at the Department of Biomedical Data Science at Dartmouth College. 

Our goal is to apply machine learning (including social network analysis, natural language processing and deep learning) to Instagram data to identify risks of substance abuse. 

As part of the project, we are developing an app that will be shown to Instagram and Facebook users, in which they fill out a short survey on substance use in the last 12 months. We will use the results of the survey, together with all the data Instagram offers (tags, likes, timestamps, picture content, etc.) to develop a predictive model.

These are some of the things I have worked on:

* **main_analysis_redacted.ipynb** - The redacted version of the main analysis notebook (work in progress), which:
  * connects to a SQL database on Heroku, fetches the relevant data, and cleans it up
  * constructs the weighted tag network for each user
  * generates potentially predictive features to be used in classification models
  * applies several classifiers
    
* **tag_model.ipynb** - A dynamical social network model that I developed that aims to capture social shifts by analyzing the Instagram data. 
  * Based on the tag information from Instagram pictures, we want to be able to generate a graph centered around some user, and design features that will be predictive of social shifts in his / her life.
  * We propose a model to generate a weighted graph with edges that are intrinsically time-dependent, in such a way to easily capture intuitive information that the tags made at some later time are more relevant than the tags made at some earlier time.
  * In order to be able to study this model, we also generate a realistic social network with a nontrivial underlying social structure that we can easily change.
  
* **visualize_network.ipynb** - In this notebook we visualize the network of an Instagram user that will be shown to users that complete the ARRA survey.
  * The code uses the profile pictures of everyone tagged in the pics of some user, and makes them circular with a nice frame (using the PIL package).
  * The tag network is then visualized in such a way that the user will be one large central node, and all the people tagged in its photos will be nodes connected to it, evenly distributed around it, with edge lengths inversely proportional to the the number of tags.
  * This information is then used to find the optimal positions of all the nodes in a given figure, draw the edges and export the figure with a transparent background.
  
* **optimal_node_positions.ipynb** - This notebook uses the code for finding the optimal node positions in a simple Instagram network visualization of `visualize_network.ipynb`, with the focus on making the code portable.
  * This is done by handling cases when there are very few or very many tags, including the prevention of node overlap and speed up of the code. 
  * The code then outputs optimal node positions (in pixels), which is then used in the HTML's canvas in the ARRA app, as it is faster and more practical to handle resizing and placing images that way.
  
* **bkg_graph.ipynb** - In this notebook we create pretty, random-looking large graphs that will be used as a background in the ARRA app. This is done by using large Barabasi-Albert random graphs, extracting the ego subgraph of the most popular node and tweaking the spring layout settings in `networkX`.
