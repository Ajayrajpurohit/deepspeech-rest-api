deepspeech rest api
===================

Simple api over mozilla deepspeech voice recognition engine.

## Endpoints
```
POST /api/v1/stt - Just look at curl command below.
Speech data may be provided in whatever audio format which ffmpeg is able to convert to wav,
so you probably don't have to worry about this at all.

$ curl -X POST -F "speech=@speech.mp3" http://127.0.0.1:8000/api/v1/stt 
{"text":"experience proves this","time":0.9638644850056153}
```

## Setup

### 0. Checkout repository
`git clone git@github.com:zelo/deepspeech-rest-api.git`

### 1. Download deepspeech data model
1. Look at `requirements.pip` file and find what is the current 
deepspeech library version used by this api
2. Go to `https://github.com/mozilla/DeepSpeech/releases` and find release doc for this version.
It should contain link to download data model. For version 0.7.1 it's `https://github.com/mozilla/DeepSpeech/releases/download/v0.7.1/deepspeech-0.7.1-models.pbmm`
3. Download and extract model from above package to `<repository_root>/model.pbmm`

### 2.1 Using docker
1. Enter `<repository_root>`
#### 2.1.1 Using `docker-compose`
1. Run `docker-compose up`
#### 2.1.2 Using `docker run`
1. Build image
`docker build . --tag zelo/deepspeech-rest-api:0.7.1`
2. Run
`docker run --rm --publish=127.0.0.1:8000:8000 --volume=$(pwd)/model.pbmm:/app/model.pbmm:ro zelo/deepspeech-rest-api:0.7.1`
### 2.2 Running outside of docker
Just look at the content of `Dockerfile` it contains complete instruction to setup app under `debian`
