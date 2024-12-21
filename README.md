# Image Search and Indexing API

This project provides a FastAPI-based backend for performing image searches and indexing operations using a vector database. The API includes endpoints for searching images, indexing new images, and deleting indexed images. It leverages custom utility functions for vector database operations.

---

## Features
- **Image Search**: Search for images using a URL and retrieve the top-k most similar results.
- **Image Indexing**: Add new images to the vector database with metadata.
- **Image Deletion**: Remove indexed images from the vector database.

---

## Requirements

- Python 3.8 or higher
- FastAPI
- Dependencies listed in `requirements.txt`

---

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Osama-Abo-Bakr/Image-Search-Qdrant.git
   cd Image-Search-Qdrant
   ```

2. **Set up a virtual environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the FastAPI server**:
   ```bash
   uvicorn main:app --reload
   ```

---

## API Endpoints

### 1. **Image Search**
**Endpoint**: `/image-search`

**Method**: `POST`

**Description**: Perform a similarity search for images.

**Parameters**:
- `image_url` (string, required): URL of the image to search.
- `top_k` (integer, required): Number of top similar images to retrieve (1-10000).
- `threshold` (float, optional): Similarity threshold (0.0-1.0).
- `class_type` (string, required): Class of the image. Options: `All`, `class-a`, `class-b`.

**Response**:
Returns the top-k most similar images along with their metadata.

---

### 2. **Image Index or Delete**
**Endpoint**: `/image-index_or_delete`

**Method**: `POST`

**Description**: Add or delete images in the vector database.

**Parameters**:
- `image_id` (integer, required): Unique identifier for the image.
- `image_url` (string, optional): URL of the image to index (required for `upsert` case).
- `folder_path` (string, required): Path to the folder where the image is stored.
- `class_type` (string, optional): Class of the image. Options: `class-a`, `class-b` (required for `upsert` case).
- `case` (string, required): Operation type. Options: `upsert`, `delete`.

**Response**:
- For `upsert`: Confirmation of image indexing.
- For `delete`: Confirmation of image deletion.

---

## Project Structure

```
project/
├── main.py              # Main FastAPI application
├── utils.py             # Custom utility functions for vector database operations
├── downloads_images/    # Folder for temporarily storing searched images
├── indexing_downloads_images/ # Folder for temporarily storing indexed images
├── requirements.txt     # Python dependencies
```

---

## Usage Notes

1. **Utility Functions**: The following utility functions are required in `utils.py`:
   - `search_vectorDB`: Handles the vector database search functionality.
   - `index_vectorDB`: Adds images to the vector database.
   - `delete_vectorDB`: Removes images from the vector database.

2. **Folder Management**:
   - `downloads_images`: Used for storing images temporarily during search operations.
   - `indexing_downloads_images`: Used for storing images temporarily during indexing operations.

3. **Validation**:
   - Ensure `top_k` is between 1 and 10000.
   - Ensure `threshold` is a float between 0.0 and 1.0.
   - For `upsert`, `image_url` and `class_type` are mandatory.

---

## License
This project is licensed under the [MIT License](LICENSE).

---

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request.

---

## Contact
For any questions or issues, please contact [Your Name] at [osamaoabobakr12@gmail.com].