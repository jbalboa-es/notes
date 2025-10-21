# Pandas
``` python
import panda as pd

# Series and DataFrames

# Custom indexes

values = [10, 20, 20]

# Series
pd.Series(values, index=['a', 'b' , 'a' ]) #to specify own custom index

# Dataframe
df = pd.DataFrame({
	'clave_1': [values]
})

df = df.set_index('clave_1')

df1 + df2 
#the return is index by index

df.reset_index()


#Import and Export

df.to_ #to export into
df.to_csv('name.csv', index=None) # to specify don't has index

df.read_ #to import
df.read_csv('name.csv', index_col=0) # to indicate which column refer to the index

df.to_dict() #to python dictionary


# Exploration functions

df.head() 
df.tail() 
df.sample() #a random row
# accept a integer parameter

df.columns#return index object with column labels
	list(df.columns)
	
df.index #return index of df (row labels)
df.shape#tuple representing the dimensions

df.options.display.max_columns = i #i: integer value

df.info() #info about DataFrame: Index, Column, Non-Null, Dtype

df.Column_name
df.['column']
 # To return the Serie of that column
 
df.[['col1', 'col2']] #Select more columns
df.[df['column']>value] #Selects rows based on conditions

df.groupby(by=grouping_columns)[columns_to_show].function()
#Groups data based on one or more columns

df.nunique()#number of unique values in each column of DataFrame or a Series
Series.unique()#array of unique values in a Series
df.corr()#pairwise correlation columns

df.sort_values()#sort DataFrame by the values in one or more columns
df.sort_values(by='column', ascending=False)#descending order
df.sort_values(by=['column1', 'column2'])
df.drop_duplicates()#return df with duplicate rows removed.
df['column']=df['column'].astype('dtype') #to change the column type
	#bool, int64, float64, object, etc.. 
df[condition][selection]
type(df.<Column_name>)

# Statiscal Functions

df.describe()#overview about statiscal measures (for numerical columns)
df.describe(include=['dtype1', 'dtype2'])
df.value_counts()#return a Series counting unique values
df['column'].value_counts(normalize=True)#normalize to calculate fractions

df.['column'].
	mean()
	min()
	max()
	std() #standart deviation
	median()
	mode()
	count()
	sum()
	hist(figsize=(width, height)) # also possible with DataFrames 
	#histogram, to modify the graphic you have to use matplotlib.pyplot

# Accessing Data

df.loc[1] #indexing attribute, to access row e.g. row_name:row_name, 'column':'column'
df.set_index('column')
df.loc['Alice' , 'age'] #

df.iloc[1,0] #index by number
df[:1]#first row
df[-1:]#last row

df.at['Alice', 'age'] #to a specific value, no more
df.iat[1, 0]

#You can change the values or add rows

df.iloc[0:2] #last no included
df.iloc[0:3, 1] #row 0 to 2, only 2nd column
df.iloc[:]#all rows

#To apply functions, use apply():
df.apply(np.max)
Series.apply(function)#function will apply to each value of the Series
df[df['column'].apply(lambda 'muted_var': muted_var condition)]

d={'key': value, 'key2':value2}
df['column']=df['column'].map(d)#to replace keys to values
df.replace({'column':d })#to the same


# Summary tables

pd.crosstab(Serie1, Serie2)
	#can add normalize attribute, and margins boolean attribute(True: to add row and columns of totals)
	
	
df.pivot_table(
	['column1', 'column2', ...], #columns
	['pivote_column'], #like group by (values are rows)
)
	#can add aggfun attribute, which receives an function to apply to the values
	
#can do + operations between Series
df.insert(loc=len(df.columns), column='new_column', value=Series)
	#loc is number of columns after insertation

df.drop(['column', 'column2'], axis=1, inplace=True) #to delete columns or rows
	#axis=1 to delete columns, nothing or 0 to delete rows
	#inplace tells whether to change original DataFrame. False, returns a new one, and True alters the current.
df.drop(['index', 'index']) #delete rows


Series=Series */+- number

df.dropna() #to drop nan value
df.fillna(n)#to replace nan value with n
df.notna()#return True or False for each value of df based on whether is a nan value or not
df.iterrows() #to iterate rows
	for i, row in df.iterrows(): #i for index
		print(i)

df.items()#same but to columns
~ #to negate
isin(list)
endswith()

df.query(condition) #return df with condition applied
pd.concat([df1, df2]) #concatenate df
pd.merge(df1, df2)
	how='outer' #keep all
		'inner' #keep intersect
		'left' #keep only left(df1) dataframe values and put Nan if df2 don't have any values associated
		'rigth'
	on='column'
df.join(df2) #like merge but mix the similar column
	how
```
