# Content-based Recommender using TF-IDF

This hands-on lab demonstrates the application of the Azure ML Computer Vision Package for image classification.

### Learning Objectives ###

The objectives of this lab are to:
- Understand the image classification workflow
- Learn how to format a dataset in order to ingest and perform augmentations
- Train a model using transfer learning based on ResNet18 and evaluate the classifier

### Data

In this lab, we will use the same sample classification dataset (resources/sample_data.zip) related to recyling dishes that was used in the previous lab.

| id | product_id | product_name | description | category_name |
| --- | --------- | ------------ | ----------- | ------------- |
| 306 | 802 | LL Fork | Stout design absorbs shock and offers more precise steering. | Components |
| 307 | 803 | ML Fork | Composite road fork with an aluminum steerer tube. | Components |
| 172 | 494 | Paint - Silver | | Part |



#### Cosmos DB

##### Ingestion

````python
def write_to_cosmos_col(uri, db_name, col_name, csv_name):
client = pymongo.MongoClient(uri)
db = client[db_name]
products_col = db[col_name]
products = pd.read_csv(csv_name)
for index, row in products.iterrows():
description = row['description']
if row['description'] == Nan:
description = ""
doc_product = {"id": row['id'], "product_id": row['product_id'], "product_name": row['product_name'], "description": description, "category_name": row['category_name']}
products_col.update({"id": row['id']}, doc_product, True)
`````
![CosmosDB](images\cosmosDB.PNG)

##### Read collections into a data frame

````python
def read_from_cosmos_col(uri, db_namem, col_name):
client = pymongo.MongoClient(uri)
db = client[db_name]
products_col = db[col_name]
df = pd.DataFrame(list(products_col.find()))
return df
`````

#### Recommender Service

![RestAPI](images\restAPI.PNG)

#### Dataset splitting

The _Azure Machine Learning Package for Computer Vision (AMLPCV)_ package offers several utility functions to split the dataset into a train and test set
