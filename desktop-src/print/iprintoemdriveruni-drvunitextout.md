---
Description: The IPrintOemDriverUni::DrvUniTextOut method is provided by the Unidrv driver so that a rendering plug-in using a device-managed drawing surface can easily output text strings.
ms.assetid: f8c21813-9bfd-46a5-abb2-78ac2f2301af
title: IPrintOemDriverUni::DrvUniTextOut method
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# IPrintOemDriverUni::DrvUniTextOut method

The `IPrintOemDriverUni::DrvUniTextOut` method is provided by the Unidrv driver so that a rendering plug-in using a device-managed drawing surface can easily output text strings.

## Syntax


```C++
HRESULT DrvUniTextOut(
   SURFOBJ  *pso,
   STROBJ   *pstro,
   FONTOBJ  *pfo,
   CLIPOBJ  *pco,
   RECTL    *prclExtra,
   RECTL    *prclOpaque,
   BRUSHOBJ *pboFore,
   BRUSHOBJ *pboOpaque,
   POINTL   *pptlBrushOrg,
   MIX      mix
);
```



## Parameters

<dl> <dt>

*pso* 
</dt> <dd>

Pointer to a [**SURFOBJ**](https://www.bing.com/search?q=**SURFOBJ**) structure that describes the surface on which to write.

</dd> <dt>

*pstro* 
</dt> <dd>

Pointer to a [**STROBJ**](https://www.bing.com/search?q=**STROBJ**) structure that defines the glyphs to be rendered and the positions in which to place them.

</dd> <dt>

*pfo* 
</dt> <dd>

Pointer to a [**FONTOBJ**](https://www.bing.com/search?q=**FONTOBJ**) structure from which to retrieve information about the font and its glyphs.

</dd> <dt>

*pco* 
</dt> <dd>

Pointer to a [**CLIPOBJ**](https://www.bing.com/search?q=**CLIPOBJ**) structure that defines the clip region through which all rendering must be done. The driver cannot affect any pixels outside the clip region.

</dd> <dt>

*prclExtra* 
</dt> <dd>

Pointer to a RECTL structure. GDI always sets this parameter to **NULL** in calls to this function. It should be ignored by the driver.

</dd> <dt>

*prclOpaque* 
</dt> <dd>

Pointer to a [**RECTL**](https://www.bing.com/search?q=**RECTL**) structure that represents a single opaque rectangle. This rectangle is bottom-right exclusive. Pixels within this rectangle (those that are not foreground and not clipped) are to be rendered with the opaque brush. This rectangle always bounds the text to be drawn. If this parameter is **NULL**, no opaque pixels are to be rendered.

</dd> <dt>

*pboFore* 
</dt> <dd>

Pointer to a [**BRUSHOBJ**](https://www.bing.com/search?q=**BRUSHOBJ**) structure that represents the brush object to be used for the foreground pixels. This brush will always be a solid color brush.

</dd> <dt>

*pboOpaque* 
</dt> <dd>

Pointer to a BRUSHOBJ structure that represents the opaque pixels. Both the foreground and background mix modes for this brush are assumed to be R2\_COPYPEN. Unless the driver sets the GCAPS\_ARBRUSHOPAQUE capabilities bit in the **flGraphicsCaps** member of the DEVINFO structure, it will always be called with a solid color brush.

</dd> <dt>

*pptlBrushOrg* 
</dt> <dd>

Pointer to a [**POINTL**](https://www.bing.com/search?q=**POINTL**) structure that defines the brush origin for both brushes.

</dd> <dt>

*mix* 
</dt> <dd>

The foreground and background raster operations (mix modes) for *pboFore*.

</dd> </dl>

## Return value

The method must return one of the following values.



| Return code                                                                               | Description                               |
|-------------------------------------------------------------------------------------------|-------------------------------------------|
| <dl> <dt>**S\_OK**</dt> </dl>      | The operation succeeded.<br/>       |
| <dl> <dt>**E\_FAIL**</dt> </dl>    | The operation failed.<br/>          |
| <dl> <dt>**E\_NOTIMPL**</dt> </dl> | The method is not implemented.<br/> |



 

## Remarks

The `IPrintOemDriverUni::DrvUniTextOut` method is provided by Unidrv for use by rendering plug-ins that support a device-managed drawing surface. Such rendering plug-ins must hook out Unidrv's [**DrvTextOut**](https://www.bing.com/search?q=**DrvTextOut**) function, and the `IPrintOemDriverUni::DrvUniTextOut` method is meant to be called from that hooking function. The hooking function must perform text region clipping and text rotation operations. It can then call `IPrintOemDriverUni::DrvUniTextOut` to request Unidrv to create the text string using downloadable fonts (and to perform glyph-based clipping).

If `IPrintOemDriverUni::DrvUniTextOut` cannot create the text string, either because the font is not available or is rotated, it calls the rendering plug-in's [**IPrintOemUni::TextOutAsBitmap**](iprintoemuni-textoutasbitmap.md) method, which draws the text string as a bitmap.

For more information, see [Handling Device-Managed Surfaces](https://www.bing.com/search?q=Handling Device-Managed Surfaces).

## Requirements



|                            |                                                                                                            |
|----------------------------|------------------------------------------------------------------------------------------------------------|
| Target platform<br/> | <dl> <dt>Desktop</dt> </dl>                         |
| Header<br/>          | <dl> <dt>Prcomoem.h (include Prcomoem.h)</dt> </dl> |



 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20IPrintOemDriverUni::DrvUniTextOut%20method%20%20RELEASE:%20%285/12/2018%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/en-us/default.aspx. "Send comments about this topic to Microsoft")



