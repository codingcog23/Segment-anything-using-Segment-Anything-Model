<h1 align="center">Segment Anything Model (SAM)</h1>

<img width="1206" alt="model_diagram" src="https://github.com/codingcog23/Segment-anything-using-Segment-Anything-Model/assets/134972060/e940c29e-1f6c-45bc-bd1f-f26b72091bc3">


The Segment Anything Model (SAM) produces high-quality object masks from input prompts such as points or boxes, enabling the generation of masks for all objects in an image. Trained on a dataset of 11 million images and 1.1 billion masks, SAM exhibits strong zero-shot performance on a variety of segmentation tasks.

<img width="702" alt="masks1" src="https://github.com/codingcog23/Segment-anything-using-Segment-Anything-Model/assets/134972060/f8835d11-a708-45da-8a54-bd4f8a924b87">
<img width="702" alt="masks2" src="https://github.com/codingcog23/Segment-anything-using-Segment-Anything-Model/assets/134972060/d2d2f17f-4ad7-4a6c-b16c-a4ab6a63cd44">

<h2 align="center">Installation</h2>

To use the code, ensure that you have Python version 3.8 or higher, along with the following dependencies: PyTorch (version 1.7 or higher) and TorchVision (version 0.8 or higher). We strongly recommend installing both PyTorch and TorchVision with CUDA support.

To install the Segment Anything Model, use the following command:

```
pip install git+https://github.com/facebookresearch/segment-anything.git

Alternatively, you can clone the repository locally and install it with:

git clone git@github.com:facebookresearch/segment-anything.git
cd segment-anything; pip install -e .
```

Additional dependencies required for mask post-processing, saving masks in COCO format, example notebooks, and exporting the model in ONNX format can be installed using the following command:

```
pip install opencv-python pycocotools matplotlib onnxruntime onnx

```

<h2 align="center">Getting Started</h2>

First download a model checkpoint. Then the model can be used in just a few lines to get masks from a given prompt:

```
from segment_anything import SamPredictor, sam_model_registry
sam = sam_model_registry["<model_type>"](checkpoint="<path/to/checkpoint>")
predictor = SamPredictor(sam)
predictor.set_image(<your_image>)
masks, _, _ = predictor.predict(<input_prompts>)

```
or generate masks for an entire image:

```
from segment_anything import SamAutomaticMaskGenerator, sam_model_registry
sam = sam_model_registry["<model_type>"](checkpoint="<path/to/checkpoint>")
mask_generator = SamAutomaticMaskGenerator(sam)
masks = mask_generator.generate(<your_image>)

```
Additionally, masks can be generated for images from the command line:
```
python scripts/amg.py --checkpoint <path/to/checkpoint> --model-type <model_type> --input <image_or_folder> --output <path/to/output>

```
See the examples notebooks on using SAM with prompts and automatically generating masks for more details.
<h2 align="center">ONNX Export</h2>

SAM's lightweight mask decoder can be exported to ONNX format so that it can be run in any environment that supports ONNX runtime, such as in-browser as showcased in the demo. Export the model with

```
python scripts/export_onnx_model.py --checkpoint <path/to/checkpoint> --model-type <model_type> --output <path/to/output>

```
## Results
![Mask](https://github.com/codingcog23/Segment-anything-using-Segment-Anything-Model/assets/134972060/99251a4d-9d87-4037-8dc1-d6ec569b2d01)

![segment-anything-model-paper](https://github.com/codingcog23/Segment-anything-using-Segment-Anything-Model/assets/134972060/aa243627-e27e-47c9-88bb-9662c75a7a21)

See the example notebook for details on how to combine image preprocessing via SAM's backbone with mask prediction using the ONNX model.
