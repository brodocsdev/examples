


# Diagrams as code and markdown combined

> A guide to configuring Visual Studio Code for working with PlantUML and Markdown to produce architecture documentation.




## Intro

A common saying claims that a picture is worth a thousand words, yet an IT architecture diagram without words may be nothing more than a collection of rectangles.

Therefore, you would find architecture diagrams combined with textual descriptions, published on a wiki or generated as a static site directly from Markdown or AsciiDoc files, rather than kept alone deep in a modeling tool repository, as used to be the case. 

Let’s have a quick look at the possible ways to work with diagrams and text combined in Markdown files, using a text editor (or IDE) to edit and preview the files, and PlantUML as the diagramming tool.

![](/PlantUML/Setup/res/img/mdPreview.png)



## Tools and ways of working

I will use Visual Studio Code as the editor, but it could be any editor or IDE. The diagramming tool can be either a WYSIWYG editor or a diagram-as-code tool. Let’s use the latter one. Both approaches have pros and cons; I will only mention that diagrams-as-code can be easily vibe-coded (fortunately you do not need a thousand words to produce a good-looking diagram) and, more importantly, they can serve as very good input to start a conversation with an LLM about your design or as part of AGENTS.md files.


There are many diagram-as-code tools, again, with pros and cons. PlantUML is one of them and supports many UML diagram types. It is not limited to UML only. You can create both simple diagrams of basic rectangles and complex AWS/GCP/Azure cloud diagrams. I do not want to explain the details of the PlantUML language here. Instead, I will focus on a quick setup of Visual Studio Code so that you can try it if you have not already.


There are two major ways to combine markdown files and diagrams. One is using placing the diagram code inside fenced code block:

```plain
@startuml
left to right direction

!theme blueprint
skinparam shadowing true


package "Web Application" {  
  [Web App] --> [API Server]
}
[API Server] --> [Database]

@@enduml
```

Second option is to keep the files separately and refer to them in markdown files. Both have good support in tools, so it is more a matter of preference, but sometimes tools you are using (editor, publisher) or diagram size may push you to some direction.

Let's try the way to keep them separately, convert locally to PNG images, and include via standard ```![](/path/to)``` markdown image links. It will let us use the markdown preview and see text and diagrams combined locally. Converted diagrams don't have to be committed if publishing tool supports auto conversion (many static site generators do).


## Visual Studio Code setup

In order to try local conversion, there is no need to [install PlantUML](https://plantuml.com/starting), which requires Java installation. Visual Studio Code extension is enough, it can be used with internal or public PlantUML server, which will handle the conversion. Public server is good to start, but can be quite slow, so local server or local installation is preferred if you plan to do more diagramming with PlantUML.

Just install the [jebbs.plantuml extension](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) and make some small changes to default configuration. Change the **Export Format** to png, **Export Out Dir** to ```./```, **Render** to PlantUMLServer and **Plantuml: Server** to official server: ```https://www.plantuml.com/plantuml```


![](/PlantUML/Setup/res/img/vscCfgExportFormat.png)
![](/PlantUML/Setup/res/img/vscCfgExportDir.png)
![](/PlantUML/Setup/res/img/vscCfgRenderer.png)




## Adding diagrams

There is a git repo at this address [https://github.com/brodocsdev/examples](https://github.com/brodocsdev/examples) containing files from this article, just clone it and open in VSC. There are two very simple diagrams committed, one is component diagram:

![](/PlantUML/Setup/res/puml/component.png)


second is sequence:

![](/PlantUML/Setup/res/puml/sequence.png)


The ```VSC Setup.md``` markdown file includes them both. When you open the preview for it, it will not show the images since only source files for diagrams are committed. They need to be converted first. Just open each of them and export it with ```PlantUML: Export Current Diagram``` plugin command. There is also VSC command to export all PlantUML diagrams of workspace, e.g. when you open fresh clone. 

![](/PlantUML/Setup/res/img/pumlExport.png)


Now, if you open preview for the markdown file again, you should see combined view of diagrams and text. The PlantUML plugin has its own preview, preview, so you can work on each and convert to PNG when finished.

## Review and publish your work

When you are done with text and diagrams, you may want to commit markdown and PlantUML files, create pull request for review, merge and see final result in publisher which support diagrams-as-code conversion out of the box. 
If you need to hand over the document in PDF format, for example to an external customer, you can use Pandoc to convert it. But this is a long story which cannot be cut short, so stay tuned 😎

Let me know in the comments which is your preferred way to combine text and diagrams, and which tools you use: Markdown or AsciiDoc.



