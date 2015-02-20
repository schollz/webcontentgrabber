You can grab the html of a website, but what if you are only interested in a small part of the content of the website? For instance, in the following website, what if you only want the recipe and ingredients?

![Website example](https://i.imgur.com/b5JUgBG.jpg?1)

# Web Content Grabber

## How it works

First it grabs the Markdown-formatted text of the html page using [html2text](https://github.com/aaronsw/html2text).  It evalutes the number of 'cooking' related words in each line and pulls out the peak.

![Website example](https://i.imgur.com/enu0SNA.jpg?1)

It does the same for extracting the ingredient list. Then it scans the directions and the ingredient list to determine what the *actual* baking time would be and gives that estimate. Finally, it parses the measurements and foods in the ingredient list and cross-references the USDA SR27 food databse to get accurate estimations of the nutrition content.
