# FCN with tf 2.0

## Data Preparation

```python3
train_imgs = tf.data.Dataset.list_files("./data/ADEChallengeData2016/images/training/*.jpg")
val_imgs = tf.data.Dataset.list_files("./data/ADEChallengeData2016/images/validation/*.jpg")

train_set = train_imgs.map(parse_image)
test_set = val_imgs.map(parse_image)

dataset = {"train": train_set, "test": test_set}

train = dataset['train'].map(load_image_train, num_parallel_calls=AUTOTUNE)
test = dataset['test'].map(load_image_test)

train
```

<DatasetV1Adapter shapes: ((224, 224, 3), (224, 224, 1)), types: (tf.float32, tf.float32)>

## Define the model

![FCN architecture](./img/fcn_architecture.png)

```python3
from tensorflow.keras import datasets, layers, models

input1 = layers.Input(shape=(224, 224, 3), name='original_img')

conv1_1 = layers.Conv2D(filters=64, kernel_size=(3, 3), padding='same', activation='relu')(input1)
conv1_2 = layers.Conv2D(filters=64, kernel_size=(3, 3), padding='same', activation='relu')(conv1_1)
pool1 = layers.MaxPool2D(pool_size=(2, 2))(conv1_2)

conv2_1 = layers.Conv2D(filters= 128, kernel_size=(3, 3), padding='same', activation='relu')(pool1)
conv2_2 = layers.Conv2D(filters= 128, kernel_size=(3, 3), padding='same', activation='relu')(conv2_1)
pool2 = layers.MaxPool2D(pool_size=(2, 2))(conv2_2)

conv3_1 = layers.Conv2D(filters= 256, kernel_size=(3, 3), padding='same', activation='relu')(pool2)
conv3_2 = layers.Conv2D(filters= 256, kernel_size=(3, 3), padding='same', activation='relu')(conv3_1)
conv3_3 = layers.Conv2D(filters= 256, kernel_size=(3, 3), padding='same', activation='relu')(conv3_2)
pool3 = layers.MaxPool2D(pool_size=(2, 2))(conv3_3)

conv4_1 = layers.Conv2D(filters= 512, kernel_size=(3, 3), padding='same', activation='relu')(pool3)
conv4_2 = layers.Conv2D(filters= 512, kernel_size=(3, 3), padding='same', activation='relu')(conv4_1)
conv4_3 = layers.Conv2D(filters= 512, kernel_size=(3, 3), padding='same', activation='relu')(conv4_2)
pool4 = layers.MaxPool2D(pool_size=(2, 2))(conv4_3)

conv5_1 = layers.Conv2D(filters= 512, kernel_size=(3, 3), padding='same', activation='relu')(pool4)
conv5_2 = layers.Conv2D(filters= 512, kernel_size=(3, 3), padding='same', activation='relu')(conv5_1)
conv5_3 = layers.Conv2D(filters= 512, kernel_size=(3, 3), padding='same', activation='relu')(conv5_2)
pool5 = layers.MaxPool2D(pool_size=(2, 2))(conv5_3)

conv6 = layers.Conv2D(filters= 4096, kernel_size=(7, 7), padding='same', activation='relu')(pool5)
conv7 = layers.Conv2D(filters= 4096, kernel_size=(1, 1), padding='same', activation='relu')(conv6)

# In FCN8, 4Xconv7, 2Xpool4 and pool3 are added
# then 8X upsampled to restore original input size
conv7_4x = layers.Conv2DTranspose(N_CLASSES, kernel_size=(4, 4), strides=(4, 4))(conv7)

pool4_conv1x1 = layers.Conv2D(N_CLASSES, (1, 1), padding='same', activation='relu')(pool4)
pool4_2x = layers.Conv2DTranspose(N_CLASSES, kernel_size=(2, 2), strides=(2, 2))(pool4_conv1x1)

pool3_conv1x1 = layers.Conv2D(N_CLASSES, (1, 1), padding='same', activation='relu')(pool3)

deconv = layers.Add()([conv7_4x, pool4_2x, pool3_conv1x1])
upsample_8x = layers.Conv2DTranspose(N_CLASSES, kernel_size=(8, 8), strides=(8, 8))(deconv)
softmax =layers.Activation('softmax')(upsample_8x)

model = tf.keras.Model(inputs = input1, outputs = softmax, name='FCN8')
model.summary()

```

## Train the model

```python3
train_imgs = glob.glob("./data/ADEChallengeData2016/images/training/*.jpg")
validation_imgs = glob.glob("./data/ADEChallengeData2016/images/validattion/*.jpg")
TRAIN_LENGTH = len(train_imgs)     # 20210
VAL_LENGTH = len(validation_imgs)  # 2000

EPOCHS = 20
STEPS_PER_EPOCH = TRAIN_LENGTH // BATCH_SIZE
VAL_SUBSPLITS = 5
VALIDATION_STEPS = VAL_LENGTH // BATCH_SIZE // VAL_SUBSPLITS

model.compile(
	optimizer='adam',
	loss='categorical_crossentropy',
	metrics=['accuracy']
  )

model_history = model.fit(
	train_dataset,
	epochs=EPOCHS,
    steps_per_epoch=STEPS_PER_EPOCH,
    validation_steps=VALIDATION_STEPS,
    validation_data=test_dataset
  )

```
## Trouble shooting

```
ResourceExhaustedError: OOM when allocating tensor with shape[32,128,112,112] and type float on /job:localhost/replica:0/task:0/device:GPU:0 by allocator GPU_0_bfc

[[node FCN8/conv2d_3/Conv2D (defined at C:\Users\Donghyuk\Miniconda3\lib\site-packages\tensorflow_core\python\framework\ops.py:1751) ]]

Hint: If you want to see a list of allocated tensors when OOM happens, add report_tensor_allocations_upon_oom to RunOptions for current allocation info.
[Op:__inference_distributed_function_3730]

Function call stack:
distributed_function
```

[shared GPU memory](https://stackoverflow.com/questions/47859924/use-shared-gpu-memory-with-tensorflow)

[OOM error](https://www.kaggle.com/c/siim-acr-pneumothorax-segmentation/discussion/97660)

