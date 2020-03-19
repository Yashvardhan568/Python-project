# Python-project
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
!pip install pywaffle
from pywaffle import Waffle
df1= pd.read_csv(r'C:\Users\HP\Desktop\coronavirus-cases-in-india\Covid cases in India.csv')
df_india = df1.copy()
df1.drop(['S. No.'],axis=1,inplace=True)
df1['Total cases'] = df1['Total Confirmed cases (Indian National)'] + df['Total Confirmed cases ( Foreign National )']
df1['Active cases'] = df1['Total cases'] - (df1['Recovered'] + df1['Deaths'])
print(f'Total number of Confirmed COVID 2019 cases across India:', df1['Total cases'].sum())
print(f'Total number of Active COVID 2019 cases across India:', df1['Active cases'].sum())
print(f'Total number of Recovered COVID 2019 cases across India:', df1['Recovered'].sum())
print(f'Total number of Deaths due to COVID 2019  across India:', df1['Deaths'].sum())
print(f'Total number of States/UTs affected:', len(df1['Name of State / UT']))
#https://www.kaggle.com/nxrprime/styling-data-frames-covid-19-vs-conferences
def highlight_max(s):
    is_max = s == s.max()
    return ['background-color: pink' if v else '' for v in is_max]
    
#df.style.apply(highlight_max,subset=['Total Confirmed cases (Indian National)', 'Total Confirmed cases ( Foreign National )'])
df1.style.apply(highlight_max,subset=['Recovered', 'Deaths','Total cases','Active cases'])

df_condensed = pd.DataFrame([df1['Active cases'].sum(),df1['Recovered'].sum(),df1['Deaths'].sum()],columns=['Cases'])
df_condensed.index=['Active cases','Recovered','Death']
df_condensed


fig = plt.figure(
    FigureClass=Waffle, 
    rows=5,
    values=df_condensed['Cases'],
    labels=list(df_condensed.index),
    figsize=(10, 3),
    legend={'loc': 'upper left', 'bbox_to_anchor': (1.1, 1)}
)

df_full = pd.merge(India_coord,df1,on='Name of State / UT')
f, ax = plt.subplots(figsize=(12, 8))
data = df_full[['Name of State / UT','Total cases','Recovered','Deaths']]
data.sort_values('Total cases',ascending=False,inplace=True)
sns.set_color_codes("pastel")
sns.barplot(x="Total cases", y="Name of State / UT", data=data,
            label="Total", color="r")

sns.set_color_codes("muted")
sns.barplot(x="Recovered", y="Name of State / UT", data=data,
            label="Recovered", color="g")


# Add a legend and informative axis label
ax.legend(ncol=2, loc="lower right", frameon=True)
ax.set(xlim=(0, 35), ylabel="",
       xlabel="Cases")
sns.despine(left=True, bottom=True)

df2= pd.read_excel(r'C:\Users\HP\Desktop\coronavirus-cases-in-india\Covid-19_italy_province.xlsx')
df_italy = df2.copy()
df_italy
 
corr = df_italy.corr()
ax = sns.heatmap(
    corr, 
    vmin=-1, vmax=1, center=0,
    cmap=sns.diverging_palette(20, 220, n=200),
    square=True
)
ax.set_xticklabels(
    ax.get_xticklabels(),
    rotation=45,
    horizontalalignment='right'
)
