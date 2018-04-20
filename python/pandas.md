# Read Json file to DataFrame and Plot

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

# Read CSV file into pandas

```
# If the CSV file has headers we don't have to name the fields like this
df = pd.read_csv('intput.csv', header=None, names=['field1, 'field2', 'field3'])
```

# Output to CSV

```
# Index=false to avoid including the numeric row ids in the output csv
df.to_csv(output_filename, header=False, index=False)
```

# Copy columns to new data frame

```
# basically = put the collection of columns/Series in a dict
output = pd.DataFrame(data={'lat': round(100 * df['lat']),
                            'lon': round(100 * df['lon']),
                            'size': df['value']},
                      dtype=int)
```

# MySQL to Pandas DataFrame

Open a `connection`, using a library like pymysql, then:

```
import pandas as pd

sql = "SELECT * from TABLENAME where foo = %s"
df = pd.read_sql(sql, connection, params=['bar'])
```
