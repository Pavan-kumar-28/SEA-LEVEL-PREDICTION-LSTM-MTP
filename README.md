we all know that through out the globe climate change is a very big isuue and this climate change is also influencing the Indian monsoons very much like they have been increasing the breakup cycles of Indian monsoon. So what I have done is using certain deep learning techniques I have predicted the break up cycle of Indian monsoon, this project will mainly be helpful for farmers as many of our farmers life are dependent on rainfall. Hence An accurate forecast of the ISM rainfall is of great importance, from planning for agriculture to disaster preparedness.

The data which i used here is climatic data or we can say satellite data for the past 40 years.
It is a unique data available in the internet not used by many people.
Generally climatic data is often delivered in a time series format. and it can be accessed only via python arrays. and it is a 3d data with var iables lat,long,time.
As my main objective here is to predict Indian summer monsoon 7 days ahead at a certain region. 
Iam not directly predicting rainfall here . we are actually predicting sea level pressure at that region and linking that low pressure fluctuations to that of rainfall. As we all know that if pressure is low at certain region then the chances of rainfall will be more according to water cycle.\ 
The deep learning techniques are advancing at fast pace in the recent years and found to be efficient in atmospheric–oceanic predictions.we employ a deep convolutional long short-term memory (ConvLSTM) model to predict the SLP anomalies over continental India and the Bay of Bengal at a lead time of 7 days during summer monsoon season.\
ConvLSTM elegantly blends properties of 1) LSTM networks in modeling sequential 
data and 2) convolutional neural network (CNN) in handling spatiotemporal data.
So after the model is trained, we test the model and find the required the accuracy.
And finally we will compare the performance of the ConvLSTM model with that of a conventional numerical weather prediction model, namely NCEP-GFS model.


__Data analysis__\
*NetCDF (network Common Data Form) is a hierarchical data format similar to hdf4 and hdf5.It is what is known as a “self-describing” data structure which means that metadata, or descriptions of the data, are included in the file itself and can be parsed programmatically, meaning that they can be accessed using code to build automated and reproducible workflows.\
*The NetCDF format can store data with multiple dimensions. It can also store different types of data through arrays that can contain geospatial imagery, terrain data, climate data, and text.\
*The daily SLP data from NCEP/NCAR reanalysis during 1979-2019 is used for developing the ConvLSTM model\
*NetCDF4 data set is used in which we have access to the different variables like time,longitude,latitude and mean sea level pressure(msl).\
*Size of the dimensions are latitude-73,longitude-144,time-14600 and Shape of the mean sea level pressure variable is (14600,73,144).\
*The region over continental India is bound by 20 ◦N to 30 ◦N and 70 ◦E to 80 ◦E.\
*For Continental India - the shape of the msl is (14600,5,5)\
The data was organised into training and test sets of 1979-2007 and 2007-2019, respectively, and area averaged grid values were computed for the test data.

__Model Implementation__\
*A sequential architecture is used with its first layer as a
ConvLSTM 2D layer with ten filters for handling the
spatio-temporal training data.\
*The input to the layer is a 5-dimensional tensor having the
following attributes: size of training data, channels, latitude,
longitude,stack size/time steps.\
*Each input data is a stack of seven frames corresponding to the
seven day lagged data for SLP anomalies predictions.\
*The output from this layer is then fed into batch normalisation
layer. A dropout layer is also added to ensure that overfitting of
data does not take place during the training phase. Subsequent
layers include MaxPooling layers, a flattening layer, and two fully
connected dense layers.\
*For optimisation of the model, the hyper-parameters and and
layers were tuned to obtain suitable activation, number of filters,
optimiser, dropouts, loss functions, epochs, and batch size.\
*The number of epochs were varied from 10 to 500 and the batch
sizes were varied 32 to 200 and we obtained satisfactory results
with 100-200 epochs and 150-200 batch size during training.\
*The results were obtained with RMSProp optimiser and
Rectified Linear Unit (ReLu) activation.\
*Application of both Mean squared error (MSE) loss function and
Huber Loss Functions yielded models with good prediction
capability.
