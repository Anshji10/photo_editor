A Photo Editor library with simple, easy support for image editing using Paints, Text, Filters, Emoji and Sticker like stories.

## Features
- [**Drawing**](#drawing) on image with option to change its Brush's Color, Size, Opacity, Erasing and basic shapes.
- Apply [**Filter Effect**](#filter-effect) on image using MediaEffect
- Adding/Editing [**Text**](#text) with option to change its Color with Custom Fonts.
- Adding [**Emoji**](#emoji) with Custom Emoji Fonts.
- Adding [**Images/Stickers**](#adding-imagesstickers)
- Pinch to Scale and Rotate views.
- [**Undo and Redo**](#undo-and-redo) for Brush and Views.
- [**Deleting**](#deleting) Views
- [**Saving**](#saving) Photo after editing.
- More [**FAQ**](#faq).

## Benefits
- Hassle free coding
- Increase efficiency
- Easy image editing

## Migrations
### AndroidX
PhotoEditor [v.1.0.0](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.1.0.0) is a migration to androidX and dropping the support of older support library. There are no API changes. If you find any issue migrating to v.1.0.0 , please follow this [Guide](https://developer.android.com/jetpack/androidx/migrate). If you still facing the issue than you can always rollback to [v.0.4.0](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.0.4.0). Any fix in PR are Welcome :)

### Kotlin
PhotoEditor [v.2.0.0](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.2.0.0) is fully migrated to Kotlin. You can use [v.1.5.1](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.1.5.1) for the Java version. There are no breaking API changes in these two versions.

Here's what it can do

## Drawing
We can customize our brush and paint with different set of property. To start drawing on image we need to enable the drawing mode
![](https://i.imgur.com/INi5LIy.gif)
| Type                                         | Method                                                                 |
|----------------------------------------------|------------------------------------------------------------------------|
| Enable/Disable                               | `mPhotoEditor.setBrushDrawingMode(true);`                              |
| Shape (brush, line, oval, rectangle, arrow)  | `mPhotoEditor.addShape(shape)`                                         |
| Shape color                                  | `mPhotoEditor.setBrushColor(colorCode)` or through the a ShapeBuilder  |
| Brush Eraser                                 | `mPhotoEditor.brushEraser()`                                           |

## Filter Effect
We can apply inbuild filter to the source images using 

 `mPhotoEditor.setFilterEffect(PhotoFilter.BRIGHTNESS)`

![](https://i.imgur.com/xXTGcVC.gif)

We can also apply custom effect using `Custom.Builder`

## Text

![](https://i.imgur.com/491BmE8.gif)

We can add the text with inputText and colorCode like this

`mPhotoEditor.addText(inputText, colorCode);` 

It will take default fonts provided in the builder. If we want different fonts for different text we can set typeface with each text like this

`mPhotoEditor.addText(mTypeface,inputText, colorCode);`

In order to edit the text we need the view, which we will receive in our PhotoEditor callback. This callback will trigger when we **Long Press** the added text

 ```java
 mPhotoEditor.setOnPhotoEditorListener(new OnPhotoEditorListener() {
            @Override
            public void onEditTextChangeListener(View rootView, String text, int colorCode) {
                
            }
        });
  ```
Now we can edit the text with a view like this

`mPhotoEditor.editText(rootView, inputText, colorCode);`

If you want more customization on text. Please refer the wiki page for more details.

## Adding Images/Stickers
 We need to provide a Bitmap to add our Images  `mPhotoEditor.addImage(bitmap);`


## Deleting
  For deleting a Text/Emoji/Image we can click on the view to toggle the view highlighter box which will have a close icon. So, by clicking on the icon we can delete the view.

## Saving

In [v.3.0.0](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.3.0.0) onward, we can save an image to a file using coroutines:

```kotlin
// Please note that if you call this from a fragment, you should call
// 'viewLifecycleOwner.lifecycleScope.launch' instead.
lifecycleScope.launch {
    val result = photoEditor.saveAsFile(filePath)
    if (result is SaveFileResult.Success) {
        showSnackbar("Image saved!")
    } else {
        showSnackbar("Couldn't save image")
    }
}
```


