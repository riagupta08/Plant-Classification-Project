# Project Name

Classifying Images Based on Plant Species 

This project classifies images based on plant species. In a world where most of us thrive off homegrown or farm-made fruits and veggies, this project serves as a great way to detect what kind of plant someone is growing. This project has real-life applications, as it can be used in farms or at home if you often forget what you are planting in your garden.

[This photo depicts results of the project](https://imgur.com/a/vQeuQpu)

## The Algorithm

The algorithm of sorting plant species works by first being trained by being shown a series of images that are different types of plants. Through the resnet tool, AI learns certain features of specific plants, like a series of thorns that aloevera photos would have. After the AI knows which images are which, the AI is shown a new set of images, labels them a type of plant species from their pre-trained knowledge, and exports them to output folders. The options for classifying the images are determined by the categories defined in the labels.txt file in the project folder.

## Running this project

1. Create your dataset by collecting photos. You can use a website like "Kaggle" to find some collections of photos. I used Kaggle to find my dataset, which already came with the categories and the test, train, and val folders. Here is the dataset I used: [https://www.kaggle.com/datasets/yudhaislamisulistya/plants-type-datasets](url).

2. Go into your Linux Terminal/VS code. Download the dataset by typing **curl -L -o ~/Downloads/plants-type-datasets.zip\
  https://www.kaggle.com/api/v1/datasets/download/yudhaislamisulistya/plants-type-datasets**

4. Go to the Docker container by first going to the jetson-inference folder. This can be done by doing **cd jetson-inference** - Then, type **./docker/run.sh**

5. Inside the Docker container, change directories. Type **cd jetson-inference/python/training/classification** - Now, we are in the classification folder. Train the AI with the dataset by doing **python3 train.py --model-dir=models/<Folder> data/<Folder>** Training the AI will take a bit so while the Epoch's are running, create a file called *labels.txt* in the folder inside your data path. This will open up a python terminal, inside this terminal, type the category names on separate lines. Once done, press **Ctrl + S** to save the file. (In the Kaggle dataset, the category names are given. Make sure to type them in the exact order given, all lowercase)

6. Not changing directories, generate resnet18.onnx to process the images we want to test. This can be done by typing: **python3 onnx_export.py --model-dir=models/<Folder>**

Exit the docker by typing **Ctrl + D**, then check to make sure that the model is still there by typing **ls models/<Folder>/** (When exiting the docker, the directory might go back to home. If this happens, type **cd jetson-inference/python/training/classification** to bring you back)

7. Still not changing directories, set the NET and DATASET variables. Type NET=models/ - Then, type DATASET=data/ - These variables will be used in the command to process our images.

8. Test 1 image. Copy the name of an image in the Category 1 folder of your test folder. Type imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/<Name of Category 1>/.jpg .jpg

[Here is a video showing how my project works!](file:///C:/Users/Student/Downloads/NVIDIA%20Project%20(Jetson%20Orin%20Nano)%20(1).mp4)
