# BAP-Computer-Vision-
Part of the Biomedical Society at UTS, the Bionic Arm Project (BAP) involved developing a mechanical hand controlled by a computer vision system. This code was developed by the software team: 

Author (me, Adrian) - [Linkedin](https://www.linkedin.com/in/adrian-kumar-a70b0b259) 

Daniel (software lead) - [Linkedin](https://www.linkedin.com/in/daniel-chahine-50a2ab264?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3BtRjad9KdTLyZIWjYuTQ8IA%3D%3D)

Anurag - [Linkedin](https://www.linkedin.com/in/anurag-majumder-481029232?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3BT4lBAii%2FR%2F2kfUeYqo3G1w%3D%3D)

Jacob - [Linkedin](https://www.linkedin.com/in/jacob-bayne-02835a277?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3B3ThAKzUJR7S5ulri5DFnEw%3D%3D)

You can view the video of how this code actually translates to movement in the mechanical hand [here](https://drive.google.com/drive/folders/1-24nlewgdvUrevBZ6LZN-M61UWab__Bv?usp=sharing) as trying out this code is simply the interface for the computer vision component.


# How to use:
1. Create a virtual environment and install required libraries from requirements.txt
2. Copy the 'remastered.py' code in virtual environment and run!
3. Press 'g' to stop all processes and stop the program safely

# Notes
Please note that this code was intended to be made on windows application, the Matplot section uses windows backend settings so any errors on different operating system may just be due to compatability.

There will be 16 angles calculated on your terminal when your hand is in frame, to understand what these angles are, the image below depicts where angle A and B are on each finger:

<img width="417" alt="image" src="https://github.com/user-attachments/assets/103124ef-a7b6-406e-9a20-6a456b5d5e8c">

The lateral angle (lat) isn't shown because it isn't a point. However the lateral angle represents your fingers side to side movement (i.e if your hand is in the position of the image above, you'll notice that the lateral angle for the middle finger is nearing 90 as its essentially straight, while the other fingers aren't). The image below shows conceptually how this looks:

<img width="284" alt="image" src="https://github.com/user-attachments/assets/be99b991-b366-4df7-97d4-00e1a2364627">

The angles that get printed on your terminal are sent in this order:
- thumb(A, B, lat, lat), index(A, B, lat), middle(A, B, lat), ring(A, B, lat), pinky(A, B, lat)


For example:

[180, 180, 90, 90, 180, 180, 90, 180, 180, 90, 180, 180, 90, 180, 180, 90] 

would be a sample output, the first 4 elements are the thumb angles in the order (A, B, lat lat)

then the following set of 3 elements are the next fingers angles in the order (A, B, lat)

Clench your fists, spread or close your fingers and see those angles change!

# How its working
This code has 4 componenets: 
1. Computer Vision - Uses camera to capture hand
2. Angle calculation - When hand detected, performs bending joints and lateral angle calculations in real time
3. Matplot - When hand detected, plots the landmark data on a coordinate system
4. BLE connection. - Looks for the microcontroller device to connect and send angles to (however this will not connect to anything on your end so you can simply ignore its process as it will stop itself or comment out the function)

Each of these 4 components are spread into functions each with their own nested functions and variables to be used, this for easier organisation and scalability as each of these functions run concurrently due to the multiprocessing implementation, meaning they all run independently of each other, hence they use a shared data class/object to control when to perform their dedicated functions.

