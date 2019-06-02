# metabolite2019 notes for all analysis procedures of metabolite project

# import all packages
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  import seaborn as sns
  import math
  %matplotlib inline
  
# sheetname用于指定sheet列表
# use comapre_1 datasets
# compare_1 datasets is preprocessing in excell with the standard:p-value<0.05&fold_change<0.8or>1.2
# Col_CvsBzr1_D_C is first sheet
sheetnames = [0,1,2,3,4,5,6,7]

# 創建一个空列表把每個sheet的數據放入列表中
sheet_list = []
for sheet in sheetnames:
    sheet_value = pd.read_excel("Compare_1_standardize.xlsx",sheetname=sheet)
    sheet_list.append(sheet_value)
    
# check sheet[0] info to confirm above lines
sheet_list[0]

# 提取目標數據 (loc是根据dataframe的具体标签选取列，而iloc是根据标签所在的位置，从0开始计数) https://blog.csdn.net/chenKFKevin/article/details/62049060
list_temp = []
for sheet in sheet_list:
    sheet = sheet.iloc[:,[0,-1,-2,-3,-4,-5,-6,-7,-8,-9,-10,-11,-12]].set_index('Metabolites')
    list_temp.append(sheet)
    
list_temp[1]

# 檢查9個列表中是否有重名的
# 提取index的名字
list_temp2 = []
for sheet in list_temp:
    sheet_index_list = np.array(sheet.index.values).tolist()
    list_temp2.append(sheet_index_list)
    
list_temp2[0]

## Col_M 和 Col_S的比较


Col_M_S = list(set(list_temp2[0]) & set(list_temp2[1]))

len(Col_M_S)

join_col_sheet = []
for sheet_id in range(0,2):
    join_col_sheet.append(list_temp[sheet_id].loc[Col_M_S,:])
    
join_col_sheet[1].index.duplicated()

list_d_index = []
for i in range(0,2):
    d_index = join_col_sheet[i].index[join_col_sheet[i].index.duplicated()]
    list_d_index.append(d_index)
    
stancol_0 = list(set(list_temp2[0]) - set(list_d_index[0]))
stancol_1 = list(set(list_temp2[1]) - set(list_d_index[1]))

Col_M_S = list(set(stancol_0) & set(stancol_1))

join_Col_M_S = []
list0_ovl = list_temp[0].loc[Col_M_S,:]
join_Col_M_S.append(list0_ovl)
list1_ovl = list_temp[1].loc[Col_M_S,:]
join_Col_M_S.append(list1_ovl)

# 取数据+合并
# join_Col_M_S = []
# for sheet_id in range(0,2):
# join_Col_M_S.append(list_temp[sheet_id].loc[join_Col_M_S,:])
# join_Col_M_S = pd.concat(join_Col_M_S,axis=1,join='inner')

join_Col_M_S = pd.concat(join_Col_M_S,axis=1,join='inner')

join_Col_M_S.to_excel("compare1_Col_M_S_sameMetaName.xls")

# extract overlapping partion of three mutants (all union)
all_c = list(set(list_temp2[0]) | set(list_temp2[1]) | set(list_temp2[2]))

all_c_e = pd.Series(all_c)

all_c_e.to_csv("all_c_allunion.csv")

