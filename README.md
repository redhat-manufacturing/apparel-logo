# sports_apparel_logo_monolith 

## Getting Started
- [Podman introduction](https://docs.google.com/document/d/1xCdkYFhxJZ0CFcx8qAWM4bllG80WI3mCfBJfB-kdIKI/edit?usp=sharing)
- Podman storage: we use the podman storage as a backup to our logs and database.

# Here are the 3 ways to start the pipeline

## 1. Run Quay Image

No need to clone github repo

```sh
 $ podman login quay.io
 $ podman volume create apparel-logo-dash-storage
 $ podman pull quay.io/guiseai_retail/apparel-logo:dashboard
 $ podman run --name apparel-logo-container \
  -p 9080:9080 \
  -v apparel-logo-dash-storage:/app/ \
  -d quay.io/guiseai_retail/apparel-logo:dashboard
```

## 2. Build image locally and run it using podman commands

clone the repo
```sh
 $ git clone https://github.com/GuiseAI/apparel-logo-monolith.git
 $ git checkout dashboard
 $ cd apparel_logo_monolith
```

1. build the image and create storage
```sh
 $ podman build -t apparel-logo-dashboard -f Containerfile.root
 $ podman volume create apparel-logo-dash-storage
```

2. run the image
```sh
 podman run --name apparel-logo-container \
  -p 9080:9080 \
  -v apparel-logo-dash-storage:/app/ \
  -d apparel-logo-dashboard
```

## 3. Build and run the image using podman-compose:

clone the repo
```sh
 $ git clone https://github.com/GuiseAI/apparel-logo-monolith.git
 $ git checkout dashboard
 $ cd apparel_logo_monolith
```

To start
```sh
 podman-compose up
```

To stop
```sh
 podman-compose down
```

## Running Unit tests

Replace the session id in 'unit_tests.py' with current session id
```
python3 unit_test.py
```

Replace the session id in 'unit_tests.py' with current session id
```
cd ml_service/application/unit_tests
python3 unit_test.py
```

For Streamer 
```
cd ml_service/application/unit_tests
python3 test_chunker.py
python3 test_reader.py
```

