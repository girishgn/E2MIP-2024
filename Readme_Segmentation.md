Running the Docker File for Training and Inference:


This document provides detailed instructions on how to set up, build, and run the Docker environment for performing both training and inference using the provided Python and Bash scripts.

1. Folder Structure Overview
    the project folder should include the following components:

    Dockerfile: The file that defines the environment setup and the steps for the container.
    Python Scripts: These handle the actual training (train.py) and inference (test.py) processes.
    Bash Scripts: Shell scripts (training.sh, inference.sh) that manage the execution of the training and inference steps.
    Dataset Storage: Data storage in the mnt folder for training and query data.

    This is the sample folder structure would be
    /<project-folder>
        |-- Dockerfile
        |-- train.py               # Python script for training
        |-- inference.py           # Python script for inference
        |-- training.sh            # Bash script to start training
        |-- inference.sh           # Bash script to start inference
        |-- /mnt                   # different from ../mnt where the data is mounted
            

2. Preparing the Dataset
    Before building and running the Docker container, please mount the neccesary data folders(training_data,training_results,query_data)

3. Building the Docker Image
    Once The dataset is in place, you can build the Docker image. To do so, navigate to the project directory containing the Dockerfile and run the following command:
        "docker build -t dockerfile ."

4. Running the Docker Container
    After successfully building the Docker image, you can now run the Docker container. Execute the following command to start the container and launch the automated training and inference processes:  "docker run -v path_host/training_data:/mnt/training_data -v path_hosts/training_results:/mnt/training_results -v path_host/testing_data_prediction_segmentation:/mnt/testing_data_prediction_segmentation -v path_host/query_data:/mnt/query_data -it dockerfile"

    #note please put the path to the host data in place of path_host in the above command

    -it: Runs the container interactively so you can see the output.
    dockerfile: The name of the Docker image you built in the previous step.

5. Automated Training and Inference
    Once the container starts, it will automatically begin both the training and inference processes. The steps are as follows:

    The training process will commence using the data from mnt/training_data. This process will output a trained model.
    After training completes, the inference process will use the trained model to make predictions based on the data in mnt/query_data.
    No further user input is required once the container is running.

6. Accessing the Predicted Results:
    After the inference is completed the folder structure of mnt subfolder would look like this
    <../mnt>
        |-- training_data/         # Your training data
        |-- query_data/   
        |-- training_results/
        |-- testing_data_prediction_segmentation
    
 # Important notes
 1) mnt directory in submission folder is different from that of where data is mounted ie..."../mnt"
 2) the test prediction folder should be empty before use runining the file
 
