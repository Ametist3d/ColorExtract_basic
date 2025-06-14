# ColorExtract basic

A powerful Python tool that combines object detection, image segmentation, and color analysis to provide comprehensive insights about images. The analyzer uses YOLOv8 for object detection and K-means clustering for dominant color extraction.

## Features

- **Object Detection & Segmentation**: Uses YOLOv8 to detect and segment objects in images
- **Dominant Color Extraction**: Employs K-means clustering to identify the most prominent colors
- **Mask-based Color Analysis**: Extracts colors specifically from detected object regions
- **Color Classification**: Converts RGB values to human-readable color names
- **Command-line Interface**: Easy-to-use CLI for batch processing and automation

## Installation

1. Clone this repository:
```bash
git clone https://github.com/Ametist3d/ColorExtract_basic.git
cd ColorExtract_basic
```

2. Install the required dependencies:
```bash
pip install -r requirements.txt
```

3. The YOLOv8 model will be automatically downloaded on first use.

## Usage

### Basic Usage

Analyze an image with default settings (5 dominant colors):
```bash
python simple_color-obj_detection_seg.py --image_path path/to/your/image.jpg
```

### Advanced Usage

Specify the number of colors to extract:
```bash
python simple_color-obj_detection_seg.py --image_path path/to/your/image.jpg --n_colors 8
```

### Command-line Arguments

- `--image_path`: Path to the image file (required)
- `--n_colors`: Number of dominant colors to extract (default: 5)

## Example Output

```
Analyzing image: sample_image.jpg
Detecting objects...
Using YOLOv8 for object detection
Extracting colors from person mask...

==================================================
DOMINANT COLORS:
==================================================
1. blue - RGB(45, 87, 132) (28.5%)
2. white - RGB(245, 242, 238) (22.1%)
3. dark gray - RGB(72, 69, 66) (18.3%)
4. brown - RGB(156, 98, 67) (16.8%)
5. black - RGB(32, 28, 25) (14.3%)

==================================================
OBJECT DETECTION:
==================================================
- person (89.2% confidence)
- backpack (76.4% confidence)
- handbag (68.1% confidence)
```

## How It Works

1. **Object Detection**: The analyzer uses YOLOv8n-seg (nano segmentation model) to detect objects and generate segmentation masks
2. **Color Extraction**: 
   - If a segmentation mask is available, colors are extracted only from the masked region
   - Otherwise, colors are extracted from the entire image
   - K-means clustering groups similar colors and identifies the most dominant ones
3. **Color Classification**: RGB values are converted to human-readable color names using a rule-based system

## Supported Image Formats

- JPEG (.jpg, .jpeg)
- PNG (.png)
- BMP (.bmp)
- TIFF (.tiff)
- And other formats supported by PIL

## Requirements

- Python 3.7+
- CUDA-compatible GPU (optional, for faster inference)

## Dependencies

See `requirements.txt` for the complete list of dependencies.

## Technical Details

### Color Classification

The analyzer uses a rule-based approach to classify RGB values into color names:
- **Primary colors**: Red, Green, Blue
- **Secondary colors**: Yellow, Orange, Purple, Cyan
- **Neutral colors**: Black, White, Gray variations
- **Earth tones**: Brown
- **Mixed colors**: Complex combinations

### Object Detection Classes

YOLOv8 can detect 80 different object classes from the COCO dataset, including:
- People and animals
- Vehicles
- Household items
- Food items
- Sports equipment
- And many more

## Performance Considerations

- **Model Size**: Uses YOLOv8n (nano) for balance between speed and accuracy
- **Memory Usage**: Large images are processed efficiently using numpy operations
- **GPU Acceleration**: Automatically uses GPU if available with CUDA

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Ultralytics](https://github.com/ultralytics/ultralytics) for the YOLOv8 implementation
- [scikit-learn](https://scikit-learn.org/) for K-means clustering
- [PIL/Pillow](https://pillow.readthedocs.io/) for image processing

## Troubleshooting

### Common Issues

1. **Model Download Error**: Ensure you have an internet connection for the initial YOLOv8 model download
2. **Memory Error**: For very large images, consider resizing them before analysis
3. **OpenCV Error**: Make sure opencv-python is properly installed

### Performance Tips

- Use smaller images (< 2000px) for faster processing
- Enable GPU acceleration by installing the CUDA-enabled version of PyTorch
- Reduce the number of colors (`--n_colors`) for faster K-means clustering

## Contact

For questions, suggestions, or issues, please open an issue on GitHub.
