<img width="260" alt="Screenshot 2023-08-15 at 12 37 26 PM" src="https://github.com/rbolivarv94/scroller-sequence/assets/72158166/06ba0e6b-93d7-46a5-9f81-acd6701111ec">

# scroller-sequence
The scroller component is designed to create a scrolling visual experience with a sequence of images and sticky information blocks. 
This documentation provides an overview of the component's structure, settings, and usage.

Table of Contents
Schema
HTML Structure
Styling
JavaScript
Schema
The scroller component uses JSON-like schema definition to configure its behavior. The schema defines the component's name, presets, settings, and blocks.

json
Copy code
{
  "name": "scroller",
  "presets": [
    {
      "name": "scroller",
      "category": "custom"
    }
  ],
  "settings": [
    {
      "type": "number",
      "id": "lengthHeight",
      "label": "Scroll Length(Recommended: totalImages*22)"
    },
    {
      "type": "number",
      "id": "totalImages",
      "label": "Total number of images on sequence",
      "default": 449
    },
    {
      "type": "text",
      "id": "seq-name",
      "label": "Image Sequencer commonName",
      "default": "TEST"
    }
  ],
  "blocks": [
    {
      "type": "infoBlock",
      "name": "infoBlock",
      "settings": [
        {
          "type": "number",
          "id": "position-inner-y",
          "label": "Position Y to show(px)"
        },
        {
          "type": "number",
          "id": "position-inner-x",
          "label": "Position X to show(%)"
        },
        {
          "type": "html",
          "label": "html code",
          "id": "info-inner"
        },
        {
          "type": "number",
          "id": "stickyHeight",
          "label": "how long(px) should stay at the top?",
          "default": 600
        }
      ]
    }
  ]
}

<img width="260" alt="Screenshot 2023-08-15 at 12 37 26 PM" src="https://github.com/rbolivarv94/scroller-sequence/assets/72158166/2c165a5c-71aa-40c0-9a3d-9e8afbfa5ba3">
![Uploading Screenshot 2023-08-15 at 12.37.18 PM.png…]()
![Uploading Screenshot 2023-08-15 at 12.37.12 PM.png…]()

HTML Structure
The scroller component's HTML structure consists of multiple images and information blocks. The component generates the images and applies the necessary styles to create the scrolling effect.

html
Copy code
<div id="background" style="height: {{ section.settings.lengthHeight }}px;"></div>
{% for block in section.blocks %}
  {% case block.type %}
    {% when 'infoBlock' %}
      <div
        class="info-block"
        data-stickyheight="{{ block.settings.stickyHeight }}"
        style="top: {{ block.settings.position-inner-y }}px; left: {{ block.settings.position-inner-x }}%; position: absolute; z-index: 1;"
      >
        <div>{{ block.settings.info-inner }}</div>
      </div>
  {% endcase %}
{% endfor %}

<div class="fixedTop">
  <div id="image-scroll" style="height: {{ section.settings.lengthHeight }}px; position: relative;">
     <!-- Images are generated here using loops -->
  </div>
</div>
<div style="height: 100vh;"></div>
Styling
The component includes embedded CSS styles to control the appearance and layout of various elements.

css
Copy code
.fixedTop {
  position: fixed;
  top: 7rem;
  width: 100%;
}

#background {
  background-repeat: no-repeat;
  background-size: cover;
}

.info-block {
  position: absolute;
  transition: transform 0.3s ease;
}

div#image-scroll {
  display: flex;
  flex-direction: column;
  align-items: center;
}

@media (min-width: 1440px) {
  .scroll-image {
    width: 100%;
  }
}

@media (max-width: 1439px) {
  .scroll-image {
    height: 90vh;
  }
}
JavaScript
The component's JavaScript functionality is responsible for handling scrolling and sticky behavior of information blocks.

javascript
Copy code
var container = document.getElementById('image-scroll');
var images = Array.from(container.getElementsByTagName('img'));
var isScrolling = false;

var observer = new IntersectionObserver(function(entries) {
  // Intersection observer logic
});

function scrollHandler() {
  // Scrolling logic
}

observer.observe(container);

window.onload = function() {
  // Sticky information blocks logic
};
This documentation provides an overview of the scroller component's structure, settings, and functionality. You can customize and integrate this component into your projects to create engaging scrolling experiences with images and sticky information blocks.
