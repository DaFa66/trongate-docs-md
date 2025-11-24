# Working With Images


Trongate CSS provides simple yet powerful image handling capabilities out of the box. Images are automatically made responsive while maintaining their aspect ratios, ensuring they look great across all devices.

## Basic Image Styling


By default, all images in Trongate CSS are responsive. Simply use the standard HTML `<img>` tag, and Trongate CSS will handle the rest:

![Example responsive image](images/dragon.webp)
```html
<img src="path/to/your/image.jpg" alt="Example responsive image">
```


This works because Trongate CSS automatically applies `max-width: 100%;` and `height: auto;` to all images, ensuring they scale proportionally within their containers while maintaining aspect ratio.

## Image Alignment


Trongate CSS provides several utility classes for controlling image alignment:

![Left aligned image](images/horse.webp)
![Right aligned image](images/horse.webp)
![Center aligned image](images/horse.webp)
```html
<!-- Left aligned image -->
<img src="path/to/image.jpg" alt="Left aligned image" class="float-left">

<!-- Right aligned image -->
<img src="path/to/image.jpg" alt="Right aligned image" class="float-right">

<!-- Center aligned image -->
<div class="text-center">
    <img src="path/to/image.jpg" alt="Center aligned image">
</div>
```

## Responsive Image Grids


Create flexible image galleries using Trongate's flexbox utilities:

![Grid image 1](images/lion.webp)![Grid image 2](images/lion.webp)![Grid image 3](images/lion.webp)
```html
<div class="flex-row flex-wrap justify-between">
    <img src="image1.jpg" alt="Grid image 1" style="width: 32%; margin-bottom: 1em;">
    <img src="image2.jpg" alt="Grid image 2" style="width: 32%; margin-bottom: 1em;">
    <img src="image3.jpg" alt="Grid image 3" style="width: 32%; margin-bottom: 1em;">
</div>
```

## Images in Cards


Images work seamlessly within card components:

![Card image example](images/falcon.webp)Images automatically fit within card boundaries while maintaining their aspect ratio.
```html
<div class="card">
    <img src="path/to/your/image.jpg" alt="Card image example">
    <div class="card-body">
        <p>Images automatically fit within card boundaries while maintaining their aspect ratio.</p>
    </div>
</div>
```

> [!TIP]
> **Best Practices**
>
> When working with images in responsive layouts, consider these best practices:
> 
> 
> - Always include meaningful alt text for accessibility.
> - Use appropriate container classes to control maximum image width.
> - Consider using different aspect ratios for different types of content.
> - Test images across different screen sizes to ensure proper scaling.


> [!NOTE]
> **Just To Let You Know...**
>
> While Trongate CSS handles responsive image scaling automatically, it's still important to serve appropriately sized images to optimize loading times and performance.


