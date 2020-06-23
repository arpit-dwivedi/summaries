Go to [Object Recognition](https://gitlab.iotiot.in/AIAPA07/module1---get-aligned-with-the-industry-/blob/master/ipopstudy.md#object-recognition) part.

Go to [Pose Recognition](https://gitlab.iotiot.in/AIAPA07/module1---get-aligned-with-the-industry-/blob/master/ipopstudy.md#pose-recognition) part.



# Face Recognition

|        | **Google Vision API** | **Amazon Rekognition** | **Microsoft Cognitive Services**  |
| ------ | ------ | ------ | ------ |
| **Input : Pythonapi to feed input** | N.A | `search_faces_by_image()`  |  <ol><li>`IdentifyAsync()` -To find the closest match of query person face from a large person group.</li> <li>`VerifyFaceToFaceAsync()` - To Verify whether two faces belong to a same person (*Compares a face Id with a face Id*).</li> <li>`VerifyFaceToPersonAsync()` - To Verify whether two faces belong to a same person (*Compares a face Id with a Person Id*).</li></ol>|
| **Input : Format and specs of input supported** | N.A | JPG and PNG only 5Mb / Image, 15Mb / Image from S3.  |  The supported input image formats are JPEG, PNG, GIF (the first frame), BMP. Images max size 4MB  |
| **Output : Output Values** | N.A | <ul><li>**Array of FaceMatch objects** *Type-array* An array of faces that match the input face, along with the confidence in the match.</li>  <li>**FaceModelVersion** *Type-String* Version number of the face detection model associated with the input collection (CollectionId).</li> <li> **SearchedFaceBoundingBox** *Type-BoundingBox object*.</li>  <li>**SearchedFaceConfidence** *Type-Float* *Range-0 to 100*  The level of confidence that the searchedFaceBoundingBox, contains a face.</li></ul> | <ul><li>**faceIds** *Type-array*  Array of query faces faceIds.</li>  <li>**2.personGroupId** *Type-String*  personGroupId of the target person.</li> <li>**largePersonGroupId** *Type-String*  largePersonGroupId of the target large person group.</li> <li>**maxNumOfCandidatesReturned** (optional) *Type-Number*  The range of maxNumOfCandidatesReturned is between 1 and 100 (default is 10).</li> <li>**confidenceThreshold** (optional) *Type-Number*  Customized identification confidence threshold, in the range of [0, 1].</li></ul>|
| **Output : Output format** | N.A | JSON  |  JSON  |
| **Steps Involved** | N.A | Create a collection->Face match->Face verification  | Authorize the API call->Create the PersonGroup->Train the PersonGroup->Identify a face->Request for large scale   |
| **Rate limits** | N.A | Not defined in documentation  |  10 Requests per second  |
| **Number of faces** | N.A | Maximum number of faces processed in an image is 15.  | Up to 64 faces max per image.   |


### On Amazon Rekognition

#### Searching for a Face Using an Image
**Request Syntax**
```json
{
   "CollectionId": "string",
   "FaceMatchThreshold": number,
   "Image": { 
      "Bytes": blob,
      "S3Object": { 
         "Bucket": "string",
         "Name": "string",
         "Version": "string"
      }
   },
   "MaxFaces": number,
   "QualityFilter": "string"
}

```
**Response Syntax will be like this**
```json
{
    "FaceMatches": [
        {
            "Face": {
                "BoundingBox": {
                    "Height": 0.06333330273628235,
                    "Left": 0.1718519926071167,
                    "Top": 0.7366669774055481,
                    "Width": 0.11061699688434601
                },
                "Confidence": 100,
                "ExternalImageId": "input.jpg",
                "FaceId": "578e2e1b-d0b0-493c-aa39-ba476a421a34",
                "ImageId": "9ba38e68-35b6-5509-9d2e-fcffa75d1653"
            },
            "Similarity": 99.9764175415039
        }
    ],
    "FaceModelVersion": "3.0",
    "SearchedFaceBoundingBox": {
        "Height": 0.06333333253860474,
        "Left": 0.17185185849666595,
        "Top": 0.7366666793823242,
        "Width": 0.11061728745698929
    },
    "SearchedFaceConfidence": 99.99999237060547
}
```
### On Microsoft Cognitive Services
**Request URL**
`https://{endpoint}/face/v1.0/identify`

**Response 200**

A successful call returns the identified candidate person(s) for each query face.

JSON fields in response body:
```json
[
    {
        "faceId": "c5c24a82-6845-4031-9d5d-978df9175426",
        "candidates": [
            {
                "personId": "25985303-c537-4467-b41d-bdb45cd95ca1",
                "confidence": 0.92
            }
        ]
    },
    {
        "faceId": "65d083d4-9447-47d1-af30-b626144bf0fb",
        "candidates": [
            {
                "personId": "2ae4935b-9659-44c3-977f-61fac20d0538",
                "confidence": 0.89
            }
        ]
    }
]

```


# Object Recognition

|        | **Google Vision API** | **Amazon Rekognition** | **Microsoft Cognitive Services**  |
| ------ | ------ | ------ | ------ |
| **Input : Pythonapi to feed input** | `localize_objects()` | `detect_labels()`  |  C#- `DetectedObject()`  |
| **Input : Format and specs of input supported** | <ul><li>Supported file formates are JPEG, PNG8, PNG24, GIF, Animated GIF (first frame only), BMP, WEBP,RAW, ICO, PDF, TIFF.</li> <li>For LABEL_DETECTION recommended size is 640 x 480.</li><li>Image files sent to the Vision API should not exceed 20MB.</li></ul>  | <ul><li>Formats : Images and videos are supported</li></ul>  |  <ul><li>Supported image formats: JPEG, PNG, GIF, BMP.</li> <li>Image file size must be less than 4MB.</li> <li>Image dimensions must be at least 50 x 50.</li></ul>  |
| **Output : Output Values** | <ul><li>**Name**-object name</li> <li>**mid**-object id</li> <li>**Score**- probability of the object (*range 0-1*)</li> <li>**position**- the position of the object</li> <li>**bounding boxes**</li></ul>  | <ul><li>**Name**-object name</li> <li>**Confidence**- probability(in %) of the object (*range 0-100*)</li><li>**Instance** </li> <li>**Parent**- To the class which the object belongs</li> <li>**Timestamp**-Only in case of video.</li></ul> |  <ul><li>**Name**-object name</li>  <li>**Confidence**- probability of the object</li> <li>**Description**- Tags like landmark or celebrity name.</li></ul>  |
| **Output : Output format** | JSON | JSON  | JSON   |

### Output sample Google API
```json
{
  "responses": [
    {
      "localizedObjectAnnotations": [
        {
          "mid": "/m/01bqk0",
          "name": "Bicycle wheel",
          "score": 0.94250876,
          "boundingPoly": {
            "normalizedVertices": [
              {
                "x": 0.31517795,
                "y": 0.78651166
              },
              {
                "x": 0.44194958,
                "y": 0.78651166
              },
              {
                "x": 0.44194958,
                "y": 0.9693963
              },
              {
                "x": 0.31517795,
                "y": 0.9693963
              }
            ]
          }
        },
        {
          "mid": "/m/01bqk0",
          "name": "Bicycle wheel",
          "score": 0.93416494,
          "boundingPoly": {
            "normalizedVertices": [
              {
                "x": 0.5033941,
                "y": 0.7553
              },
              {
                "x": 0.6290014,
                "y": 0.7553
              },
              {
                "x": 0.6290014,
                "y": 0.9428198
              },
              {
                "x": 0.5033941,
                "y": 0.9428198
              }
            ]
          }
        },
        {
          "mid": "/m/0199g",
          "name": "Bicycle",
          "score": 0.9013836,
          "boundingPoly": {
            "normalizedVertices": [
              {
                "x": 0.31614146,
                "y": 0.66446227
              },
              {
                "x": 0.6335362,
                "y": 0.66446227
              },
              {
                "x": 0.6335362,
                "y": 0.96874213
              },
              {
                "x": 0.31614146,
                "y": 0.96874213
              }
            ]
          }
        },
        {
          "mid": "/m/06z37_",
          "name": "Picture frame",
          "score": 0.714297,
          "boundingPoly": {
            "normalizedVertices": [
              {
                "x": 0.7882674,
                "y": 0.16615547
              },
              {
                "x": 0.9662208,
                "y": 0.16615547
              },
              {
                "x": 0.9662208,
                "y": 0.3177338
              },
              {
                "x": 0.7882674,
                "y": 0.3177338
              }
            ]
          }
        }
      ]
    }
  ]
}


```


### Output sample Amazon Rekognition
```json
{
            
    {
    "Labels": [
        {
            "Name": "Vehicle",
            "Confidence": 99.15271759033203,
            "Instances": [],
            "Parents": [
                {
                    "Name": "Transportation"
                }
            ]
        },
        {
            "Name": "Transportation",
            "Confidence": 99.15271759033203,
            "Instances": [],
            "Parents": []
        },
        {
            "Name": "Automobile",
            "Confidence": 99.15271759033203,
            "Instances": [],
            "Parents": [
                {
                    "Name": "Vehicle"
                },
                {
                    "Name": "Transportation"
                }
            ]
        },
        {
            "Name": "Car",
            "Confidence": 99.15271759033203,
            "Instances": [
                {
                    "BoundingBox": {
                        "Width": 0.10616336017847061,
                        "Height": 0.18528179824352264,
                        "Left": 0.0037978808395564556,
                        "Top": 0.5039216876029968
                    },
                    "Confidence": 99.15271759033203
                },
                {
                    "BoundingBox": {
                        "Width": 0.2429988533258438,
                        "Height": 0.21577216684818268,
                        "Left": 0.7309805154800415,
                        "Top": 0.5251884460449219
                    },
                    "Confidence": 99.1286392211914
                },
                {
                    "BoundingBox": {
                        "Width": 0.14233611524105072,
                        "Height": 0.15528248250484467,
                        "Left": 0.6494812965393066,
                        "Top": 0.5333095788955688
                    },
                    "Confidence": 98.48368072509766
                },
                {
                    "BoundingBox": {
                        "Width": 0.11086395382881165,
                        "Height": 0.10271988064050674,
                        "Left": 0.10355594009160995,
                        "Top": 0.5354844927787781
                    },
                    "Confidence": 96.45606231689453
                },
                {
                    "BoundingBox": {
                        "Width": 0.06254628300666809,
                        "Height": 0.053911514580249786,
                        "Left": 0.46083059906959534,
                        "Top": 0.5573825240135193
                    },
                    "Confidence": 93.65448760986328
                },
                {
                    "BoundingBox": {
                        "Width": 0.10105438530445099,
                        "Height": 0.12226245552301407,
                        "Left": 0.5743985772132874,
                        "Top": 0.534368634223938
                    },
                    "Confidence": 93.06217193603516
                },
                {
                    "BoundingBox": {
                        "Width": 0.056389667093753815,
                        "Height": 0.17163699865341187,
                        "Left": 0.9427769780158997,
                        "Top": 0.5235804319381714
                    },
                    "Confidence": 92.6864013671875
                },
                {
                    "BoundingBox": {
                        "Width": 0.06003860384225845,
                        "Height": 0.06737709045410156,
                        "Left": 0.22409997880458832,
                        "Top": 0.5441341400146484
                    },
                    "Confidence": 90.4227066040039
                },
                {
                    "BoundingBox": {
                        "Width": 0.02848697081208229,
                        "Height": 0.19150497019290924,
                        "Left": 0.0,
                        "Top": 0.5107086896896362
                    },
                    "Confidence": 86.65286254882812
                },
                {
                    "BoundingBox": {
                        "Width": 0.04067881405353546,
                        "Height": 0.03428703173995018,
                        "Left": 0.316415935754776,
                        "Top": 0.5566273927688599
                    },
                    "Confidence": 85.36471557617188
                },
                {
                    "BoundingBox": {
                        "Width": 0.043411049991846085,
                        "Height": 0.0893595889210701,
                        "Left": 0.18293385207653046,
                        "Top": 0.5394920110702515
                    },
                    "Confidence": 82.21705627441406
                },
                {
                    "BoundingBox": {
                        "Width": 0.031183116137981415,
                        "Height": 0.03989990055561066,
                        "Left": 0.2853088080883026,
                        "Top": 0.5579366683959961
                    },
                    "Confidence": 81.0157470703125
                },
                {
                    "BoundingBox": {
                        "Width": 0.031113790348172188,
                        "Height": 0.056484755128622055,
                        "Left": 0.2580395042896271,
                        "Top": 0.5504819750785828
                    },
                    "Confidence": 56.13441467285156
                },
                {
                    "BoundingBox": {
                        "Width": 0.08586374670267105,
                        "Height": 0.08550430089235306,
                        "Left": 0.5128012895584106,
                        "Top": 0.5438792705535889
                    },
                    "Confidence": 52.37760925292969
                }
            ],
            "Parents": [
                {
                    "Name": "Vehicle"
                },
                {
                    "Name": "Transportation"
                }
            ]
        },
        {
            "Name": "Human",
            "Confidence": 98.9914321899414,
            "Instances": [],
            "Parents": []
        },
        {
            "Name": "Person",
            "Confidence": 98.9914321899414,
            "Instances": [
                {
                    "BoundingBox": {
                        "Width": 0.19360728561878204,
                        "Height": 0.2742200493812561,
                        "Left": 0.43734854459762573,
                        "Top": 0.35072067379951477
                    },
                    "Confidence": 98.9914321899414
                },
                {
                    "BoundingBox": {
                        "Width": 0.03801717236638069,
                        "Height": 0.06597328186035156,
                        "Left": 0.9155802130699158,
                        "Top": 0.5010883808135986
                    },
                    "Confidence": 85.02790832519531
                }
            ],
            "Parents": []
        }
    ],
    "LabelModelVersion": "2.0"
}

    
}

```
### Output sample Microsoft Cognitive Services
```json
{
   "objects":[
      {
         "rectangle":{
            "x":730,
            "y":66,
            "w":135,
            "h":85
         },
         "object":"kitchen appliance",
         "confidence":0.501
      },
      {
         "rectangle":{
            "x":523,
            "y":377,
            "w":185,
            "h":46
         },
         "object":"computer keyboard",
         "confidence":0.51
      },
      {
         "rectangle":{
            "x":471,
            "y":218,
            "w":289,
            "h":226
         },
         "object":"Laptop",
         "confidence":0.85,
         "parent":{
            "object":"computer",
            "confidence":0.851
         }
      },
      {
         "rectangle":{
            "x":654,
            "y":0,
            "w":584,
            "h":473
         },
         "object":"person",
         "confidence":0.855
      }
   ],
   "requestId":"a7fde8fd-cc18-4f5f-99d3-897dcd07b308",
   "metadata":{
      "width":1260,
      "height":473,
      "format":"Jpeg"
   }
}

```

# Pose Recognition
|        | **TFLite** |
| ------ | ------ |
|**Model Used**|PoseNet model|
| **Input : Method to feed input** | `estimateSinglePose()`  |
| **Input : Format and specs of input supported** |  Formats : Images and videos are supported |
| **Output : Output Values** | **Part ID**, with a **confidence score** between 0.0 and 1.0. There are total 16 Part Id and the algorithm is simply estimating where key body joints are.  |
## Output Example
![alt text](https://www.tensorflow.org/images/lite/models/pose_estimation.gif "Logo Title Text 1")