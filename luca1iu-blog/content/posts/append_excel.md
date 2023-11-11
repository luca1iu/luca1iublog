+++
title = 'How to merge multiple excel files using python'
date = 2023-11-11T21:34:44+08:00
+++


When you have multiple excel files with the same column and you want to merge multiple excel files into one excel file…

## Python method
1. import packages
```python
import pandas as pd
import os
```

2. Put all the excel to be merged into a separate folder

3. define a function

```python
def append(path): 
    frames = [] 
    for root, dirs, files in os.walk(path):
        for file in files:
            file_with_path = os.path.join(root, file)
            df = pd.read_excel(file_with_path, engine='openpyxl')
            frames.append(df)
    df = pd.concat(frames, axis=0)
    return df

df = append(path)
df.to_excel("merged_excel.xlsx")
#path：The folder where all the excel files need to be merged
```

tips:
It is also possible to use directly without defining the function.

```python
frames = [] 
for root, dirs, files in os.walk(path):
    for file in files:
        file_with_path = os.path.join(root, file) 
        df = pd.read_excel(file_with_path, engine='openpyxl')
        frames.append(df)
df = pd.concat(frames, axis=0)
df.to_excel("merged_excel.xlsx")
```

### notes
1. `root` in the above code is the path to the folder that contains all the excel files to be merged
2. `files` is a list, containing the names of all the excel files in the folder
3. `os.path.join(root, file)` is to merge the paths and file names of the folders, so that pd.read_excel() can read the excel files later


## some special cases
#### If the excel file name includes the date and needs to be written to the final summary excel


```python
def append(path): 
    frames = [] 
    for root, dirs, files in os.walk(path):
        for file in files:
            file_with_path = os.path.join(root, file) 
            df = pd.read_excel(file_with_path, engine='openpyxl')
            
            df["date"] = pd.to_datetime(file.strip('.xls'))
            #extract date string from the filename
            frames.append(df)
    df = pd.concat(frames, axis=0)
    return df
```


#### If you need to merge multiple excel into one excel, and the sheet is named as the name of each excel name

```python
def combine(path):
    with pd.ExcelWriter("merged_excel.xlsx") as writer:
        for root, dirs, files in os.walk(path):
            for file in files:
                filename = os.path.join(root, file)
                df = pd.read_excel(filename, engine='openpyxl')
                df.to_excel(writer, sheet_name=file.strip('.xls')) 
                #Delete the file name suffix, 
                #sometimes it could be .csv/.xlsx
        return df
```

