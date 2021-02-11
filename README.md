# CNN
# #### we are going to use a framework called TensorFlow and Keras. 
#### since our data is sequential so we will use sequential model.
#### from tensorflow ew have imported Dense as we will use fully connected layer after the covolutional layer operations will be over.
#### if we have lots of parameters to learn then in that case we need to use drop-out which basically shuts some the randomly picked neurons. dropout is generally a good idea if we are facing an OVERFITTING(high variance case) condition. the value of dropout is manually entred and its a hit and trail method to find the optimum value.
###### -------
#### after dropout we have imported activation - This plays a major role in any of the deep learning structure. It generally varies from problem to problem. If we have binary classification problem then we use Sigmoid as our activation function (sigmoid has an issue of VANISHING GARADIANT we have relatively okay result in the range of -3 to +3).... Sign function is also used but the gradiant in sign function vanishes everywhere. if we have classes i-e greater than two (say k classes) then for this we use Softmax function.  To overcome this issue of vanishing gradiant problem researchers come up with ReLu (Rectified Linear Unit  max(o,y)). this solves the problem of vanishing gradiant. There is one more activation function which gives some weightage to the negative values as opposed to ReLu which map negatives to zero. As we know that is 2D so we will use flatten command to make a one dimensional vector (to feed it to the nueral network). 

#### now we imported Conv2D--  this will allow us to use 2 dimesional Convolutional Neural Network.
### why convolution layer is used???
#### Lets say we have a colored image of 1000x1000x3 then the number of input features will be 3Millions and we use 1000(say) number of hidden neurons then the WEIGHT MATRIX will be of dimension (1000, 3M) which is around 3Billions of parameters for the network to learn (think about the RAM requirement or what if the image is slightly large). 
#### So we need to impliment CONVOLUTIONAL OPERATION  which is one of the most fundamental building block of CNN.  we apply this operation on the input image & FILTERS f (often called as KERNALS in research papers). Filters are basically used for detecting the edges such as vertical or horizontal edges. we can have several filters which can be used to detect edges at some angles. some of the basic filters we have seen is - vertical edges, horizontal edges, SOBEL filters(this gives weightage to the centre row so its a little bit robust filter), SHAW filter (this is sort of vertical filter but use high values). One thing to note is that all these filter's order is taken as odd(3x3, 5x5). Secondly, we dont choose the values in filter by ourselves.  Lastly, treating the values of the filter as PARAMETERS. we just consider them as parameters and the updation is done using BACK-PROPAGATION with a valid optimizer.  
#### we had DOWNSIDEs of using the convolution operation-- 
#### 1) everytime we detect the edges the image shrinks which we dont want all the time (specially seen in case of large number of hidden layers)
#### 2) All the corner pixels in the input tensor is used only once. Whereas the pixel in the middle overlaps with so many regions of filters while calulation of output. So baisically we are loosing so many corner information. 
#### To deal with these downsides researchers come up with PADDING (n+2p-f+1)---- adding rows and columns to the input tensor depending upon the requirement.
#### Padding is of two types- ------   (1) VALID (p=0)  (2) SAME (p=k - to make output size same as input). 
#### STRIDE-  this is sort of jump we want to take while applying filter with conv operation.


#### the same concept is applied to the colored image (3 channels RGB)- just the tensor size will increase. And a thing to note is that the number of channels is same as number of fliter layers. i-e if RGB image say 39x39x3 then filter can be 3x3x3. 

### The steps followed here are- 
#### convolutional operation is applied between input and filter (we can take any number of filter)
#### we get an output which can be of same dimension if we did padding else it will shrink
#### we apply a BIAS to the output which will be our final tensor.
#### we apply some sort of NON-LINEARITY (ReLu) to get the Y-hat.... cat or dog
#### NOTE: how big the image is we would have constant number of parameters in here---- if we have an image of size 3x3x3. this becomes 27 and a bias so total of 28 parameters. Say we have use 10 filters then we will have 280 PARAMETERS only (independent of size of image).  so we can say that this property makes it LESS PRONE TO OVER FITTING as opposed to simple neural network.
