# Writing Blog Articles

The website has a Blog page that hosts articles written by COGS. Articles on the blog page are written in [Markdown](https://www.markdownguide.org/basic-syntax/), which lets you add headings, bold, italics, tables, images, code blocks, lists and blockquotes.

To add an article, follow the steps below:

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

1. Add an article to the `src/assets/blog-page-articles` folder.

    1. This article should end in `.md` and should have a descriptive filename.
    2. Make sure to place in the article in the correct folder based on it's year. If the folder doesn't exist, feel free to create it.
    3. After making the file, copy and paste the following metadata to the top of the file, and change it according to what your article is about:

        ```Markdown
        <!--
            Title: 			Article Title
            Description:	Description of the article
            Date:		    January 1, 2023
            Image:			assets/images/banner.png
            Authors: 		Alexander Xie, Alan Tong
            Tags:			Club, Article
        -->
        ```

        - `Title` - Title of the article
        - `Description` - Description of the article
        - `Date` - Date the article was written
        - `Image` - Image to use as the banner image on top of the article
        - `Authors` - Comma-separated list of authors for the article
        - `Tags` - Comma-separated list of tags for the article
            - There is no official list of tags, but please try to reuse existing tags listed in other articles when possible.

2. Run the following command to refresh the website's articles

    ```bash
    > py update_articles.py
    ```

3. Commit and push your changes to Github

    ```bash
    > git add .
    > git commit -m "Description of changes, etc."
    > git push
    ```
