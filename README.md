# Dog Breed Prediction 
[![Accuracy](https://img.shields.io/badge/accuracy-86%2E12%25-green.svg)](https://github.com/DucLeTrong/dog_breed_classification)

## Chewy Updates/Notes
This project was forked for use in the internal Chewy Hackathon called Innovation Week held in December 2021.  It was leveraged as part of the breeds pages on https://be.chewy.com as new functionality to detect a breed by uploading a picture.  The following changes were made.  These changes were done quick and dirty as part of getting a working demo up and running.
- Added flask to the infer script to turn this code into a simple api (/classify?image=<image-url>).  An example: https://rschwager.pythonanywhere.com/classify?image=https://random.dog/5540b113-87af-4280-b998-d12a13d6b5ec.jpg.  Note: This url will work through March 2022.
- Modified the script to take image urls as well as file paths.
- Changed the output of the infer script/API to JSON.  Boosted the confidence number by 10x in the response.  Example:
```
{
  "breedsClassified": [
    {
      "breed": "Bullmastiff",
      "confidence": "0.36959701776504517"
    },
    {
      "breed": "Boxer",
      "confidence": "0.31436026096343994"
    },
    {
      "breed": "Dogue_de_bordeaux",
      "confidence": "0.31120267510414124"
    }
  ],
  "humanDetected": false,
  "dogDetected": true
}
```
- Included the model as part of the repository.
- Removed the version requirements from requirements.txt.
- There is a logic error when neither a human nor a dog is detected as confident.  That got commented out.
- For Chewy employees, you can read more about this project at: https://chewyinc.atlassian.net/wiki/spaces/ME/pages/1406534670/Breed+Detector

To run as an API, run these commands from the project directory:
```
export FLASK_APP=infer
flask run
```
This will setup a server at http://localhost:5000/.  You can test by hitting that url and you should get an "OK" response.
  
## About data set
The dog breed dataset consists of 133 different breeds
- [Data](https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip)

- Download data and unzip:
```
$ wget https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip

$ unzip dogImages.zip
```


## Training
- Clone project
```
$ git clone https://github.com/DucLeTrong/dog_breed_classification

$ cd dog_breed_classification
```

- Install requirements
```
$ pip3 install -r requirements.txt
```

- Train model 
```
$ python3 train.py 
```

## Test model 
```
$ python3 test.py 
```

## Inference
```
$ python3 infer.py --img_path='2.jpg' --model_path='model.pt'
```
- If a __dog__ is detected in the image, return the predicted breed.

![png](result/result_dog.jpg)

- If a __human__ is detected in the image, return the resembling dog breed.

![png](result/result_human1.jpg)

![png](result/result_human2.jpg)

- If __neither__ is detected in the image, provide output that indicates an error.

