# Object Detection annotation tool for Google Colab
This tool can be used in Jupyter Labs running in local enviornments also,

Object Detection annotation tool to use in Google Colab and Local Jupyter notebooks.

### How to use
- First Clone this repo or download as zip
  ```bash
  git clone https://github.com/theroyakash/GoogleColabAnnotationTool.git
  ```
- Now import the packages
  ```python
  from GoogleColabAnnotationTool.annotate import annotate
  ```
- Transform all images into numpy arrays
  ```python
  def load_image_into_numpy_array(path):
      """
      Load an image from file into a numpy array.
      Puts image into numpy array to feed into tensorflow graph.
      Note that by convention we put it into a numpy array with shape
      (height, width, channels), where channels=3 for RGB.

          Args:
              - ``path`` (str): a file path.

          Returns:
              - ``uint8`` numpy array with shape ``(img_height, img_width, 3)``
      """
      img_data = tf.io.gfile.GFile(path, 'rb').read()
      image = Image.open(BytesIO(img_data))
    
      (im_width, im_height) = image.size

      return np.array(image.getdata()).reshape((im_height, im_width, 3)).astype(np.uint8)
    
  train_image_dir = '/contents/image_path/'
  train_images_np = []
  for i in range(1, 6):
      image_path = os.path.join(train_image_dir, 'image_data' + str(i) + '.jpg')
      train_images_np.append(load_image_into_numpy_array(image_path))
  ```
- Now with all the images converted to numpy arrays run the annotation tool
  ```python
  bounding_boxes = []
  annotate(train_images_np, box_storage_pointer=bounding_boxes)
  ```
