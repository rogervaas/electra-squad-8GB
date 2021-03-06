# electra-squad-8
Fine tuning Electra large model using RTX2080 8 GB on Squad 2 

This repo is a clone of original implementation of Electra (https://github.com/google-research/electra).

I did a fine tunning on Squad 2.0 of the large pre-trained model, using a limited resource GPU RTX 2080 8GB.

To achieve this I did:
- reduce batch size to 4 (original is 32)
- use mixed precision to slight reduce the memory consumption.
- freeze 2/3 of the network and train the last 8 layers (layer 16 to 23).

All other params (lr, warmup etc) kept unchanged.

With one epoch (~ 8 hours of computing), the eval results were:
```
- HasAns_exact: 82.22 
- HasAns_f1: 87.31 
- HasAns_total: 5928.00 
- NoAns_exact: 91.34 
- NoAns_f1: 91.34 
- NoAns_total: 5945.00 
- best_exact: 86.85 
- best_exact_thresh: -2.53 
- best_f1: 89.41
- best_f1_thresh: -2.53 
- exact: 86.79 
- f1: 89.33 
- total: 11873.00
```

The train scripts/train.sh.
The other modifications is in configure_finetunning.py and model/optimization.py.

## TO-DO
- Train for more epochs.
- Train the first 8 layers (1-8)
- From the fine tunned model, freeze the layers 16-23 and train layer 8-15.
