### CloudFront

CloudFront is a content delivery network. User would first query an edge location for a file, if that file doesn't exist in the edge location, it would then be fetched from the origin (for example, an S3 bucket). Later when a second user queries the same file, the file will then be served from the edge location.

CloudFront is used to make `S3 transfer acceleration` possible. Your files will be first uploaded to edge locations, then through AWS backbone network uploaded to your bucket.

- Objects are cached for the life of the TTL (Time To Live)

- You can invalidate cached objects, but you will be charged.
