# sports_apparel_logo_monolith 

## Getting Started
- [Podman introduction](https://docs.google.com/document/d/1xCdkYFhxJZ0CFcx8qAWM4bllG80WI3mCfBJfB-kdIKI/edit?usp=sharing)
- Podman storage: we use the podman storage as a backup to our logs and database.

# Here are the 3 ways to start the pipeline

## 1. Run Quay Image

- No need to clone github repo
- Make sure for every new pull, change the name of volume

```sh
 $ podman login quay.io
 $ podman volume create <podman-storage-name>
 $ podman pull quay.io/guiseai_retail/apparel-logo:ob_1.0.1_ovino
 $ podman run --name apparel-logo-container \
  -p 9080:9080 \
  -v <podman-storage-name>:/app/ \
  -d quay.io/guiseai_retail/apparel-logo:ob_1.0.1_ovino
```

## 2. Build image locally and run it using podman commands

- clone the repo
```sh
 $ git clone https://github.com/GuiseAI/apparel-logo-monolith.git
 $ cd apparel_logo_monolith
 $ git checkout <branch_name>
```

- Make sure for every new build, change the name of volume

1. build the image and create storage
```sh
 $ podman build -t <apparel-logo-image-name> -f Containerfile.root
 $ podman volume create <podman-storage-name>
```

- Remove -d from command if you want to print logs on terminal

2. run the image
```sh
 podman run --name <apparel-logo-container-name> \
  -p 9080:9080 \
  -v <podman-storage-name>:/app/ \
  -d <apparel-logo-image-name>
```

## 3. Build and run the image using podman-compose:

- clone the repo
```sh
 $ git clone https://github.com/GuiseAI/apparel-logo-monolith.git
 $ cd apparel_logo_monolith
 $ git checkout <branch-name>
```

- Inside contaner-compose.yml file, change image and container_name as per your choice.

To start
```sh
 podman-compose up
```

To stop
```sh
 podman-compose down
```

