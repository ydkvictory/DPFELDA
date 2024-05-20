# DPFELDA
# Predicting lncRNA-disease associations based on a dual-path feature extraction network with multiple sources of information integration

Introduction

This is code of DPFELDA ("Predicting lncRNA–disease associations based on a dual-path feature extraction network with multiple sources of information integration")

Environmental Requirement

pytorch 1.13.0
torch_geometric 2.2.0
xlrd 1.2.0
numpy 1.22.4
scikit-learn 1.0.2


catalogues

1.Data preprocessing

Announcement
Please download the Raw data zip and extract it to the Raw data folder in the DPFELDA directory.
Data preprocessing1 Constructing data4 using Raw data. Raw data includes information from HMDDv 4.0,lnc2Cancer v3.0,lncRNAdisease 3.0,MeSH,miRbase,starBase databases.
Data preprocessing2 calculates the similarity network of diseases to lncRNAs using dataset 4 as an example.

Announcement
The default dataset for model training is dataset4. If you want to adjust the dataset, modify the" --dataset-path "，“--lncRNA-numbe”，“--disease-number”,"--miRNA-number" of param.py in Compensation feature extraction and Topological feature extraction

2.Compensation feature extraction
(1) code: Node Topology Compensation Feature Exploration Code
 	param.py Hyperparameter settings
    	Transformer.py The Transformer model framework
	loss.py Loss Functions
	utils.py Tool files e.g. data input
(2) data1,data2,data3,data4
	LD.csv Disease association information for lncRNA 
	MD.csv  Information on the association of miRNAs with diseases
	LM.csv  Information on lncRNA-miRNA interactions
	LD from lncRNADisease v2.0 ,lncRNADisease v3.0 ,lnc2Cancer v3.0
	LM from starbase v2.0
	MD from HMDD v 2.0,HMDD v 4.0

3.Topological feature extraction
(1）code 	 
	dataprocessing.py Data processing code to obtain the edges of the associated nodes in the similarity network
	GCNCAM.py Graph Convolution of Multi-View Structures with CBAM Node Topology Feature Extraction Networks
	param.py Parameter settings
(3) data1,data2,data3,data4
	LDA Disease association matrix for lncRNAs
	DSS,DGS,DCS Semantic similarity matrix for diseases, Gaussian kernel similarity matrix for diseases, cosine similarity matrix for diseases
	LFS,LGS,LCS Functional similarity of lncRNA,  GIP similarity, cosine similarity matrices
4.Results of the experiment The code implementation of the final binary classification task includes the characteristics of the disease and lncRNA for which the final classification is performed, as well as the classification model.

How to train a model ?

Topological features of training nodes

run representaionlearning.py

Compensatory features for training nodes

run main.py

View Category Results
To visually illustrate the classification impact of DPFELDA trained features, we stored the trained node features in the Classified feature folder and executed five-fold cross-validation on each of the four datasets using result.ipynb.
Please execute the result.ipynb file

