# Keras Training

## csv collection

Run VisionAware and open Detection Window (the button "Collect Coordinate Information").  
Begin detection, then press the button to collect coordinate information.  
These csv files will be saved under the directory "csv".  
*Note: you must choose a model that contains the same number of objects as you are detecting. Detection Window currently does a check to see the number of objects before saving a csv file.*  

## Data augmentation

Clone the predict-object-location repository (`git clone https://github.com/NeuronAware/predict-object-location.git`) and open Augment Numbers Binary.ipynb.  
Modify the two paths in the first cell for input csv files and the two paths in the final cell for the output paths (for passing and failing).  
In the third last cell, you can set parameters for augmentation. Currently, the augmentation creates about 30000 augmented csv files for both pass and fail with 10 input files.  

## Binary classification

When ready, open binary_classification.ipynb.  
In the first cell, edit the variable `objects` to the correct number of subparts.  
If necessary, modify the network structure to your needs.  
If necessary, modify the csv paths in the second cell. The first block will expect a failing dataset and the second will expect a passing dataset.  
In the second last cell, you may introduce a loop to perpetuate the training process. Otherwise, just set the number of epochs with the variable `increment` or manually.  
In the final cell, you may set the saved model name.  

## Protobuf conversion

After training, you may use keras_to_tensorflow.py to convert the keras model into a tensorflow protobuffer. The usage is as follows:  
`python keras_to_tensorflow.py --input_model="path/to/keras/model.h5" --output_model="path/to/save/model.pb"`