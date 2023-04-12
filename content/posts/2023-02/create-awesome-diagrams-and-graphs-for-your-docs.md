---
layout: post
author: Angel
date: 2023-02-23T17:05:15-05:00
title: "Awesome Diagrams and Graphs for Your Documentation"
tags: ["notes", "productivity", "diagrams", "diagrams.net", "app", "webapp"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

[Diagrams.net (or Draw.io)](https://www.diagrams.net) is a [free and open source](https://github.com/jgraph/drawio) cross-platform graph drawing software developed in HTML5 and JavaScript by UK-based JGraph Ltd in 2000.

Its interface can be used to create diagrams such as flowcharts, network diagrams, organizational charts, or any other type of diagram.

It is a useful alternative to more commercial tools like [Microsoft Visio](https://www.microsoft.com/en-us/microsoft-365/visio/flowchart-software) or [Lucidchart](https://www.lucidchart.com). 

## Getting Started

You can immediately start by heading over to the web application at [app.diagrams.net](https://app.diagrams.net/). There you can create and export your diagrams through the included web interface.

Desktop apps are available for Windows and Mac OS, which you can download [here](https://github.com/jgraph/drawio-desktop/releases/).

There are also [integrations](https://www.diagrams.net/integrations.html) with other platforms and applications, including [Atlassian Confluence Cloud](https://www.diagrams.net/doc/drawio-confluence-cloud.html) and Jira Cloud, Google applications, GitHub and Microsoft applications. 

## Workflow

### Online Whiteboard

The web based editor at diagrams.net gives you an easy-to-use online whiteboard to quickly note ideas and create graphs.

Below is a general overview of the layout of the editor and some of the elements.

![img](https://www.diagrams.net/assets/img/blog/interface-introduction.png)

### Choosing the Right Template

To choose a template, click on the `File` menu and select `New`. 

You'll be prompted with a list of templates, if you want a blank diagram, select it and then select `Insert`.

![img](https://www.diagrams.net/assets/img/blog/template-insert.png)

If you wish to select a different template, you can navigate back and select the template of your choosing.

### Adding Shapes and Text

To add a shape, simply click on the shape tool in the toolbar and drag the shape onto the canvas. You can also utilize the shape library and search for a specific shape.

The shape library search feature looks for shape names that match or are similar to your search term.

- At the top of the left panel, type your search term and press Enter.
- Click `More Results` to see more matching shapes.

![img](https://www.diagrams.net/assets/img/blog/shape-search.png)

To add text to your diagram, click on the text tool in the toolbar and click on the canvas where you want to add the text. 

You can also select `Arrange > Insert > Text` to insert a basic text shape. Or click the `+` icon in the toolbar, then select `Text`.

### Connecting Shapes

Click on the connector tool in the toolbar and drag the connector from one shape to another. You can customize the connector by changing its style, color, and thickness.

You can also connect shapes by cloning them, this will add another shape and automatically connect them.

![img](https://www.diagrams.net/assets/img/blog/clone-connect.gif)

You can learn more about the different ways to connect shapes [here](https://www.diagrams.net/doc/faq/connect-shapes).

### Adding Images and Other Elements

To add an image, simply click on the `Image` tool in the toolbar and select the image you want to add. You can then resize and position the image as needed.

JPEG, PNG, and SVG images can all be inserted into the diagram editor with drag and drop or via the menu.

Image files in diagrams work in the same way as in documents - you can resize, rotate and flip them as a single image, but you can’t resize any components within the image.

![img](https://www.diagrams.net/assets/img/blog/image-insert.gif)

Alternatively, you can insert from the menu: 

- Select `Arrange > Insert > Image`

or

- Click the `+` icon in the toolbar, then select `Image`. 

### Saving and Exporting Your Diagram

Once you have finished creating your diagram, you can save it by clicking on the `File` menu and selecting `Save`. 

You can then export your diagram as an image, PDF, URL, or other format by clicking on the `Export as` menu and selecting the format you want to use.

![img](https://www.diagrams.net/assets/img/blog/aws-example-file-export-as.png)

### Run Your Own Diagramming Server with Docker

There are many reasons that a SaaS application is not the right choice and companies prefer to run the software in their own environment, where all of the data and applications are kept behind a firewall for maximum security. 

**Draw.io Docker image**

The [draw.io Docker image](https://hub.docker.com/r/jgraph/drawio) is based on Tomcat to support reverse proxies, and is kept up to date with the production draw.io running on app.diagrams.net.

- [Install](/posts/2023-02/get-started-with-docker/#getting-started) and run the Docker platform on your server or desktop machine.
- Run the draw.io Docker container:

```    
docker run -it --rm --name="draw" -p 8080:8080 -p 8443:8443 jgraph/drawio
```

Note: Use the `DRAWIO_*` environment variables listed in `docker-entrypoint.sh` in the main directory to set up certificates and access to an SSL keystore mount. 

For example, a configured command will look similar to:

```
docker run -it -m1g -e LETS_ENCRYPT_ENABLED=true -e PUBLIC_DNS=drawio.example.com --rm --name="draw" -p 80:80 -p 443:8443 jgraph/drawio
```

For more information on setup and configuration options, refer to the [draw.io Docker image page on DockerHub](https://hub.docker.com/r/jgraph/drawio).

## Conclusion

Diagrams.net is a powerful and versatile tool for creating beautiful diagrams and drawings. 

With its wide range of templates and intuitive interface, you can quickly create professional-looking diagrams and drawings that are sure to impress.

### Learn More
- [Getting Started Guide](https://www.diagrams.net/doc/getting-started-editor)
- [Documentation](https://www.diagrams.net/doc/)
- [Features](https://www.diagrams.net/features)
- [Blog](https://www.diagrams.net/blog)
- [About JGraph Ltd](https://www.diagrams.net/about)
- [Docker Guide](https://www.diagrams.net/blog/diagrams-docker-app)
- [Project GitHub](https://github.com/jgraph)
- [Docker Hub](https://hub.docker.com/r/jgraph/drawio)