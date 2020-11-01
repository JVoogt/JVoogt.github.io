---
layout: post
title: Presenting from within Jupyter Notebooks
categories: how2
comments: true
---

## Introduction
I am sure that you do not want to read my whole back story on why I decided to write about how to present directly from your Jupyter Notebooks. Thus I think we should jump right into it.

## Opinions does matter
In my honest opinion there is 3 main ways on how to present your Notebooks, which we will cover in this article.
* Using your notebook in its normal form
* Using the built in Notebook to presentation converter
* RISE which uses reveal.js framework to allow us to instantly switch to presentation mode with additional customization’s

## Which one is better
“It depends” – every IT professional’s favorite words ever.
No, but seriously it really does depends. I have used all of the above methods to present the same notebook to different audiences in this last few weeks. Leaving the notebook in its natural form allows you to show your code and execution times of each segment.

While using the built in converter makes for a very safe presentation, it does take some time to get the layout just right of the slides and fragments. but once this is defined you can run a simple Powershell command to convert your notebook with results to an HTML file. I really like this as I know I do not have to run this code again in front of an audience and risk potential failure.

RISE brings together the best of both worlds, it allows you to run code blocks while in presentation mode. RISE also allows you to use more of your screen real estate as with the built in method you are limited to a predefined block size.

### Presenting Directly from your Notebook
This works well for a technical audience, When they are more interested in your code and results rather than the flash of a good PowerPoint Presentation.

![@JPVoogt](/public/img/JVoogt_2019-09-10-Presenting-from-within-Jupyter-Notebooks_1.png){:class="img-responsive"}
 
### Built in Presentation Mode
{% highlight sql %}
jupyter nbconvert Jupyter "NotebookName.ipynb" --to slides --post serve
{% endhighlight %}

Executing the above command in Powershell/CMD creates a HTML version of your Notebook. I like to do this and store the HTML copy on my phone before a presentation. This will allow me to have a disaster plan in case something happens to my laptop during or before my session

Go over to Matthew Speck’s article for a detailed setup: [link](https://medium.com/@mjspeck/presenting-code-using-jupyter-notebook-slides-a8a3c3b59d67)

### RISE
This is by far my favorite method of presenting a Notebook as it combined the best of both worlds. It is built on the Reveal.js framework. RISE allows you to present your Notebook in a PowerPoint format, with the ability to still execute your code blocks in the presentation mode.

You can read more on this [here](https://rise.readthedocs.io/en/maint-5.5/).

![@JPVoogt](/public/img/JVoogt_2019-09-10-Presenting-from-within-Jupyter-Notebooks_2.png){:class="img-responsive"}

## Download My Notebooks and HTML files with the below link
[CloudySQL – Data Manipulation Using Python for Beginners](https://github.com/JVoogt/Presentations/tree/master/CloudySQL%20-%20Data%20Manipulation%20Using%20Python%20for%20Beginners)



{% include post_footer.html %}
