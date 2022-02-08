![Banner](./2021/assets/HerbariumChallengeBanner.png)



[![Herbarium2021.png](https://i.postimg.cc/htpxH99f/Herbarium2021.png)](https://postimg.cc/BjPXFP70)


# Description 

*The Herbarium 2022: Flora of North America* is a part of a project of the [New York Botanical Garden](https://www.nybg.org/) funded by the [National Science Foundation](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2054684&HistoricalAwards=false) to build tools to identify novel plant species around the world. The dataset strives to represent all known vascular plant taxa in North America, using images gathered from 60 different botanical institutions around the world. <br>

*The Herbarium 2022: Flora of North America* dataset comprises **1.05 M images** of **15,500 vascular plants**, which constitute more than **90% of the taxa** documented in North America. We used the comprehensive Checklist of the [Vascular Plants of the Americas (VPA)](https://doi.org/10.1126/science.aao0398) produced by [Missouri Botanical Garden](https://www.missouribotanicalgarden.org/) and aligned the taxonomic names to [The World Checklist of Vascular Plants (WCVP)](https://www.nature.com/articles/s41597-021-00997-6) from the [Royal Botanical Garden Kew](https://www.kew.org/). Our dataset is constrained to include only **vascular land plants** (lycophytes, ferns, gymnosperms, and flowering plants). <br>

Our dataset has a long-tail distribution. **The number of images per taxon** is as few as seven and as many as 100 images. Although more images are available, we capped the maximum number in an attempt to ensure sufficient but manageable training data size for competition participants. <br>


# Background

There are approximately **3,000 herbaria worldwide** and they are massive repositories of plant diversity data. These collections not only represent a vast amount of plant diversity, but since herbarium collections include specimens dating back hundreds of years, they provide snapshots of plant diversity through time. Plant specimens are maintained in herbaria by pressing, drying, and mounting them; a specimen collected nearly two hundred years ago by Darwin looks much the same as one collected a month ago by an NYBG botanist. All specimens not only maintain their morphological features but also include collection dates and locations, their reproductive state, and the name of the person who collected the specimen. This information, multiplied by millions of plant collections, provides the framework for understanding plant diversity on a massive scale and learning how it has changed over time. 


There are approximately 400,000 known vascular plant taxa with an estimated 80,000 still to be discovered. Herbaria contain an overwhelming amount of unnamed and new specimens, and with the threats of climate change, we need new tools to quicken the pace of species discovery. This is more pressing today as a United Nations report indicates that more than one million species are at risk of extinction, and amid this dire prediction is a recent estimate that suggests plants are disappearing more quickly than animals. 


In botany, a **‘flora’ is a complete account of the plants found in a geographic region**. The dichotomous keys and detailed descriptions of diagnostic morphological features contained within a flora are used by botanists to determine which names to apply to plant specimens. **This year's competition dataset aims to encapsulate the flora of North America so that we can test the capability of artificial intelligence to replicate this traditional tool** —a crucial first step to harnessing AI’s potential botanical applications.    


# About

This is an FGVC competition hosted as part of the [FGVC9](https://sites.google.com/view/fgvc9) workshop at [CVPR 2022](http://cvpr2022.thecvf.com/) and sponsored by [NYBG](https://www.nybg.org/).

Details of this competition are mirrored on the [github](https://github.com/visipedia/herbarium_comp) page. Please post in the forum or open an issue if you have any questions or problems with the dataset.

# Acknowledgements

The images are provided by the [New York Botanical Garden](https://www.nybg.org/) and 60 other institutions around the world. 
![h22-banner](https://i.postimg.cc/g0DJMF52/output.png)


## Kaggle Competition

The leaderboard is being hosted on Kaggle ([challenge page](https://www.kaggle.com/c/herbarium-2022-fgvc9)).

### Dates
|||
|------|---------------|
Competition Starts|Feb 14 , 2022|
Entry Deadline|April 4, 2022|
Team Merger Deadline|May 3, 2022|
Final Submission Deadline|May 26, 2022|

### Evaluation
Competition submissions are evaluated using the [macro F1 score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html).

F1 is calculated as follows:

<img src="https://render.githubusercontent.com/render/math?math=F_1 = 2 * \frac{precision * recall}{precision %2B recall}">

where:

<img src="https://render.githubusercontent.com/render/math?math=precision = \frac{TP}{TP %2B FP}">

<img src="https://render.githubusercontent.com/render/math?math=recall = \frac{TP}{TP %2B FN}">

In "macro" F1 a separate F1 score is calculated for each `species` value and then averaged.

### Submission File Format

For each image `Id`, you should predict the image label in the `Predicted` column. The submission file should have the following format:

    Id,Predicted
    0,0
    1,27
    2,42
    ...

## Data 

The dataset is hosted on [Kaggle](https://www.kaggle.com/c/herbarium-2021-fgvc9/data).

The training and test set contain images of herbarium specimens from close to 65,000 species of vascular plants. Each image contains exactly one specimen. The text labels on the specimen images have been blurred to remove category information in the image.

The data has been approximately split 80%/20% for training/test. Each category has at least 1 instance in both the training and test datasets. Note that the test set distribution is slightly different from the training set distribution. The training set contains species with hundreds of examples, but the test set has the number of examples per species capped at a maximum of 10.

### Dataset Format
Each image has different image dimensions, with a maximum of 1000 pixels in the larger dimension. These have been resized from the original image resolution. All images are in JPEG format.

This dataset uses the [COCO dataset format](https://cocodataset.org/#format-data) with additional annotation fields. In addition to the species category labels, we also provide region and supercategory information.

The training set metadata (`train/metadata.json`) and test set metadata (`test/metadata.json`) are JSON files in the format below. Naturally, the test set metadata file omits the "annotations", "categories," and "regions" elements.

    { 
      "annotations" : [annotation], 
      "categories" : [category],
      "images" : [image],
      "info" : info,
      "licenses": [license],
      "institutions": [institution]
    }
    
    info {
      "year" : int,
      "version" : str,
      "url": str,
      "description" : str,
      "contributor" : str,
      "date_created" : datetime
    }

    image {
      "id" : int,
      "width" : int,
      "height" : int,
      "file_name" : str,
      "license" : int
    }

    annotation {
      "id": int,
      "image_id": int,
      "category_id": int,
      # Institution that provided this specimen.
      "institution_id": int
    }

    category {
      "id" : int,
      # Species name
      "name" : str,
      # We also provide the super-categories for each species.
      "family": str,
      "order": str
    }

    institution {
      "id": int
      "name": str
    }

    license {
      "id": int,
      "name": str,
      "url": str
    }


The training set images are organized in subfolders `train/images/<subfolder1>/<subfolder2>/<image id>.jpg`, where `<subfolder1>` combined with `<subfolder2>` corresponds to the `category_id`. For example, a training image with an `image_id` of `1104517` and a `category_id` of `00001`, can be found at `train/images/000/01/1104517.jpg`. 


The test set images are organized in subfolders `test/images/<subfolder>/<image id>.jpg`, where `<subfolder>` corresponds to the integer division of the `image_id` by 1000. For example, a test image with and `image_id` of `8005`, can be found at `test/images/008/8005.jpg`. 

### Terms of Use
* You will use the data only for non-commercial research and educational purposes.
* You will NOT distribute the images.

## About

This is an FGVC competition hosted as part of the [FGVC9](https://sites.google.com/view/fgvc9) workshop at [CVPR 2022](http://cvpr2022.thecvf.com/) and sponsored by [NYBG](https://www.nybg.org/).

Please post in the Kaggle forum or open an issue if you have any questions or problems with the dataset.

