## How well does a GNN perform if an image's adjacency matrix is used for image classification?

Why this?
- I googled and couldn't find a straightforward answer
- From some previous literature review, it seems that images are often converted to graph like structures using superpixel-based methods, splitting images into grids and connecting them via k-nearest neighbor, generating and connecting image embeddings found via convolutional neural networks, using edge detection methods to split different components of an image and then connect them as sparse graph (Long et al. 2021, Vasudevan et al. 2023, Han et al. 2022, Zheng et al. 2022)
- I have performed ImageNet classification using AlexNet, so I can reuse some data processing code and the dataset
- How bad is it use just dense adjacency matrices for training?
 - My guess here is that adjacency matrices for similar objects (in images) will have similar graph structures/patterns, so the model should be able to distinguish between them
 - Both the training and the validation will be performed on the adjacency matrix representations of images
 - That said, I have never worked with images as graphs or graph-based models, so we will see how this turns out