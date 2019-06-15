# Grab
This is step by step instruction on how to evaluate my model with test dataset.

1. Open Ten.ipynb in jupyter notebook
2. Run Import packages and functions
3. Scroll down to Test and import your test data
4. import my_model3.h5 model 
5. run all cells below.

If you would like to oversee training process, you need do 
1. Change 'mypath' and 'labels path' to your dirtectoty.
2. run the remaining cell by cell until Test session.

My process for solving safety challenge is :
1. Remove high gps accuracy (meters) and discontinued sensor data
2. Remove low speed because I would like to analyse driving behaviosrs.
3. Scale data into [-1,1] by min-max scaling.
4. Create total_acceleration and total_gyro features by adding accelteration vecters and gyro vecters in x,y,z axis respectively
5. I choose a time lenght at the minimum no.records of BookingID in training set (=120 second)
6. Select Feature to train model (acc_x, acc_y, acc_z, gyro_x, gyro_y, gyro_z, Speed, total_acceleration, total_gyro)
7. Sampling data with non-overlap 120 second frame.
8. Split sampling data to training set and test set at 80% : 20%
9. train the CNN model (minimize categorical_crossentropy)
10. Evaluation and tune parameter by AUC score 
11. Evaluation on test set.

### Prediction idea

1. Split driving data into non-overlap 120 time frames.
2. Run model on each frame.
3. Average the prediction. If the result is greater than 0.5, set BookingId to 1.

### Problem-solving
As a driver, There are many reasons caused to driving dangerously.
For example, In rush hour, Grab driver need to take a customer to the airport. 
So driver need to drive with high speed and acceleration. As a result, ML model will predict the BookingId trip to be dangerous.
However, This is customer satisfaction to arrive the airport on time. To summerise, The best ways to detect if
the driver is driving dangerously. To be fair, we should use ML model with other data sourcess (ex. customer review or camara)
to get all aspects during the driving trip before judging anything. 

