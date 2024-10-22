# low-resource-translation
Project 2 of the course IFT6759

## Running the evaluation script
Install the virtual environnement and call the evaluator.py script with the proper input file and target file.
```
# create and source a clean virtual env
pip install -r requirements.txt

# run the evaluator
python evaluator.py --input-file-path /project/cq-training-1/project2/data/train.lang1 --target-file-path /project/cq-training-1/project2/data/train.lang2
```

## Train models

### Train on aligned data
Example to train a transformer on the aligned data.
```
python train.py --model_name=transformer --batch_size=128 --epochs=100
```

### Train with pre-trained embeddings
Example to train a transformer with pre-trained embeddings.
```
python train.py --embedding=fasttext --embedding_dim=256 --model_name=transformer --batch_size=128 --epochs=100
```

### Train with back-translation
Example to train a transformer using back-translation.

1. First train a model target->source (fr->en)
```
python train.py --fr_to_en --model_name=transformer --batch_size=128 --epochs=100
```
2. Train the model source->target (en->en)
```
python train.py --back_translation=True --back_translation_model=<path_to_model> --back_translation_ratio=4 --model_name=transformer --batch_size=128 --epochs=100
```

> Model configurations can be passed with the argument --config=<configuration_dict>
