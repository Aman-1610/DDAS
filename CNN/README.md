# CNN Model for Media Content Comparison

## Why Use CNN?
- **Purpose**: CNNs analyze patterns in images and videos to detect duplicates.
- **Relevance**: It identifies duplicate media files, even when resized, cropped, or slightly modified.

### Advantages:
- Effective for visual similarity detection.
- Works for image-based and video-based files.

---

## How to Use CNN in DDAS

### Step 1: Install Required Libraries
Add the TensorFlow dependency:
```xml
<dependency>
    <groupId>org.tensorflow</groupId>
    <artifactId>tensorflow</artifactId>
    <version>2.9.0</version>
</dependency>
```
### Step 2: Load Pre-trained Model
```xml
import org.tensorflow.SavedModelBundle;
SavedModelBundle model = SavedModelBundle.load("path_to_model");
```
### Step 3: Extract Feature Vectors
Preprocess media files and extract features:
``` xml
Tensor output = model.session().runner().feed("input_tensor", input).fetch("output_tensor").run().get(0);
