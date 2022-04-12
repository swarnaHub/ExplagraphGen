# ExplagraphGen

PyTorch code for our ACL 2022 paper:

[Explanation Graph Generation via Pre-trained Language Models: An Empirical Study with Contrastive Learning](https://arxiv.org/abs/2204.04813)

[Swarnadeep Saha](https://swarnahub.github.io/), [Prateek Yadav](https://prateek-yadav.github.io/), and [Mohit Bansal](https://www.cs.unc.edu/~mbansal/)

## Installation
This repository is tested on Python 3.8.3.  
You should install the repository on a virtual environment. All dependencies can be installed as follows:
```
pip install -r requirements.txt
```

## ExplaGraphs Dataset
ExplaGraphs dataset can be found inside the ```data``` folder. For more details, check out the ExplaGraphs website hosted [here](https://explagraphs.github.io/).

It contains the training data in ```train.tsv``` and the validation samples in ```dev.tsv```.

Each training sample contains four tab-separated entries -- belief, argument, stance label and the explanation graph.

The graph is organized as a bracketed string ```(edge_1)(edge_2)...(edge_n)```, where each edge is of the form ```concept_1; relation; concept_2```. 

## Contrastive Graph Data
All the negatively perturbed graphs for training our contrastive models can be found in ```contrastive_data/train.neg_target```.

The corresponding gold samples (belief, argument, stance) and the gold graphs are contained in ```contrastive_data/train.source``` and ```contrastive_data/train.target```. The files are created in a way to be directly used for training the models.

The positively perturbed graphs can be found in ```contrastive_data/train.pos_target```.

## Models

We experiment with rationalizing models that first predict the stance and then conditions on it to generate the graph.

For training the stance prediction model, run the following script
```
bash scripts/train_stance.sh
```
The validation samples in ```contrastive_data/val.source``` are already appended with the predicted stances from our best model. If you train your own stance prediction model, replace the stances in ```contrastive_data/val.source``` with your predictions so that you condition on the predicted stances before generating the graph.

Next, the Max-margin Graph Generation model and the Contrastive model can be trained using the following scripts.
```
bash scripts/train_graph_max_margin.sh
bash scripts/train_graph_contrastive.sh
```

All trained models will be saved in the ```models``` folder. The scripts to evaluate your models can also be found in the ```scripts``` folder.

We'll share our trained models soon. Stay tuned!

## Predictions
You can find the predicted stances and the generated graphs from our max-margin model in ```output/preds.tsv```.

## Evaluation Metrics
For running the evaluation metrics, refer to the detailed steps outlined in the original [ExplaGraphs](https://github.com/swarnaHub/ExplaGraphs) repository. If you wish to reproduce our results on the validation set of ExplaGraphs, run the evaluation scripts on ```output/preds.tsv```. 

Note that the test set is hidden and if you wish to evaluate your own model on it, refer to the instructions [here](https://github.com/swarnaHub/ExplaGraphs).

### Citation
```
@inproceedings{saha2022explagraphsgen,
  title={Explanation Graph Generation via Pre-trained Language Models: An Empirical Study with Contrastive Learning},
  author={Saha, Swarnadeep and Yadav, Prateek and Bansal, Mohit},
  booktitle={ACL},
  year={2022}
}
```

### Related Citation
```
@inproceedings{saha2021explagraphs,
  title={ExplaGraphs: An Explanation Graph Generation Task for Structured Commonsense Reasoning},
  author={Saha, Swarnadeep and Yadav, Prateek and Bauer, Lisa and Bansal, Mohit},
  booktitle={EMNLP},
  year={2021}
}
```
