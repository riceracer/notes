# gcloud tool

## init

Run this to set tool context before other commands:

    gcloud init

## copy from storage to local host

    export BUCKET=my-bucket-name
    gsutil -m cp gs://$BUCKET/path/to/files/* .

* the -m flag makes copy operations must faster when using wildcards


## Rsync between buckets

```
export SOURCEBUCKET=source-bucket
export DESTBUCKET=destination-bucket
export BUCKETPATH=path/to/sync
gsutil -m rsync -r gs://$SOURCEBUCKET/$BUCKETPATH gs://$DESTBUCKET/$BUCKETPATH
```

## Bucket to bucket copy

Rsync is better, but in case you need to do this manually:

```
export DOWNLOADBUCKET=foo
export UPLOADBUCKET=bar
DATE=2017-01-03
ENDDATE=2017-01-31
while [ "$DATE" != "$ENDDATE" ]; do 
  echo $DATE
  FILENAME=filename.${DATE}*.csv
  gsutil -m cp gs://$DOWNLOADBUCKET/path/${FILENAME} gs://$UPLOADBUCKET/path/
  DATE=$(date -I -d "$DATE + 1 day")
  echo
done
```
