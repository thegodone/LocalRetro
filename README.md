# LocalRetro
Implementation of Retrosynthesis Prediction with LocalRetro developed by prof. Yousung Jung group at KAIST (contact: ysjn@kaist.ac.kr).

## Developer
Shuan Chen<br>

## Prerequisites
* Python (version >= 3.6) 
* Numpy (version >= 1.16.4) 
* PyTorch (version >= 1.0.0) 
* RDKit (version >= 2019)
* DGL (version >= 0.5.2)
* DGLLife (version >= 0.2.6)

## Publication
TBD

## Usage
### [1] Download the raw data of USPTO-50K or USPTO-MIT dataset
See the README in `./data` to download the raw data files for training and testing the model.


### [2] Data preprocessing
A two-step data preprocessing is needed to train the LocalRetro model.

#### 1) Local reaction template derivation 
First go to the data processing folder
```
cd Preprocessing
```
and extract the reaction template with specified dataset name (default: USPTO_50K).
```
python Extract_from_train_data.py -d USPTO_50K
```
This will give you four files, including 
(1) atom_templates.csv
(2) bond_templates.csv
(3) smiles2smarts_templates.csv
(4) template_rxnclass.csv (if train_class.csv exists in data folder)<br>

#### 2) Assign the derived templates to raw data
By running
```
python Run_preprocessing.py -d USPTO_50K
```
You can get four preprocessed files, including 
(1) preprocessed_train.csv
(2) preprocessed_val.csv
(3) preprocessed_test.csv
(4) labeled_data.csv<br>


### [3] Train LocalRetro model
Go to the localretro folder
```
cd ../localretro
```
and run the following to train the model with specified dataset (default: USPTO_50K) and use GRA or not (default: True)
```
python Train.py -d USPTO_50K
```
The trained model will be saved at ` LocalRetro/Results/USPTO_50K_GRA_checkpoints/model.pth`<br>

### [4] Test LocalRetro model
To use the model to test on test set, simply run 
```
python Test.py -d USPTO_50K
```
to get the raw prediction file saved at ` LocalRetro/Results/USPTO_50K_GRA_outputs/raw_prediction.txt`<br>
Finally you can get the reactants of each prediciton by decoding the raw prediction file
```
python Decode_predictions.py -d USPTO_50K
```
The decoded reactants will be saved at the same directory with raw prediciton named `decoded_prediction.txt`and `decoded_class_prediction.txt`<br>

## Retrosynthesis on desired product
We also made a python notebook for quick retrosynthesis prediction on desired product at `Retrosynthesis.ipynb`.
See the README in `./Pretrained_models` to download the models for retrosynthesis prediction.

## Reproduce the prediction accuracy in the paper
For fast reproducing the model, we shared the trained model and decoded results at `./Results` directory.
You can get the prediction accuracy of USPTO_50K by running the python notebook `Top_K_accuracy.ipynb` with changing using GRA or given reaction class.


