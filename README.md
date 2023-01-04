Note: Azure ML has an updated method of consuming Delta files: https://learn.microsoft.com/en-us/azure/databricks/mlflow/tracking-ex-delta

# This repo will show a basic Demo of how to use Delta file format from AML 

With the new announcement from Databricks of relasing DeltaLake for standalone compute, we can now easily integrate the AML CI/Cluster with Delta file format generated/saved from Spark 

https://delta.io/news/delta-lake-1-0-0-released/

![image](https://user-images.githubusercontent.com/5873303/121592654-f55d1780-ca08-11eb-9b85-4dbe1da86433.png)

![image](https://user-images.githubusercontent.com/5873303/121588011-66013580-ca03-11eb-8c87-c1bd0535cacf.png)

## 1) Use Databricks to import the notebook: [Databricks_Delta_Load.ipynb](Databricks_Delta_Load.ipynb)

The databricks  notebook will show a demo of how to load sample safe_driver data and save it as a spark dataframe in delta file format. 
Than we will register/create a datastore and upload the delta files and than create a file dataset referencing that datastore .

## 2) Verify that the Datastore and Dataset have been registered in AML, you should see a list of parquet files and the json transaction log file for delta:

![image](https://user-images.githubusercontent.com/5873303/121588340-cbedbd00-ca03-11eb-9e0c-74d74d36b932.png)

## 2) Use AML Notebook to import the notebook: [Delta_AML_Read_Demo.ipynb](Delta_AML_Read_Demo.ipynb) and run it on a AML compute instance 

This notebook will show how to install the detla table and than use AML Datastore and Dataset to download the delta table 
and convert the delta table to pandas frames:



```
from deltalake import DeltaTable
dt = DeltaTable("/mnt/batch/tasks/shared/LS_root/mounts/clusters/deltademocpu/code/delta_driver/")

table= dt.to_pyarrow_table()
# Convert back to pandas
df_pandas = table.to_pandas()

```
