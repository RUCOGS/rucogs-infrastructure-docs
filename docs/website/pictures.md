# Uploading Pictures

The website has a picture page that display pictures of past events at COGS. To upload pictures to this page, follow the steps below:

## Prerequisites

1. Make sure you have [Python](https://www.python.org/downloads/) installed on your computer.
2. Make sure you have [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) installed on your computer.
3. Clone the [website GitHub repository](https://github.com/rucogs/rucogs.github.io) locally if you don't have it already

    ```bash
    > git clone https://github.com/rucogs/rucogs.github.io
    ```

4. Inside the repository folder, install the python packages using

    ```bash
    > pip install -r requirements.txt
    ```

## Steps

1. Upload pictures to the `src/assets/pictures-page-images` folder

    - Make sure to place in the image in the correct folder based on it's year and then semester
    - If the folder doesn't exist, feel free to create it.

2. Run the following command. This will add the images to the website as well as generate preview thumbnails for the images

    ```bash
    > py update_images.py
    ```

3. Commit and push your changes to GitHub

    ```bash
    > git add .
    > git commit -m "Description of changes, etc."
    > git push
    ```
