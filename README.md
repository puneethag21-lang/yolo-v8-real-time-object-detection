# yolo-v8-real-time-object-detection
Real-time AI object detection system leveraging YOLO for high-speed and accurate visual recognition.


Step-by-Step Process to Train and Deploy YOLOv8 Model
🔹 Step 1: Create Roboflow Account

1.Go to  https://roboflow.com

2.Click Get Started

3.Sign in using your Google account

🔹 Step 2: Create Workspace

4.Enter your workspace name

5.Skip team invitation and click Create Workspace

🔹 Step 3: Select Dataset

6.Go to Explore section

7.Search for the dataset (Example: Car and bike)

8.Click on the desired dataset

9.Open the Dataset tab from navigation bar

🔹 Step 4: Download Dataset in YOLOv8 Format

10.Click Download Dataset

11.Select format → YOLOv8

12.Copy the provided download code (top right corner copy icon)

Step 5: Setup Google Colab for Training

13.Open Google Colab

14.Set Runtime → GPU

15.Install YOLOv8:
!pip install ultralytics

16.Paste the copied Roboflow dataset download code and run it.

🔹 Step 6: Locate Data.yaml File

17.In Colab file section, locate your dataset folder

18.Open the folder and find data.yaml

19.Click 3 dots → Copy Path

🔹 Step 7: Train the YOLOv8 Model

Run the training command:
!yolo task=detect mode=train model=yolov8m.pt data=[PASTE_COPIED_PATH] epochs=70 imgsz=640
⚠ Replace [PASTE_COPIED_PATH] with your actual data.yaml path.

Now the training will start and model begins learning.

🔹 Step 8: Download Trained Model

20.After training completes, look for:
Results saved to runs/detect/train

21.Open that file

22.Download the best.pt file (this is your trained model)

-> Deployment in VS Code

🔹 Step 9: Setup Local Environment

23.Create a new folder on your system

24.Move best.pt into that folder

25.Open that folder in VS Code

26.Install ultralytics:
pip install ultralytics

🔹 Step 10: Create main.py File

Create a new file named main.py and paste this code:

from ultralytics import YOLO
import cv2

model = YOLO("best.pt")

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    results = model(frame)
    annotated_frame = results[0].plot()

    cv2.imshow("Object Detection", annotated_frame)

    if cv2.waitKey(1) & 0xFF == ord("q"):
        break

cap.release()
cv2.destroyAllWindows()

🔹 Step 11: Run the Project

Run:python main.py

BOOM 🎉 Camera will open and your trained ML model will start detecting objects in real-time.














