You can grab the html of a website, but what if you are only interested in a small part of the content of the website? For instance, in the following website, what if you only want the recipe and ingredients?

![Website example](https://i.imgur.com/b5JUgBG.jpg?1)

# Web Content Grabber

## How it works

First it grabs the Markdown-formatted text of the html page using [html2text](https://github.com/aaronsw/html2text).  It then searches through for the number of lines with any number of a given set of content-related words. For instance, in probing the recipe website above with "cooking" related words you'll see the following:

![Website example](https://i.imgur.com/enu0SNA.jpg?1)

The peak that emerges is the directions for the recipe on the website. That content can then be efficiently extracted using a single-gaussian curve fitting algorithm.

## Installation

Requirements:

```bash
$ sudo pip install html2text numpy scipy
```

If you want to plot pictures, you'll also need ```matplotlib```.

## Configuration

The contexts that it looks for are on in the ```context_settings.json``` file. The main keys are the names of the context that you want, and then the ```context_words``` are the words that are searched for. Additionally it only searches for words if the number of words is within ```hasFewerWordsThan``` and ```hasMoreWordsThan```. If everything is good, then it also searches whether it has a special character ```hasSpecial``` which also incluences the result.

```json
{  
   "ingredients":{  
      "context_words":[  
         "cup","can","jar","package","ounce","pound","whole","tablespoon"
      ],
      "hasFewerWordsThan":6,
      "hasMoreWordsThan":1,
      "hasSpecial":"*"
   },
   "directions":{  
      "context_words":[  
         "aioloi","aged","adjust","braise","infuse","homogenize","blend","brush","line","lard","carmelize","peel","emulsify","preheat"
      ],
      "hasFewerWordsThan":-1,
      "hasMoreWordsThan":6,
      "hasSpecial":"NONE"
   }
}
```

## Example

For example, if you run the builtin context_settings.json on a recipe website, like [Alton Brown's waffle recipe](), then you get distinct peaks for the "directions" and "ingredients":

![Contextual peaks](https://i.imgur.com/ju9eboZ.png?1)

From that, the actual text is extracted is:

```
------------------------------
directions
------------------------------
Preheat waffle iron according to manufacturer's directions.
In a medium bowl whisk together the flours, soda, baking powder, salt, and sugar. In another bowl beat together eggs and melted butter, and then add the buttermilk. Add the wet ingredients to the dry and stir until combined. Allow to rest for 5 minutes.
Ladle the recommended amount of waffle batter onto the iron according to the manufacturer's recommendations. Close iron top and cook until the waffle is golden on both sides and is easily removed from iron. Serve immediately or keep warm in a 200 degree F oven until ready to serve.
Recipe courtesy Alton Brown, 2005


------------------------------
ingredients
------------------------------
  * 4 3/4 ounces all-purpose flour, approximately 1 cup
  * 4 3/4 ounces whole-wheat flour, approximately 1 cup
  * 1/2 teaspoon baking soda
  * 1 teaspoon baking powder
  * 1 teaspoon salt
  * 3 tablespoons sugar
  * 3 whole eggs, beaten
  * 2 ounces unsalted butter, melted
  * 16 ounces buttermilk, room temperature
```
