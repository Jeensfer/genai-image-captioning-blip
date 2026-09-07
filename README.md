## Prototype Development for Image Captioning Using the BLIP Model and Gradio Framework
#### Name: Jeensfer Jo
#### Reg No: 212225240058
### AIM:
To design and deploy a prototype application for image captioning by utilizing the BLIP image-captioning model and integrating it with the Gradio UI framework for user interaction and evaluation.

### PROBLEM STATEMENT:
The project aims to develop an image captioning application that automatically generates meaningful descriptions for uploaded images. It uses the BLIP model to understand the visual content and convert it into natural language. The application is developed using the Gradio framework to provide a simple and interactive interface. Users can upload an image and instantly view its generated caption. This demonstrates how AI can combine computer vision and natural language processing for image understanding.

#### STEP 1:

Configure the Hugging Face API and load the required environment variables and libraries for image processing.

#### STEP 2:

Convert the uploaded image into Base64 format and send it to the Hugging Face Image-to-Text model to generate a caption.

#### STEP 3:

Create a Gradio interface that allows users to upload an image and displays the generated caption.

### PROGRAM:
```py
import os
from PIL import Image
import gradio as gr
from google import genai

# 1. Set Gemini API Key
api_key = "API_KEY"
client = genai.Client(api_key=api_key)

# 2. Define Image Captioning Function
def captioner(image):
    if image is None:
        return "Please upload an image."
    try:
        prompt = "Write a short, descriptive caption for this image."
        response = client.models.generate_content(
            model='gemini-2.5-flash',
            contents=[image, prompt]
        )
        return response.text
    except Exception as e:
        return f"Error: {str(e)}"

# 3. Build & Launch Gradio Interface
gr.close_all()

demo = gr.Interface(
    fn=captioner,
    inputs=[gr.Image(label="Upload image", type="pil")],
    outputs=[gr.Textbox(label="Caption", lines=3)],
    title="Image Captioning with Gemini",
    description="Upload an image to generate a descriptive caption using Gemini 2.5 Flash.",
    flagging_mode="never"
)

# Launches inline inside your Jupyter Notebook
demo.launch()
```
### OUTPUT:
<img width="1011" height="496" alt="image" src="https://github.com/user-attachments/assets/b4198632-84aa-4857-8b9c-af612bf01b12" />

### RESULT:
The Image Captioning application successfully generates an accurate text description for the uploaded image and displays the generated caption through the Gradio interface.
