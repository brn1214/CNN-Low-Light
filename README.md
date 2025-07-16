# CNN-Low-Light

---

## Objective
To develop a prototype of a low-light object tracking system, to create an algorithm that enhances video illumination and subsequently performs object tracking, and to evaluate the effectiveness of the developed algorithm.

## Tasks

Analysis of scientific literature on the research topic.

Research into methods for improving the quality of video images in low-light conditions.

Development of a prototype of a low-light object tracking system.

Conducting an experiment to test the effectiveness of the implemented low-light object tracking system prototype.

* Video files of any size and with any frame rate.

* Video with improved illumination.

* Video with object tracking.

<img width="1054" height="286" alt="Captura de pantalla 2025-07-16 a la(s) 1 02 25 a m" src="https://github.com/user-attachments/assets/5c9c6bc5-30bb-4c7e-82d3-c38e603730db" />

## Illumination Enhancement Model Architecture

The S-curve parameters, ϕs and ϕh, are determined by a neural network.

The image is converted from the RGB color space to YIQ, and the ϕs and ϕh parameters are determined using the Y channel. Finally, the image is converted back to the RGB color space.

<img width="862" height="584" alt="Captura de pantalla 2025-07-16 a la(s) 1 03 47 a m" src="https://github.com/user-attachments/assets/88d44143-93d9-47dc-9cf4-71920477e89d" />

## **S-curve**
* The SCENet module of the LightenFormer model is used, which is based on an S-curve for illumination enhancement.
* The parameters for illumination enhancement are determined for each pixel, which allows for more precise enhancement.

<img width="457" height="119" alt="Captura de pantalla 2025-07-16 a la(s) 1 05 07 a m" src="https://github.com/user-attachments/assets/9789077d-c37a-4fa8-9c00-cb6407d7d643" />

<img width="363" height="303" alt="image" src="https://github.com/user-attachments/assets/7cf2947c-83f3-46e6-88d0-2656f64464f6" />

## Loss functions

The following loss functions are used to train the network and obtain suitable weights:

<img width="855" height="439" alt="Captura de pantalla 2025-07-16 a la(s) 1 06 21 a m" src="https://github.com/user-attachments/assets/1ae848b0-ac3c-437a-a478-603e4d779679" />

<img width="1081" height="389" alt="Captura de pantalla 2025-07-16 a la(s) 1 09 15 a m" src="https://github.com/user-attachments/assets/084c6e4a-b283-4577-a3f8-472665aa0184" />

The initial model was proposed using the following hyperparameters.
Improved illumination was noted, but artifacts also appeared.

<img width="1213" height="417" alt="Captura de pantalla 2025-07-16 a la(s) 1 10 10 a m" src="https://github.com/user-attachments/assets/aa304752-42cc-472b-a2c8-d291b9041256" />

It was decided to double the number of channels in the network:
The image quality improved, but a loss of contrast was observed in some images.

<img width="1157" height="445" alt="Captura de pantalla 2025-07-16 a la(s) 1 11 25 a m" src="https://github.com/user-attachments/assets/a9126c1d-8514-4647-8fbb-c7968ed03cd7" />

To solve this problem, it was proposed to add a new loss function.

### Sobel edge detector

<img width="530" height="134" alt="Captura de pantalla 2025-07-16 a la(s) 1 11 58 a m" src="https://github.com/user-attachments/assets/2dbacb85-3403-4fa5-bba9-7f1df1db928d" />

Ultimately, the model was trained with the hyperparameters: λe=13, λt=150, λs=10, and λc=5.
The following graph shows the behavior of the loss function over the epochs.

<img width="1238" height="379" alt="Captura de pantalla 2025-07-16 a la(s) 1 13 54 a m" src="https://github.com/user-attachments/assets/06ff4db4-ef4f-47f2-ac7d-7a6c5917221d" />

The model was tested with enhanced video and object tracking.
The MixFormer model does not recognize objects by category and requires manual input of object coordinates in the first video frame.
 
<img width="177" height="100" alt="image" src="https://github.com/user-attachments/assets/dfefe24c-acc9-4f51-8d07-2a4e25817ec2" />
<img width="178" height="100" alt="image" src="https://github.com/user-attachments/assets/9eb2f5c8-fd99-4b75-a971-7bd08c2a4b3c" />

To evaluate the results, the ground truth coordinates of objects in each frame are needed.
Some objects in the selected videos were manually labeled due to the lack of pre-labeled datasets.

<img width="651" height="411" alt="Captura de pantalla 2025-07-16 a la(s) 1 16 06 a m" src="https://github.com/user-attachments/assets/790994cf-1b4e-4190-8986-fe56c078ed65" />

## Conclusions

* The use of unsupervised learning methods overcame the lack of aligned datasets.

* The proposed approach proved effective as it enhances illumination pixel by pixel.

* The algorithm significantly improved the quality of video in low-light conditions.

* The algorithm showed an improvement in the effectiveness of object tracking in low-light conditions.






























