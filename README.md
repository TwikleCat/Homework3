# Homework3
Data collection and preparation
'''
import numpy as np # linear algebra
import pandas as pd# data processing, CSV file I/O (e.g. pd.read_csv)
import matplotlib.pyplot as plt
import seaborn as sns
# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
        '''

'''
df = pd.read_csv("/kaggle/input/e-commerce-dataset/realistic_e_commerce_sales_data.csv")
df.head(3)
'''
