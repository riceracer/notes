# Pandas

```
import pandas as pd
```

## Read Json file to DataFrame and Plot

```
import pandas as pd
import pylab

filename='source.json'
df = pd.read_json(filename)
num_entries = len(df)

# print statistics
print("\nMEAN\n", df.mean())
print("\nMEDIAN\n", df.median())

# may be needed to make plots show
pylab.ion()

# plot histogram. Use log y-scale when needed
df.hist(column='lat', bins=200)
df.hist(column='depth', bins=200, log=True)

# scatterplot (great for geographic plots!)
df.plot.scatter(x='lon', y='lat', s=1, title='All Locations')

# filter stuff!
dist_to_coast = 1
depth = -10
filter = (df['distToCoast'] < dist_to_coast) & (df['depth'] > depth_threshold)
include = df.loc[filter]
exclude = df.loc[~filter]

# show two datasets in same scatterplot
ax = include.plot.scatter(x='lon', y='lat', s=1, title='Combined plot', color='b')
exclude.plot.scatter(x='lon', y='lat', s=1, title='Combined plot', color='r', ax =ax)

# if running a script use input() to block until exit
input("Press Enter to exit...")
```

## Read CSV file into pandas

```
# If the CSV file has headers we don't have to name the fields like this
df = pd.read_csv('intput.csv', header=None, names=['field1, 'field2', 'field3'])
```

## Write to CSV

```
# Index=false to avoid including the numeric row ids in the output csv
df.to_csv(output_filename, header=False, index=False)
```

## Copy columns to new data frame

```
# basically = put the collection of columns/Series in a dict
output = pd.DataFrame(data={'lat': round(100 * df['lat']),
                            'lon': round(100 * df['lon']),
                            'size': df['value']},
                      dtype=int)
```

## MySQL to Pandas DataFrame

Open a `connection`, using a library like pymysql, then:

```
sql = "SELECT * from TABLENAME where foo = %s"
df = pd.read_sql(sql, connection, params=['bar'])
```

## Filter DataFrame by string prefix

```
fieldname = 'names'
prefix = 'Da'
filtered_df = df.loc[df[fieldname].str.startswith(prefix)]
```

## Groupby

Group and put items into a list
```
grouped = df.groupby(['KEYFIELD'])
values_by_group = grouped.apply(lambda x: (list(x['FIELD1']), list(x['FIELD2'])))
```

## Keys

Get keys to the df:
```
keys = df.keys()
```

## Append series

```
s1 = df['foo']
s2 = df['bar']
joined = s1.append(s2).unique()
```

## Pandas Timestamps

Assuming some input of parseable datetimes (like ISO8601):

```
sourcetimes = ...  # list of strings
pd_times = list()
pd_times.extend([pd.to_datetime(x) for x in sourcetimes])
```

## Sample timeseries

* Real docs: https://pandas.pydata.org/pandas-docs/stable/timeseries.html
* Assuming a 'time' column with Timestamps in the dataframe:
* pad/ffill option does a forward fill - fills values with last value in the series before the interval time (typically right choice when you don't want to peak into the future).

```
time_column = 'event_time'
time_interval = '15Min'
df = df.drop_duplicates(time_column)
df = df.set_index(time_column)
df = df.asfreq(time_interval, method='pad')
```

## Difference/calculate between successive rows in DataFrame

builtin:
```
foo = df['FIELDNAME'].diff()
```

manual (or for other functions):

```
# difference
foo = df['FIELDNAME'] - track_df['FIELDNAME'].shift(1)

# some other calc:
foo = bar(df['FIELDNAME'], track_df['FIELDNAME'].shift(1))
```

## Column min of other columns

```
df['min_thing'] = df[['thing1', 'thing2']].min(axis=1)
```

## Select set of columns from DataFrame to flatten into feature list

When working with a timeseries dataframe and you want to flatten to a single list of feature and label values

```
# feature_df = dataframe
feature_names = ['col1', 'col3', 'col5', 'col7']
num_elements = len(df) * len(feature_names)
features = df[feature_names].values.reshape(num_elements)
labels = df['LABEL_COLUMN'].values
```

## Filter by multiple columns

    df2 = df[(df['col1'] == False) & (df['col2'] == True)]

## Find rows with NaN

    df.loc[df['field1'].isna(), :]
    
## Replace rows of NaN with Nones

    df1 = df.where((pd.notnull(df)), None)
    
## Show value counts of a column in a dataframe

    df.field_name.value_counts()

## Print ALL rows of a data frame

```
with pd.option_context('display.max_rows', None, 'display.max_columns', None):
    print(df)
```

## Get distance to location in Data Frame

```
from geopy.distance import vincenty

# target must be in lat, lon order
target = (33.0544, 33.6637)
df['dist2target'] = df.apply(lambda x: vincenty((x['lat'], x['lon']), target).km, axis=1)
```
