## How to install this package
I made this file because I am pretty code illiterate and serves as a reminder 

1. Make sure you have anaconda installed on your machine
2. Use conda env create -f BRepNet_environment.yml to isntall all dependencies
3. Jupyter notebook for VSCode or similar works well for the visualisation
4. Download the raw data using:
        cd /path/to/where_you_keep_data/
        curl https://fusion-360-gallery-dataset.s3-us-west-2.amazonaws.com/segmentation/s2.0.0/s2.0.0.zip -o s2.0.0.zip
        unzip s2.0.0.zip
5. Process the data locally using this code in Anaconda powershell(make sure you have activated the conda environment you created using the .yml file) (takes 2-3 hours depending on your device)
        python -m pipeline.quickstart --dataset_dir /path/to/where_you_keep_data/ --num_workers 10
        we set num_workers to 10 - seems to perform the best locally
6. Train the model (takes between 5 and 10 hours depending on your GPU):
        python -m train.train --dataset_file /path/to/where_you_keep_data/s2.0.0/processed/dataset.json \
        --dataset_dir /path/to/where_you_keep_data/s2.0.0/processed/ \
        --max_epochs 200 \
        --num_workers=10 \
        --gpus=1
7. Train.train will save the best version of your training model under:
        /logs/../../checkpoints/filename.ckpt
8. Alternatively use the pretrained model provided by Autodesk:
        ../example_files/pretrained_models/pretrained_s2.0.0_extended_step_uv_net_features_0816_183419.ckpt

9. You can now run the scripts under ../notebooks/filename.ipynb
        - BRepNET_Walkthrough.ipynb --> this notebook is a collection of tools and implementation of the segmentation model.