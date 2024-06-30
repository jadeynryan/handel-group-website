## Repo contents

-   **README.md**: content shown in GitHub repository
-   **\_freeze**: [storage for computational results of documents](https://quarto.org/docs/projects/code-execution.html#freeze)
-   **\_quarto.yml**: [config file](https://quarto.org/docs/websites/#config-file) for site metadata, website options ([navigation](https://quarto.org/docs/websites/website-navigation.html), [Google Analytics tag](https://quarto.org/docs/websites/website-tools.html#google-analytics)), and [html options](https://quarto.org/docs/output-formats/html-basics.html)
-   **\_site**: rendered site files to be copied to UGA server
-   **andreas-handel.qmd**: about page with Andreas' bio
-   **custom-theme.scss**: SCSS and CSS for styling website
-   **handel-group-website.Rproj**: RStudio project file
-   **images**: header image, logo, and subfolders for images for people & project pages
-   **index.qmd**: config/content for home page
-   **news**: folder for news/group updates (each post should be a subfolder)
-   **news.qmd**: config for news page
-   **notes-and-how-to.md**: this help doc
-   **opportunities.qmd**: config/content for opportunities page
-   **people-current.yml**: content for Group Members page - list **current** members here
-   **people-former.yml**: content for Group Members page - list **former** members here
-   **people.ejs**: [custom EJS template](https://quarto.org/docs/websites/website-listings-custom.html#listing-templates) to generate HTML for the Group Members page
-   **people.qmd**: config/content for people page
-   **projects.qmd**: config/content for projects page
-   **projects.yml**: content for projects page
-   **publications.qmd**: config/content for publications page
-   **resources.qmd**: config/content for resources page
-   **software**: zip files for software linked for download in the resources page

## How to update

### Home page

Edit `index.qmd`.

### News

Copy an existing subfolder of `/news` and modify as needed. `news.qmd` will automatically include this new post as an entry on the News page's listing.

### Publications

Edit `publications.qmd`.

### Projects

1.  Add an image to `images/projects/`.
2.  Edit `projects.qmd`.
    -   Copy a card div (starts with `::: {.card}` and ends with `:::`)
    -   Modify the card title, image, and description. Note the title and image use spans to assign the CSS class `.card-title` or `.card-image-left` (floats the image to the left) or `.card-image-right` (floats the image to the right). For more info, see the [Quarto Docs on divs and spans](https://quarto.org/docs/authoring/markdown-basics.html#sec-divs-and-spans). These CSS classes are defined in `custom-theme.scss`.
    -   By default, the image takes 50% and the text takes 50% of the card. Override this by setting the image width:
        ```
        ::: {.card}
        
        [Title]{.card-title}
        
        ![](images/image.png){.card-image-left width="30%"}
        
        Text here, taking up 70% of page.
        :::
        ```
### Group members

**To change a current member to a former member:**

1.  In `people-current.yml`, copy the entry and paste into `people-former.yml`.
2.  Add the final year in the group to the `years:` field.

**To add a new member:**

1.  Add their photo to `images/people`.
2.  In `people-current.yml`, copy the entry and modify as needed.
    -   If they did not provide a photo, you can use `images/people/avatar.jpg` for the `image` field.

#### Custom listing

`people.qmd` uses a [custom listing](#0) template (`people.ejs`) that generates the HTML of the Group Members page using the content from `people-current.yml` and `people-former.yml`. The `.yml` files (edit these) pass the info for each person to the `.ejs` file (don't edit this, unless new fields are needed). The current fields used in the template are: name, image, role, and links. The only fields that are required are name and image.

##### Andreas' bio page

This page is currently live but not accessible through any links. If you change your mind and want this page, uncomment out the markdown at the top of `people.qmd` and comment out your entry in `people-current.yml`. Edit `andreas-handel.qmd`. This page uses and modifies the [Trestles about template](https://quarto.org/docs/websites/website-about.html).

#### Links/icons

`people.ejs` loads and uses the [iconify design](https://icon-sets.iconify.design/) javascript package so almost all icon packages are available (e.g., [Font Awesome Brands](https://icon-sets.iconify.design/fa6-brands/?list=recent), [Academicons](https://icon-sets.iconify.design/academicons/?keyword=aca)) using the syntax `academicons:google-scholar` under the `icon:` field.

`people.qmd` and `andreas-handel.qmd` use the Quarto shortcode syntax to use the [`iconify extension`](https://github.com/mcanouil/quarto-iconify).

The reason the syntax is different between the `people-current/former.yml` and the `.qmd` files is that the `icon` field in the `.yml` files are directly embedded in the HTML of the website through `people.ejs`. Conversely, the `.qmd` files use a [shortcode](https://quarto.org/docs/extensions/creating.html) which is a separate markdown directive.

### Resources

Edit `resources.qmd`.

To add new software zip files, add them to the `software` folder.

### Opportunities

Edit `opportunities.qmd`.

### Style/theme

To change the base theme from flatly, edit `_quarto.yml` → `format:` \> `html:` \> `theme:`. For more info on HTML theme options, see these [Quarto Docs](https://quarto.org/docs/output-formats/html-themes.html).

To change the fonts or colors, or further customize the appearance, edit `custom-theme.scss`. Read more on [Quarto custom theming](https://quarto.org/docs/output-formats/html-themes-more.html) or see the full [flatly.scss theme](https://github.com/quarto-dev/quarto-cli/blob/main/src/resources/formats/html/bootstrap/themes/flatly.scss) to see more variables to customize.

### Website configuration or pages

To update the website title, description, favicon, navigation, site URL, repo URL, footer, etc., edit the `_quarto.yml`.

To add/remove a page, change the `navbar:` \> `left:` fields. Add/remove the corresponding `.qmd` file.

## Preview website

In the `Terminal`, run `quarto preview`. Changes made to most\* files will cause automatic re-rendering and the preview will update.

\*Sometimes `_quarto.yml`, `people-current.yml`, `people-former.yml`, and `people.ejs` will not automatically re-render and update the preview. In these cases, make a change to a `.qmd` file (add a space or line break somewhere, and then delete).

## Render website

In the `Terminal`, run `quarto render`. This will render the website files into the `_site` folder, which can be copied to the UGA server.
