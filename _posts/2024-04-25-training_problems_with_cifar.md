# Discovering some strange fastai *problems* (bugs? misinterpretations? me doing something wrong?) 

## Issue Number 1
This was a little issue in using a testing dataset I ran into while doing the CIFAR10[^1] question for Assignment 2 of ELEC4630.


### What I wanted to do
Essentially, the established way to load test_trainers in fastai is something like the following, as found [here](https://forums.fast.ai/t/fastai-v2-recipes-tips-and-tricks-wiki/64486/3?page=2).

    dls = learn.dls.test_dl(get_image_files(path))
    _,_,losses = learn.get_preds(dl=dls, with_input=False, with_loss=True, with_decoded=False,
                                         with_preds=False, with_targs=False, act=None)
    interp = ClassificationInterpretation(learn, dls, losses)

However, I **consistently** got the following error running that code, despite all my best efforts to circumnavigate it

    File ~/Documents/Fourth Year/ELEC4630/.venv/lib/python3.11/site-packages/fastai/learner.py:176, in Learner._call_one(self, event_name)
        174 def _call_one(self, event_name):
        175     if not hasattr(event, event_name): raise Exception(f'missing {event_name}')
    --> 176     for cb in self.cbs.sorted('order'): cb(event_name)
    
    File ~/Documents/Fourth Year/ELEC4630/.venv/lib/python3.11/site-packages/fastai/callback/core.py:62, in Callback.__call__(self, event_name)
    ...
        619     if isinstance(x,dict):
        620         key = list(x.keys())[idx] if isinstance(idx, int) else idx
    
    IndexError: Exception occured in `GatherPredsCallback` when calling event `after_batch`:
    	tuple index out of range

## What I had to do
Instead, I needed to load it in the same manner as the DataBlock dataloader, as below. 

    path = Path('cifar10_testing')
    
    db_test = DataBlock(
        blocks=(ImageBlock, CategoryBlock), 
        get_items=get_image_files, 
        splitter=RandomSplitter(valid_pct=0.2, seed=42),
        get_y=parent_label,
        item_tfms=[Resize(192, method='squish')]
    )
    dls_test = db.dataloaders(path)

Though seemingly equivalent, it seems weird that that specific functionality, recommended in fastai forums, is not supported. 

## Issue Number Two
This one was seriously weird. Essentially, once I got the testing batch working, the images were displaying very strangely. See below. 

![](/images/weird_images.png "weird distorted images")

To fit it, I had to *train a model on the testing set itself* despite not using it at all. Super weird. I think there's something either buggy in fastai (or something I'm missing) that's making the images not be processed/be over processed and then corrected at the end of training? It needs further digging. 

## Footnotes

[^1]: The [CIFAR10 Dataset](https://www.kaggle.com/c/cifar-10/) is a very popular dataset for image classification.
