# aml-delta

This repo will show a basic Demo of how to use Delta file format from AML Compute.

![image](https://user-images.githubusercontent.com/5873303/121588011-66013580-ca03-11eb-8c87-c1bd0535cacf.png)

## 1) Use Databricks to import the notebook: Databricks_Delta_Load.ipynb

The databricks  notebook will show a demo of how to load sample safe_driver data and save it as a spark dataframe in delta file format. 
Than we will register/create a datastore and upload the delta files and than create a file dataset referencing that datastore .

## 2) Verify that the Datastore and Dataset have been registered in AML, you should see a list of parquet files and the json transaction log file for delta:

![image](https://user-images.githubusercontent.com/5873303/121588340-cbedbd00-ca03-11eb-9e0c-74d74d36b932.png)

## 2) Use AML Notebook to import the notebook: Delta_DBX_Read_Demo.ipynb

This notebook will show how to install the detla table and than use AML Datastore and Dataset to download the delta table 
and convert the delta table to pandas frames:



```
from deltalake import DeltaTable
dt = DeltaTable("/mnt/batch/tasks/shared/LS_root/mounts/clusters/deltademocpu/code/delta_driver/")

table= dt.to_pyarrow_table()
# Convert back to pandas
df_pandas = table.to_pandas()

```
