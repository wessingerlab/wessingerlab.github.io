### Website created using advice from many websites including:

https://www.emilyzabor.com/tutorials/rmarkdown_websites_tutorial.html#r_markdown_website_basics (info on getting the basics of the website created)

https://www.w3.org/wiki/CSS_absolute_and_fixed_positioning?source=post_page---------------------------#:~:text=Whereas%20the%20position%20and%20dimensions,or%20the%20paper's%20page%20box (info on css positioning of elements)

https://www.geeksforgeeks.org/css-text-formatting/ (information on what you can do with css to style elements, mostly for the style.css but also for the css code blocks within the .rmds)


### Things to know: 

if you are trying to google how to do something new that I have not left any notes for and not coming up with good results often times adding "github pages with rmd" to the end of your search will lead you to more informative answers

each .Rmd is "knit" to create the corresponding .html which are what makes up the actual website -> when making changes you can check what it will look like individually by clicking "knit" in the top of the .Rmd or what all of them together will look like by clicking the Build Website button under the Build tab in the environment screen

the .Rmd reads from the top down so if you want an image to occur alongside a bit of text, you need to have the code for the image BEFORE the text (assumes you did not format the image to take up the whole screen)

when the website is built it will move all the files it creates into a folder within the folder the rproj is called _sites --> to upload these files to the github in a way that github will be able to read them to create a website, move them out of _sites into the same folder that the rproj is in, click yes 3x to replace all the files that already exist within that folder (this is fine you're overwriting them with the same file that they already are)

within each .Rmd there are notes describing what the code is doing within html comments. These are: < ! - - (without the spaces) and - - > (without the spaces), the same is true within the header.html and the style.css (comments are  /astrix and astrix/)


the _site.yml controls the creation of the tabs within the navigation bar (all text under navbar:) at the top of the website and the formatting of the output html files(under output:).
  under navbar: the title corresponds to the text at the right hand side and is the title of the **website on the navbar** (this is different than the actual title of the website which is controlled by the name: command above the navbar command)
    under right: each href:/text: pair represents a tab within the navbar, the title: is the title of that tab as it appears in the navbar, the href: controls the name of the file used as a reference to create the content within that tab (these are the same as the name of all of the .Rmds just with a .html at the end and control the actual name of the link to that webpage ex: https://wessingerlab.github.io/additional_research.html is from the additional_research.html which is made from knitting the additional_research.Rmd)
  under output: there are 2 files right now 1) the style.css is in charge of base formatting for all web pages that are created, this is coded in css and has annotations within it to explain what the css does and 2) header.html which controls the formatting of the favicon (the icon that represents the lab website in the tab of the website, in your history and in your favoirtes bar)

the website was loading very slowly so I evaluated it with https://tools.pingdom.com/ and found that a large portion of the problem was the number and size of the images we used. my solution to this was to reduce the image size of most images to at MOST 500MB without losing image quality using [jpegoptim](https://www.omgubuntu.co.uk/2016/03/how-to-optimize-jpeg-command-line-linux) (installed on the lab computer).. to ensure you don't over compress (the image will become super pixelated), copy all original images to another place before trying to edit them in your working dir
```{R, echo=TRUE}
jpegoptim --size=500k path_to_wessingerlab.github.io/images/image_name.jpg
```
  
if R crashes and you can no longer push origin (with error "index.lock already exists") use

```{R, echo=TRUE}
rm -rf path_to_wessingerlab.github.io/.git/index.lock
```
  