# Optimizing Images
### The problem
- For images like banner.png we initially had a version that had a width of about 1500px
- We know that we use this picture inside a container that is constraint to max-width==1140px
    - On mobile the picture fills the entire width of the container, but mobiles are only up to 768px
    - On Desktop the image fills only 1 half of the container, so 570px.
    - If we have a high-density screens that have more physical than logical pixels, we want to also support 2x and 3x versions of an image.
- The max width of the picture is therefore 570px for 1x and 1140px for 2x. We cannot support 3x, because the picture was initially not large enough.

### What I did:
1. Open the image in Gimp and resize it to 1140px and save it as banner@2x.png
2. Resize the image to 570px and save it as banner.png
3. Go to cloudconvert.com and convert those images to the WEBP format to make it even smaller
4. Reference the picture in the HTML-markup. Make sure to give an alternate in the PNG-format in case the browser does not support WEBP:
```html
    <picture>
        <source
        type="image/webp"
        srcset="../images/banner.webp 1x, ../images/banner@2x.webp 2x"
        />
        <source
        type="image/webp"
        srcset="../images/banner.png 1x, ../images/banner@2x.png 2x"
        />
        <img class="hero__image" src="../images/banner.png" alt="" />
    </picture>
```