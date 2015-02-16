# docker-fakes3
FakeS3 Docker Container

#### To Boot
```
docker run -e PORT=5000 -e HOSTNAME=s3.myorganisation.dev -p 5000 boardiq/fakes3
```

#### To Use
```ruby
require 'fog'

conn = Fog::Storage::AWS.new({
  aws_access_key_id:      123, 
  aws_secret_access_key:  "asdf", 
  host:                   ENV['MY_FAKES3_HOSTNAME'], 
  scheme:                 'http', 
  path_style:             true, 
  port:                   ENV['MY_FAKES3_PORT']
})

dir = conn.directories.create key: 'testing'
dir.files.create key: 'newfile.pdf', body: File.open("/path/to/test/file")
```

#### Notes
- The hostname that you connect to FakeS3 on must be the same as the hostname that FakeS3 boots under.
