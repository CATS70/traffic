Hereafter the different configurations I tested:
I started with a Basic config adapted from lecture notes :
model = tf.keras.models.Sequential([
# Convolutional layer. Learn 32 filters using a 3x3 kernel
tf.keras.layers.Conv2D(32, (3, 3), activation="relu", input_shape=(30, 30, 3)
),
# Max-pooling layer, using 2x2 pool size
tf.keras.layers.MaxPooling2D(pool_size=(2, 2)),
# Flatten units
tf.keras.layers.Flatten(),
# Add a hidden layer with dropout
tf.keras.layers.Dense(128, activation="relu"),
tf.keras.layers.Dropout(0.5),
# Add an output layer with output units for all 10 digits
tf.keras.layers.Dense(43, activation="softmax")
])
The result was very poor (an accuracy of around 0.05)
Then I doubled hidden layers => not much improvement
Then I doubled the units of the 2 hidden layers (from 128 to 256) => not much improvement
My first improvment came when I doubled convolution and pooling and went back with 1 hidden layer and dropout. This increased highly the accuracy from 0.05 to 0.94
So I tried to keep 2 convolution and pooling  and increase the number of hidden layer and dropout. This decreased the accuracy from 0.94 to 0.66
My 1st conclusion was that playing with hidden layer doesn't help much. So I concentrated myself on convolution and pooling.
So I doubled filters of the 2 convolution (32 -> 64). This decreased highly the accuracy. Back to 0.05 and was time consuming
So I went back to 1 convolution and doubled filters (32 -> 64) =  decrease highly the accuracy. Back to 0.05
My second conclusion was that playing with number of filter doesn't help much too.
Then I did some changes to convolution and pooling size backing to a 32 filters:
A convolution size of 5x5 decreased th accuracy to around 0.86 
A pooling size of 3x3 decreased highly the accuracy. Back to 0.05
My 3rd conclusion was that playing with convolution and pooling size is inefficient.
Then I went back to the very first setting and apply some changes to dropout values:
dropout at 0.3 decrease lightly the accuracy
dropout at 0.7 = accuracy strongly decrease
Based on these experiments I concluded that the best tuning was on the convolution and pooling size. This seems logical afteward because this steps simplify the image to be analyzed.
However I tried new settings:
I tripled convolution and pooling and then caused an error (I guess iamges are too small)
I kept 2 convolution but only with 1 pooling. This gave good results but it' time consuming with an asymptote begining at epoch 5
Then I used my more efficient settings with grayscale image
2 convolution + 2 pooling + grayscale => Same results than before but with better performance.

My final conclusion for this kind of computer vision is that the best results ar given with greyscal images and 2 convolutions and pooling.