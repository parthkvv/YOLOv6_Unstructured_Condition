YOLOv6 readme file(https://github.com/meituan/YOLOv6)

Dataset Preparation
	The base data directory should consist of the following files:
		"images" folder - containing the images for train, test and val
		"labels" folder - containing the labels for train, test and val in .txt 				                          yolo format. Each image has seperate file.  
		
		"class.txt" - Txt file with class names (Input to the conv_xml_to_txt.py file)

		Running conv_xml_to_txt.py at the base data directory:
		"train/txt" - generate txt files containing labels(class,xyxy) from original xml labels(Input)
		"val/txt" - generate txt files containing labels(class,xyxy) from original xml labels(Input)
		"train/txt" - generate txt files containing labels(class,xyxy) from original xml labels(Input)

	Generated custom dataset should be in the format :

	custom_dataset
	├── images
	│   ├── train
	│   │   ├── train0.jpg
	│   │   └── train1.jpg
	│   ├── val
	│   │   ├── val0.jpg
	│   │   └── val1.jpg
	│   └── test
	│       ├── test0.jpg
	│       └── test1.jpg
	└── labels
       	    ├── train
    	    │   ├── train0.txt
    	    │   └── train1.txt
    	    ├── val
    	    │   ├── val0.txt
    	    │   └── val1.txt
    	    └── test
        	├── test0.txt
        	└── test1.txt


TRAIN 

	- python tools\train.py --batch 16 --conf E:\IISc\Object_detection\YOLOv6\YOLOv6-main\configs\yolov6s.py --data E:\IISc\Object_detection\YOLOv6\YOLOv6-main\data\dataset.yaml --device 0 --epochs 25 --eval-final-only

	saved weights
	- \tools\runs\train\exp\

(NOTE: DELETE the train.cache, val.cache, test.cache files generated after each run in dataset\labels)


Evaluate :
	(For final mAP calculation on custom dataset) 
	
	Set val variable value in data\custom.yaml as- 
	E:\\IISc\\Object_detection\\IDD\\backup\\images\\test

	- python \tools\eval.py --data E:\IISc\Object_detection\YOLOv6\YOLOv6-main\data\dataset.yaml --batch 2 --weights E:\IISc\Object_detection\YOLOv6\YOLOv6-main\weights\best_ckpt.pt --task val

(NOTE: DELETE the train.cache, val.cache, test.cache files generated after each run in dataset\labels)


EVALUATION :
	(Use xyxy format labels for label and image paths in main() of Evaluation.py) 
	- \Evaluation\Evaluation.py
		- Generate csv files with results
(Refer Evaluation\Readme_evaluation.txt for details)

(NOTE: DELETE the train.cache, val.cache, test.cache files generated after each run in dataset\labels)