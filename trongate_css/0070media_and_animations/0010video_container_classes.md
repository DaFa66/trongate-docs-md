# Video Containers


Trongate CSS provides utility classes to help you embed videos responsively. The `.video-container` and `.video` classes work together to ensure embedded videos maintain proper aspect ratios and remain responsive across all device sizes.

## Basic Implementation


To embed a responsive video, wrap the `<iframe>` in a container with the `.video-container` class, and add the `.video` class to the `<iframe>` itself. For example:

```html
<div class="video-container">  
    <iframe  
        class="video"  
        src="https://www.youtube.com/embed/UIa3r12oCo8?si=9Nb8ivyEbxYt0Z27"  
        title="YouTube video player"  
        frameborder="0"  
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"  
        referrerpolicy="strict-origin-when-cross-origin"  
        allowfullscreen></iframe>  
</div>
```


**Note:** The `width` and `height` attributes are intentionally omitted from the `<iframe>` tag as the CSS rules dynamically control the dimensions to ensure responsiveness.

## Different Aspect Ratios


While the default aspect ratio is 16:9, you can specify different ratios using modifier classes:

```html
<!-- For 4:3 videos -->  
<div class="video-container aspect-4-3">  
    <iframe  
        class="video"  
        src="https://www.youtube.com/embed/UIa3r12oCo8"  
        allowfullscreen></iframe>  
</div>  

<!-- For square (1:1) videos -->  
<div class="video-container aspect-1-1">  
    <iframe  
        class="video"  
        src="https://www.youtube.com/embed/UIa3r12oCo8"  
        allowfullscreen></iframe>  
</div>
```

## How It Works


The video container classes use CSS custom properties to maintain the correct aspect ratio. The key is the `padding-bottom` value, which is calculated based on the aspect ratio:

```css
.video-container {  
    --aspect-ratio: 16 / 9; /* Default aspect ratio */  
    position: relative;  
    width: 100%;  
    height: 0;  
    padding-bottom: calc(100% / var(--aspect-ratio));  
}  

.video-container.aspect-4-3 {  
    --aspect-ratio: 4 / 3;  
}  

.video-container.aspect-1-1 {  
    --aspect-ratio: 1 / 1;  
}  

.video {  
    position: absolute;  
    top: 0;  
    left: 0;  
    width: 100%;  
    height: 100%;  
    border: 0;  
}
```


By combining the `.video-container` and `.video` classes, your videos will maintain their proper proportions and adapt seamlessly to different screen sizes.

