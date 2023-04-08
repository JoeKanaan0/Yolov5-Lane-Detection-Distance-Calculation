# Yolov5-Lane-Detection-Distance-Calculation



## Instructions to run

Step 0: If you already have machine learning frameworks such as tensorflow or pytorch installed, or libraries that are used in machine learning such as numpy, matplotlib, scipy... These libraries can interfere with the installation. So you could either type pip uninstall {library_name} in the terminal for each library, or you could do the other recommended option which is opening a virtual environment that will use the packages locally and won’t interfere with packages installed on your system. If you don’t want to use a virtual environment, you can skip the instructions in this step and open up the command prompt instead:

To Install a Virtual Environment:

Open your browser and search anaconda download or use this URL “https://www.anaconda.com/products/distribution” if you don’t already have it. And download it for windows. It should be roughly around 750 MB.

After downloading it you can run the .exe file to install it on your system and check all boxes on the page where there are 4 boxes except for the one that says, “Add to your PATH”. 
After installing anaconda, open up your window search and type anaconda, and you should see “anaconda prompt”, click it and a terminal similar to the command prompt should pop up. You should see something like:

	(base) C:\Users\user>

After that you need to create a virtual environment where you will run your project from, first you need to run the command:

	conda create -n yolov5 python=3.8


The command prompt will ask you to input N or Y, press Y and hit enter.


Note: you can choose a different name than yolov5 but it’s a good choice to always choose a name that you will remember later.

After you’ve created your environment you need to activate it. To do so run the command:

	conda activate yolov5

After running this command you should see something like this


	(yolov5) C:\Users\user>


Now you’ve successfully created a virtual environment. You can deactivate it using 


	conda deactivate


But it is not required, you could simply close the terminal after finishing using the project. And when you want to later on open the environment, you open the anaconda prompt, and you simply activate it again using:


	conda activate yolov5


The steps after this will be the same if you either are using the command prompt or the anaconda prompt.

Step 1: In the command prompt/anaconda prompt, use the command: 

	cd "{project_path}"

Replace {project_path} by the path of the yolov5 folder. To get the path you could click on the folder and in the top bar you can see the path, click it and hit CTRL + C to copy it and then go to your prompt and type cd, then a space, then CTRL + V to paste it. And then hit enter. After doing that the path should no longer be C:\Users\user> but rather, the path of your folder.


Step 2: Make sure you're on the right path, type the command: 

	dir

You should see something like:

04/06/2023  04:24 PM    <DIR>          .
04/07/2023  09:57 AM    <DIR>          ..
04/06/2023  04:02 PM               151 .gitattributes
04/06/2023  04:02 PM    <DIR>          camera_cal
04/06/2023  04:02 PM    <DIR>          data
04/06/2023  04:02 PM    <DIR>          deep_sort
04/06/2023  07:07 PM    <DIR>          inference
04/06/2023  05:41 PM            22,996 lane_finding.py
04/06/2023  04:02 PM            35,801 LICENSE
04/06/2023  04:02 PM    <DIR>          MOT16_eval
04/06/2023  04:02 PM             5,419 README.md
04/06/2023  04:34 PM               507 requirements.txt
04/06/2023  04:23 PM    <DIR>          runs
04/06/2023  04:02 PM            55,418 steering_wheel_image.jpg
04/06/2023  05:04 PM            15,091 track.py
04/06/2023  04:02 PM    <DIR>          yolov5
04/06/2023  04:24 PM        42,806,829 yolov5m.pt
04/06/2023  05:41 PM    <DIR>          __pycache__
               8 File(s)     42,942,212 bytes
              10 Dir(s)  98,276,859,904 bytes free


Step 3: Now that you're in the correct folder, you need to install the pytorch framework, so run the command:


	pip install torch==1.8.0 torchvision==0.9.0


Or if you have a GPU on your machine and you want to use it, then you can run the command:

	pip install torch==1.8.0 torchvision==0.9.0 -f https://download.pytorch.org/whl/cu111/torch_stable.html



But running the GPU command requires that you already have CUDA installed so you need to install cuda beforehand, from
the official nvidia website at the URL: "https://developer.nvidia.com/cuda-11.3.0-download-archive". 

Note: It will take some time since pytorch is a big framework.

Note: You only need to install cuda if you want to use a GPU, if you want to use your CPU (Which is much slower), there
is no need to install it and you should run the first command.


After installing pytorch you need to also run:

	pip install pyshine


Pyshine is a library that Pytorch will use in this project.



Step 3: You also need to install the required packages that yolov5 uses to run the code. To do that 
you need to run the command: 


	pip install -r requirements.txt


This will take sometime because there are alot of packages that yolov5 requires.


Step 5: After you've installed all the necessary libraries, you need to run the model on the video, to do that you use this command:

	python track.py --source "{video_path}" --show-vid --save-vid


Here the video_path is the path of the video mp4 file.

Note: The --show-vid arguement is present to show the video while the model is training, and since it's a big model, the frame
rate wil be slow, but the outputted video will have a normal framerate. If you only want the outputted video and you don't
want to see the model while it's running on the video, you can remove --show-vid and it will also help make the model faster.

Note: The --save-vid will save the video that contains the lane and distance detection. So if you only want to see the model
being trained and you don't want to save the video, you can remove this command. To find the downloaded folder navigate to 
your project then go into the yolov5 sub-folder, then into the data sub-folder, then into the outputs sub-folder and there you
will find the video result.


Step 6: Now the video is working and everytime you want to test the model on a video all you have to do is navigate to the folder
using the "cd" command and run one of the commands in Step 5. (If you're using anaconda you have to activate the virtual environment
beforehand).


Final Note: The model was trained on the test_sample video inside the yolov5 folder so the model will perform best on videos that are similar to it. Each video has
it's own specific camera configurations and would produce different results. And the lanes in each video might not be detected well 
depending on the lane visibility, camera quality, and many other factors. The warning system also currently displays a warning for
any object that's closer than 1 meter no matter if it's infront of it or not. If you want to make it only display a warning when
the object is 1 meter away and if it's infront of it. Then open up the track.py code and uncomment the line 248 by removing the '#'.
