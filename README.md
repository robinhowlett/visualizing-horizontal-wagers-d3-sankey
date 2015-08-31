## Sankey Diagram with Flow-Based API and End-to-End Highlighting

**Contributor:** [Ming Qin](github.com/QinMing) & Yahoo! Inc.

**Contributor's Contact Info.:** <mingq@yahoo-inc.com>

**Contributor's Orgnization:** Yahoo! Inc.

**Original Author:** [Ming Qin](github.com/QinMing) & Yahoo! Inc.

**Original Author's Orgnization:** Yahoo! Inc.

**Original Author's Contact Info.:** <mingq@yahoo-inc.com>

**Original Visualization Source Link:** <a href = "" target = "blank">Not published yet</a>

The original visualization is then developed on top of [D3’s Sankey plugin](http://bost.ocks.org/mike/sankey/) by [Mike Bostock](github.com/mbostock) (<mike@ocks.org>) at The New York Times.

Thanks David Ureña (at MicroStrategy, Inc.) and [Pradyut](http://community.microstrategy.com/t5/user/viewprofilepage/user-id/19497) for inspiration!

**Usage:** This visualization needs 2 or more attributes and 1 or more metrics.

**Screenshot:**

![Alt text][screenshot]
[screenshot]: ./style/images/screenshot.png?raw=true

**Description:**

Sankey diagrams visualize the magnitude of flow between nodes in a network.

In addition to [the original visualization](http://bost.ocks.org/mike/sankey/), this plugin has following features:

_1. Flow-based API and End-to-end highlighting_

The [original plugin](http://bost.ocks.org/mike/sankey/) take `nodes` and `links` as input, while this one has a different API. Instead of `links`, the input data contain `flows`, which has a single weight but multiple nodes in a chain. The attribute `thru` specify the array of these node objects (it can be object references, indices in `nodes` or node `name`). Here's an example of input data
```
{
    nodes: [
      {
        "name": "node0",
        "disp": "A",
      }, {
        "name": "node1",
        "disp": "B",
      }

      ......

    ],

    flows: [
      {
        value: 50,
        thru: [ "node0", "node1"]
      }, {
        value: 30,
        thru: [ 0, 1, 2 ]
      }

      ......

    ]
}
```
Compared to links, the flow structure is easier to construct because our raw data are in a multi-attribute table, where each row corresponds to a `flow`. In this sense, the plugin is also very suitable for visualizing parallel sets. The data in the screenshot come from this [parallel set visualization](https://www.jasondavies.com/parallel-sets/), but note that it's highlighting is very different.

Given the flow structure, the end-to-end highlighting is implemented. Whenever the mouse hover over an element, there are a certain subset of `flows` going through it. Then some new links (called `dlinks`) are dynamically computed from this flow subset, and placed on the canvas. The `dlinks` are positioned so as to make the highlighted flow looks consistent. But the positioning algorithm is coarse and can be improved.

_2. Rich tooltips_

Double click on the diagram to hide this feature.

_3. Settings_
You can customize the default tooltip style and number formats in the "visualization properties"
