
# ComfyUI Node Creation

## 1. Node Definition (Python)

**Create a Python class:** The class is the blueprint for your custom node. It defines the structure, logic, and behavior of your node.

**Example:**

```python
class MyCoolNode:
```

**Define INPUT_TYPES:** Specify required inputs as a dictionary, using tuples for type and options.

**Example:**

```python
@classmethod
def INPUT_TYPES(cls):
    inputs = {
        "required": { # Mandatory inputs
            "input1": ("IMAGE", {"default": None}), 
            # "input2": ("INT", {"min": 0, "max": 100}), 
        },
        "optional": { # Optional inputs
            "input3": ("STRING", {"default": "Hello"}),
        },
        "hidden": { # Hidden inputs (for internal use)
            "internal_data": ("INT", {"default": 0}), 
        }
    }
    return inputs
```

**Explanation:**
- `@classmethod:` This decorator indicates that the INPUT_TYPES function is a class method, meaning it can be called directly on the class (e.g., MyCoolNode.INPUT_TYPES()) rather than an instance of the class.
- `inputs Dictionary:` Contains different types of input parameters.
- `cls:` The `cls` argument in class methods refers to the class itself. It's used to access class attributes and methods within the class method.
- `"required:"` Mandatory inputs that must be provided when using the node.
- `"optional:"` Inputs that are not required but can be provided for customization.
- `"hidden:"` Inputs that are not visible in the ComfyUI interface (often used for internal node logic).
- `Tuples:` Each input value is defined as a tuple: ("data_type", {"options"}).
- `data_type:` Specifies the type of data expected (e.g., "IMAGE", "INT", "STRING").
- `{"options"}:` A dictionary providing additional settings for the input. Common options include:
  - `default:` Sets a default value for the input.
  - `min:` Specifies the minimum allowed value (for numeric inputs).
  - `max:` Specifies the maximum allowed value (for numeric inputs).

**Core Data Types:**
- `INT:` Represents an integer number.
- `FLOAT:` Represents a floating-point number (decimal value).
- `STRING:` A sequence of characters, useful for text, file paths, etc.
- `BOOL:` A boolean value (True or False).
- `IMAGE:` Represents a single image object. This is the foundation for working with images in ComfyUI.
- `IMAGE_BATCH:` A collection of image objects, useful for processing multiple images at once.
- `MASK:` A single image mask. Masks are used to define specific areas of an image for processing.
- `MASK_BATCH:` A collection of image masks.

**Advanced Data Types:**
- `CONTROL:` This is used for nodes that represent user-controllable settings like sliders, checkboxes, etc.
- `SAMPLER:` A sampler object, often used for controlling image generation processes.
- `MODEL:` Represents a model, such as a Stable Diffusion model.
- `AUDIO:` Represents audio data. This is relatively new in ComfyUI and allows for working with audio processing.
- `VIDEO:` Represents video data. ComfyUI can handle video generation and editing.
- `LIST:` A list of values (various types allowed within). Can be helpful for organizing and iterating through data.
- `DICT:` A dictionary of key-value pairs. Provides flexibility for storing and retrieving information.

**Considerations:**
- `Custom Types:` While the above are common, ComfyUI is very flexible. You can define custom types within your own nodes if you need more specialized handling.

**Define CATEGORY:**
- `Purpose:` Assigns a category for your node in ComfyUI's node browser, making it easier to find.
- **Example:**

```python
CATEGORY = "My Custom Nodes"
```

**Define RETURN_TYPES:** List the types of outputs the node will produce. Same possibilities as INPUT_TYPES.

**Example:**

```python
RETURN_TYPES = ("IMAGE",) # Returns a single image
```

**Define RETURN_NAMES:** Provide names for the output values (e.g., "RETURN VALUE").

**Example:**

```python
RETURN_NAMES = ("Processed Image", "Image Description") # Names for the outputs
```

**Define FUNCTION:** Specify the function name responsible for node logic.

**Example:**

```python
def process_image(self, input_image): # Function definition
```

**Define CATEGORY:** Assign a category for your node in ComfyUI's node browser. The category is what shows up in the node menu.

**Example:**

```python
CATEGORY = "My Custom Nodes" # Category for the node browser
```

## 2. Node Logic Implementation (Python)

- **Create a function with the name specified in FUNCTION:** This function will receive input values and process them.
- **Implement the node's core logic:** Perform calculations, handle data, or interact with external sources.
- **Return output values:** Ensure the function returns a tuple of values matching the RETURN_TYPES.

## 3. Node Integration (Python)

- **Create a `__init__.py` file:** This file registers your node with ComfyUI.
- **Import your node class:** Import the Python class you defined earlier.
- **Define NODE_CLASS_MAPPINGS:**

**Example**

```python
from .MyCoolNode import MyCoolNodeClass # Import your node class

NODE_CLASS_MAPPINGS = {
    "MyCoolNode": MyCoolNodeClass # Map the identifier to the class
}
```

- **Define NODE_DISPLAY_NAMES_MAPPINGS:** Map the identifier to a user-friendly display name.
- **Export mappings:** Use `__all__` to make the mappings available for ComfyUI to discover.

**Example:**

```python
__all__ = ['NODE_CLASS_MAPPINGS', 'NODE_DISPLAY_NAME_MAPPINGS'] # Export mappings
```
