﻿# AppoMobi.Maui.DrawnUi DEMO

Demo of an upcoming rendering engine for .Net MAUI to draw your UI on a Skia canvas, with gestures and animations, designed to draw pixel-perfect custom controls instead of using native ones.

Supports **iOS**, **MacCatalyst**, **Android**, **Windows**.

* To use inside a usual Maui app, consume drawn controls here and there inside `Canvas` views.
* Create a totally drawn app with just one `Canvas` as root view and consume controls inside, `SkiaShell` is provided for navigation.
* Drawn controls are totally virtual and are basically commands for the DrawnUi library on what and how to draw on a skia canvas.
 
_The current development state is __PRE-ALPHA__, some features remain to be implemented, the project is active._

The rendering engine is free to use, the goal is to provide an easy way to create and draw custom-made ui elements.

Library repo will go public at Alpha stage, Pre-Alpha nuget package is already available to be consumed. 

## What's new

### An updated nuget and demo are incoming soon with performance improvements for iOS (Metal renderer) and more.

__1.0.1.32-pre__
[nuget](https://www.nuget.org/packages/AppoMobi.Maui.DrawnUi/1.0.1.32-pre)
* Garbage collection effect reduced..
* SkiaImageLoader now uses Glide on Android for urls. 
* Images auto-detect going online to instantly reload missed sources from being offline.
* Fixes: gestures in drawer, scroll, carousel etc.
* Demo: ⛳ added __Parallax__ effect to cells in the second tab.
* Docs: added more info about caching.

## Development Notes

* All files to be consumed (images etc) must be placed inside the maui app Resources/Raw folder, subfolders allowed.
* If you use the LiveTree toolbar in VS it would crash while debugging at some point please do not use it. 

## Screenshots

### _Draw your recycled cells on a canvas_

https://github.com/taublast/AppoMobi.Maui.DrawnUi.Demo/assets/25801194/f562e126-1586-4a4f-a08c-fb6437c0df27

### _Scroll, navigate and switch virtual views_

https://github.com/taublast/AppoMobi.Maui.DrawnUi.Demo/assets/25801194/e86200de-16ba-4e24-a7f5-ec7ba944a9a9

### _Create your drawn controls_

https://github.com/taublast/AppoMobi.Maui.DrawnUi.Demo/assets/25801194/2182de51-929e-47f6-a560-e9d97ad16e52

### _Draw rich and tappable text_

https://github.com/taublast/AppoMobi.Maui.DrawnUi.Demo/assets/25801194/a2efa080-f234-4d04-a7f5-aab8af462fb2

### _Play with the Canvas_

https://github.com/taublast/AppoMobi.Maui.DrawnUi.Demo/assets/25801194/6f92241a-ab39-4f66-bc78-2f10755a2bae


## Features

* __Draw your UI using SkiaSharp with hardware acceleration__
* __Easily create your controls and animations__
* __Design in Xaml or code-behind__
* __2D and 3D Transforms__
* __Animations__ targeting max fps
* __Gestures__ support for panning, scrolling and zooming (_rotation incoming_)
* __Caching system__ for elements and images
* __Optimized for performance__, rendering only visible elements, recycling templates etc
* __Prebuilt Basic Ui Elements__	
	* __SkiaShape__ (Rounded rectangle, Circle, Gauge, _more to come_) can wrap other elements
	* __SkiaLabel__, multiline with many options
	* __SkiaImage__ with options and filters
	* __SkiaSvg__ with many options
	* __SkiaLottie__ with tint customization
	* __SkiaRive__ (actually Windows only)
	* __SkiaLayout__ (Absolute, Grid, Vertical stack, Horizontal stack, _todo Masonry_) with templates support
	* __SkiaScroll__ (Horizonal, Vertical, Both) with header, footer, zoom support and adjustable inertia, bounce, snap and much more. Can act like a collectionview with custom refresh indicator, load more etc
	* __SkiaHotspot__ to handle gestures in a easy way
	* __SkiaMauiElement__ for when skia is not enough

* __Derived custom controls__
	* __SkiaButton__ include anything inside, text, images etc
	* __SkiaScrollLooped__ for neverending scrolls
    * __SkiaDrawer__ to swipe in and out your controls
	* __SkiaCarousel__ swipe and slide controls inside a carousel
	* __SkiaHoverMask__ to overlay a clipping shape
	* __SkiaLabelFps__ for developement
	* __SkiaDecoratedGrid__ to draw shapes between rows and columns
	* __ScrollPickerWheel__ for creating wheel pickers
	* __RefreshIndicator__ can use lottie and anything for your scroll refresh view
	* __SkiaTabsSelector__ create top and bottom tabs
	* __SkiaViewSwitcher__ switch your views, pop, push and slide	
	* __Create your own!__ 

* Animated Effects
	* __Ripple__
	* __Shimmer__
	* __BlinkColors__
	* (_todo Pulse, Shake etc_)
	* __Commit yours!__

* Animators
	
	* _todo add info

* Transforms
	* TranslationX
	* TranslationY
	* ScaleX
	* ScaleY
	* Rotation
	* CameraAngleX
	* CameraAngleY
	* CameraAngleZ
	* SkewX
	* SkewY
	* Perspective1
	* Perspective2
	
## Installation

Install the package __AppoMobi.Maui.DrawnUi__ from NuGet. Check the pre-release option if you don't see the package.

After that initialize the library inside your MauiProgram.cs file:

```csharp
builder.UseDrawnUi<App>();
```

## Quick Start

You will be mainly using Maui view `Canvas` that will wrap your SkiaControls.
Anywhere in your existing Maui app you can include a `Canvas` and start drawing your UI.
The `Canvas` control is aware of its children size and will resize accordingly.
At the same time you could set a fixed size for the `Canvas` and its children will adapt to it.

#### Xaml
Import the namespace:
```xml  
  xmlns:draw="http://schemas.appomobi.com/drawnUi/2023/draw"
```
Consume:

```xml  
<draw:Canvas>
     <draw:SkiaSvg
        Source="Svg/dotnet_bot.svg"
        LockRatio="1"
        TintColor="White"
        WidthRequest="44" />
</draw:Canvas>
```

As you can see in this example the Maui view `Canvas` will adapt it's size to drawn content and should take 44x44 pts. `LockRatio="1"` tells the engine to take the highest calculated dimension and multiply it by 1, so even we omitted `HeightRequest` it was set to 44.

#### Code behind

```csharp
	_todo_
```

Please check the demo app, it contains many examples of usage.

## Images

* Images loaded and converted for skia format are cached on a per-app run basis.

* When am image fails to load then if the app was offline the image will get its method `ReloadSource` invoked. So when you go online your missing images will get automatically loded!

* 'SkiaScroll' can also control loading of images via `VelocityImageLoaderLock` property, that would lock and unlock loading of images globally in case of a huge velocity scroll.

Base control for using images is `SkiaImage` with many virtuals to be easily subclassed for your needs. The `Source` property is a usual maui `ImageSource`.
`SkiaImageManager` loads platform sources and converts them to skia format. It falls back to default maui methods for loading `ImageSource` in some cases.

On Android the `Glide` library is used for loading urls. It caches images, making it so if the app is offline it still gets its images from cache if they were loaded previously.

### Gestures

To make your root `Canvas` catch gestures you need to attach a `TouchEffect` to it. This can be done automatically by setting `GesturesEnabled="True"` for the `Canvas`.
After that skia controls can process gestures in multiple ways:
* At low level by implementing an `ISkiaGestureListener` interface and overriding `OnGestureReceived`.
* At control level by overriding `ProcessGestures`, recommended for custom controls.
* Attaching a `HandleGestures` effect that has properties similar to `SkiaHotspot`.
* Including a `SkiaHotspot` as a child.
* Using a `SkiaButton`.

Parent controls have full control over gestures and passing them to children. 
In a base scenario a gesture would be passed all along to the ends of a view tree to its ends for every top-level control.
If a gesture is marked as consumed (by returning the reference of the consumer, not consumed if `null`) a control would typically stop processing gestures at its level. 

By overriding `ProcessGestures` any control might process gestures with or without passing them to children.

When creating a custom control the standard code for the override would be to pass gestures below by calling `base` then processing at the current level. You might choose to do it differently according to your needs.

The engine is designed to pass the ending gestures to those who already returned "consumed" for preceding gestures even if the following gestures are out of their hitbox.

__More docs will be added on this matter.__


### Caching System

_!_ Without caching animations going beyond simple wouldn't be possible. 
Caching makes complicated processing needed just once for layout calculation 
and then the caching result is redrawn on every frame.

Caching is controlled using a property `UseCache` of the following type:

```csharp
public enum SkiaCacheType
{
    /// <summary>
    /// True and old school
    /// </summary>
    None,

    /// <summary>
    /// Create and reuse SKPicture. Try this first for labels, svg etc. 
    /// Do not use this when dropping shadows or with other effects, better use Bitmap. 
    /// </summary>
    Operations,

    /// <summary>
    /// Will use simple SKBitmap cache type, will not use hardware acceleration.
    /// Slower but will work for sizes bigger than graphics memory if needed.
    /// </summary>
    Image,

    /// <summary>
    /// Using `Image` cache type with double buffering. Best for fast animated scenarios, this must be implemented by a specific control, not all controls support this, will fallback to 'Image' if anything.
    /// </summary>
    ImageDoubleBuffered,

    /// <summary>
    /// The way to go when dealing with images surrounded by shapes etc.
    /// The cached surface will use the same graphic context as your canvas.
    /// If hardware acceleration is enabled will try to cache as Bitmap inside graphics memory. Will fallback to simple Bitmap cache type if not possible. If you experience issues using it, switch to Memory cache type.
    /// </summary>
    GPU,
}

```

You should tweak your design caching to avoid unnecessary re-drawing of elements. 
The basic approach here is to cache small elements at some level. 
When you start using any kind of animations you should start using caching to max your FPS. You can check the __DemoApp__ for such examples.

#### Caching Tips:

* Cache shapes, svg and text as `Operations`.
* Prefer caching shadows and gradients as `Image` instead of `Operations`.
* Cache large static overlays as `GPU`, large static blocks as `Image`.
* For dynamically changing controls consider `ImageDoubleBuffered`, it consumes double the memory as `Image` but doesn't slow down rendering: you would see the latest prepared cache until the actual state wouldn't finish rendering itsself to a hidden cache layer in background.
* Do not include controls cached with `GPU` inside controls that use different type of cache, except for `Disabled`, will get a native crash otherwise.

#### Loaded Images

We are using the __EasyCaching.InMemory__ library for caching loaded bitmaps. It's impact can much be seen when using recycled cells inside a scroll. 
_todo add options and link to ImageLoader and SkiaImage docs_

_!_ When using images inside dynamic scene, like a a templated stack with scroll or other 
you should try to set the image cache to `Image` this would most probably climb your fps.
This is due to the fact that image sources are usually of the wrong size and they need processing 
before being drawn. When using `Image` cache the image would be processed only once and 
then just redrawn.

### Transforms

* TranslationX
* TranslationY
* ScaleX
* ScaleY
* Rotation
* CameraAngleX
* CameraAngleY
* CameraAngleZ
* SkewX
* SkewY
* Perspective1
* Perspective2

### Animations

One would create animations and effects using animators. Animators are attached to controls, but technically register themselves at the root canvas level and their code is executed on every rendering frame. If the canvas is not redrawing then animators will not be executed.
When the canvas has a registered animator running it would constantly force re-drawing itself until all animators are stopped.

There are two types of animators: 
* __Animators__ are executed before the drawing, so you can move and transform elements before the are rendered on the canvas.
* __PostAnimators__ are executed after their parent element was drawn, so you can paint an effect over the existing result, or execute any other post-drawing logic.

### Layout

For initial items positionning you would be using `SkiaLayout`. 
Its `Absolute` layout type is already buil-it in every skia control..

You can position your children using familiar properties like
`HorizonalOptions`, `VerticalOptions`, `Margin`, parent `Padding`,
`WidthRequest`, `HeightRequest`,`MinimumWidthRequest`, `MinimumHeightRequest` 
and additional `MaximumWidthRequest`,  `MaximumHeightRequest`, `HorizontalFillRatio`, `VerticalFillRatio` and `LockRatio` properties.

* `LockRatio`will be used to calculate the width when the height is set or vice versa. If it's above 0 the max value will be applied, if it's below 0 the min value will be applied. If it's 0 then the ratio will be ignored.
* `HorizontalFillRatio`, `VerticalFillRatio` will let you take a percent and the available size if you don't set a numeric request. For example if `HorizontalFillRatio` is set to 0.5 you will take 50% of the available width, at the same time being able to align the control at start, center or at the and in a usual way.

For dynamic positioning or other precise cases use `TranslationX` and `TranslationY`.

When you need to layout children in a more arranged way you will want to wrap them with a `SkiaLayout`
of different `LayoutType` : Grid, Colum, Row and others.

Layout supports `ItemTemplate` for most of layout types.

Some differences from Xamarin.Forms/Maui to notice:

* Layouts as other controls come with `HorizontalOptions` and `VerticalOptions` as `Start` and not `Fill` by default, so if your children do not request a size explicitly, 
the parent layout will not take any space at all unless you ask it to `Fill` the desired dimension, for example a `Column` needs its  `HorizontalOptions` to be `Fill` or specified explicitly.

* Actually for performance reasons in `Column` and `Row` layouts children cannot have `Fill`, `End` and `Center` in the direction of the layout, only `Start`. For example, if you have a `Column` children must have `VerticalOptions` set to `Start`. When you still need these options for children please use `Absolute` or `Grid` layouts.

_!_ Layouts `Column` and `Row`, whether templated or not, 
will always check if child is out of the visible screen bounds and avoid rendering it in that case.
That is especially useful when the layout is inside a `SkiaScroll`, this way we always render 
only the visible part. You can tweak this but setting a `SkiaLayout` property `HiddenAmountToRender` in points, how many of the hidden amount outside the visible bounds should still be rendered. 
This system ensures that you can have an infinite-size layout inside a scroll and it will work just fine drawing only the visible area.
At the same time if you want a `SkiaScroll` to <s>lye</s> communicate to its content that everything is visible on the screen you can set its `VirtualizationEnabled="False"`.

_!_ You can absolutely use the `Margin` property in a usual Maui way. In case if you would need to bind a specific margin you can switch to 
using `MarginLeft`, `MarginTop`, `MarginRight`, `MarginBottom` properties, -1.0 by default, 
if set they will override the specific value from `Margin`, and the result would be accessible via `Margins` read-only bindable static property.  
Even more, sometimes you might want to bind your code to `AddMarginTop`, `AddMarginLeft`, `AddMarginRight`, `AddMarginBottom`..  
When designing custom controls please use `Margins` property to read the final margin value.

#### Loading sources

SkiaImage, SkiaLottie and other controls that have a `Source` property, can load data from web, from bundled resources and from native file system.
The conventions is the following:
- if a web url is detected the source is loaded from web
- if a file path starts with file:// it will be loaded from native file system
- otherwise will try to load from bundled resources with root folder 'Resources\Raw'. 

Example below will load animation from `Resources\Raw\Lottie\Loader.json`.

```xml  
            <draw:SkiaLottie
                InputTransparent="True"
                AutoPlay="True"
                ColorTint="{StaticResource ColorPrimary}"
                HorizontalOptions="Center"
                ="1"
                Opacity="0.85"
                Repeat="-1"
                Source="Lottie/Loader.json"
                Tag="Loader"
                VerticalOptions="Center"
                WidthRequest="56" />
```


#### Enhanced usage

When dealing with subviews in code behind you could typically use two ways. 

Example for adding a subview:
 
* Use method `SetParent` passing new parent. In this case parent layout will not be invalidated, use this for optimized logic when you know what you are doing. You can mainly use this way when just constructing parent, knowing it will be measured at start anyway.
* Call parent's method `AddSubView` passing subview Parent's layout will be invalidated, and OnChildAdded will be called on parent.
* When working with `Children` property use `Add` method, it will set `Views` to a new instance of appropriate collection, and call `AddSubView` for each item.

For removing a subview the usual options would be:

* Call `SetParent` passing null, for soft removal.
* Call parent's method `RemoveSubView` passing subview`.Parent`'s layout will be invalidated, and OnChildRemoved will be called on parent.	
* When working with `Children` property use `Remove` method, it will set `Views` to a new instance of appropriate collection, and call `RemoveSubView` for each item.
 
#### In Deep

When XAML would be constructed it would fill `Children` property with views, this property is for high-level access. `Views` 

Will be then filled internally. When you add or remove items in `Children` methods `AddSubView` and `RemoveSubView` will be called for managing `Views`.


### Enhanced Usage

#### Draw a line or rectangle or reserve space

Use a simple `SkiaControl`. For complex shapes use `SkiaShape` or `SkiaPath`.

#### Simulate Maui Grid

`SkiaLayout` of `Grid` type, set children properties as usual (`Grid.`something)

#### Simulate Maui CollectionView

`SkiaScroll` + `SkiaLayout` (ItemTemplate=...). Set cache of the cell to Bitmap or Operations depending on your needs.


#### Simulate Maui StackLayout with a BidableLayout.ItemTemplate 

`SkiaScroll` (Virtualisation=false) + `SkiaLayout` (ItemTemplate=..., UseCache=CacheType.Operations) 



#### *Styles*

When you want to dynamically change properties in Xaml you might want to use conditional styles.
They look like regular Maui styles, but with some nuances:
* When defining style is resources you must set a unique `Class` attribute
* They are selected at runtime upon `Condition` or `State` bindable properties. `State` is like Maui `VisualState`but you can have several of them applied at the same time.

Define a style inside `ResourceDictionary`:

```xml  
    <Style
        x:Key="SkiaLabelDefaultStyle"
        Class="SkiaLabelDefaultStyle"
        TargetType="draw:SkiaLabel">
        <Setter Property="TextColor" Value="#E8E3D7" />
        <Setter Property="FontFamily" Value="FontText" />
        <Setter Property="FontSize" Value="15" />
    </Style>
```

Apply a style:

```xml  
<draw:SkiaLabel
    Style="{StaticResource SkiaLabelStyle}"
    Text="Simple Styled Label" />
```
Apply styles upon conditions:

```xml  
   <views:SkiaShape
    LockRatio="1"
    Type="Circle"
    WidthRequest="16">
    <views:SkiaControl.Styles>
        <views:ConditionalStyle
            State="Normal"
            Style="{x:StaticResource StyleCameraDot}" />
        <views:ConditionalStyle
            Condition="{Binding .}"
            Style="{x:StaticResource StyleCameraDotOn}" />
    </views:SkiaControl.Styles>

</views:SkiaShape>
```

Same as:

```xml  
   <views:SkiaShape
    Style="{StaticResource StyleCameraDot}"
    LockRatio="1"
    Type="Circle"
    WidthRequest="16">
    <views:SkiaControl.Styles>
        <views:ConditionalStyle
            Condition="{Binding .}"
            Style="{x:StaticResource StyleCameraDotOn}" />
    </views:SkiaControl.Styles>

</views:SkiaShape>
```
When the BindingContext (x:Boolean) is True the style `StyleCameraDotOn` will be applied, otherwise `StyleCameraDot` will be applied.

To apply styles upon states you will be using standart Maui *VisualStates* mechanism, or you can even have serveral states at the same time, every `SkiaControl` has a `string[]  States` bindable property to server this purpose:

```xml  
   <views:SkiaShape
    States="{Binding VisualStates}"
	LockRatio="1"
	Type="Circle"
	WidthRequest="16">
	<views:SkiaControl.Styles>
		<views:ConditionalStyle
			State="Normal"
			Style="{x:StaticResource StyleCameraDot}" />
		<views:ConditionalStyle
			State="IsOn"
			Style="{x:StaticResource StyleCameraDotOn}" />
	</views:SkiaControl.Styles>
```

### Hints

_todo_

For SkiaStack of type Row or Column avoid using 
Fill for children ?? that would require a second measurement pass.

## Maui Views

### `Canvas`

#### _Events_:

__`WillDraw`__ 

__`WillFirstTimeDraw`__ 

__`WasDrawn`__ 

#### _Methods_: 

__`TakeScreenShot(Action<SKImage> callback)`__ Takes screenshot on next draw. Passes an `SKImage`, can be null. If you need an `SKBitmap` use `SKBitmap.FromImage` on it.

#### _Properties_:

__`Surface`__ 


### `SkiaShell`

The usage is almost the same as the standard Maui Shell, 
with some extra features.

`SkiaShell` is derived from `FastShell` that uses Maui interfaces 
and implements methods for standard maui navigation, 
then adds features to be able to navigate inside the Canvas.

Some additional features to be mentioned are actions that can be executed for specific routes.
code example:

```csharp  
RegisterRoute("profile", typeof(ScreenUserProfile));

RegisterActionRoute("settings", () =>
{
    //select settings tab
    this.NavigationLayout.SelectedIndex = 4;
});

```

#### Usage

Please see the demo.

## Drawn Controls

### `SkiaControl`

Base drawn element, derived from Maui `Element` to assure basic Maui Xaml compatibility, could derive from a `BindableObject` if Maui would provide public interfaces for that matter.

#### _Properties_:

__`LockRatio`__ a numeric value that will be used to calculate the width when the height is set or vice versa. If it's above 0 the max value will be applied, if it's below 0 the min value will be applied. If it's 0 then the ratio will be ignored.

Example 1:
```xml  
  <draw:SkiaShape
                        LockRatio="1"
                        WidthRequest="40" />
```
HeightRequest wasn't specified but this control will request 40 by 40 pts.

Example 2:
```xml  
  <draw:SkiaShape
	LockRatio="-1"
	HeightRequest="30"
	WidthRequest="40" />
```
This control will request 30 by 30 pts.

### `SkiaScroll`

`SkiaScroll` is a scrollable container that supports virtualization and recycling of its children.

If you include a `SkiaLayout` inside a `SkiaScroll` only visible on screen items will be rendered.

If the include a `SkiaLayout` that uses `ItemTemplate` this combination will automatically become virtualized and you will get sort of a CollectionView with recycled cells at your disposal. It is a good practice to use it for long lists of items.

#### _Properties_:

__`Orientation`__ a value of type `ScrollOrientation` that can be `Vertical` or `Horizontal`.

__`FrictionScrolled`__  Use this to control how fast the scroll will decelerate. Values 0.1f - 0.3f are the best, default is 0.1f.

__`IgnoreWrongDirection`__  Will ignore gestures of the wrong direction, for example, if this Orientation is Horizontal will ignore gestures with vertical direction velocity. Might want to set it to true when you have a horizontal scroll inside a vertical scroll, this will let the parent scroll start scrolling vertically even if the gesture started inside its horizontal scroll child.

### `SkiaLayout`

`SkiaLayout` is a container that supports various layout types: `Absolute`, `Grid`, `Row`, `Column`, and others. 

It also supports virtualization and recycling of its children with `ItemTemplate` property.

Controls inside templated `SkiaLayout` can implement `ISkiaCell` interface to eventually receive information about their state:
* `OnAppearing`
* `OnDisapearing`
* `OnScrolled`

This lets one to create custom controls that can react to scrolling and other events with animations etc.

### `SkiaShape`

`SkiaShape` is a base class for all shapes. You could fill it, stroke, drop shadows, apply gradients, and even clip other controls with it.

### `SkiaImage`

`SkiaImage` is a control that renders images. It can't apply filters and transformations.



### `SkiaSvg`

`SkiaSvg` is a control that renders svg files. It can't tint the svg with a color or gradient, and apply some transforms to it.


### `SkiaLabel`

A multi-line label fighting for his place under the sun.

#### _Properties_:

__`FontWeight`__ a numeric value used in case you have properly registered your fonts to support weights. 
You can use your font the usual Maui way but in the case of custom font files used from resources you might want to register them, using the following example:
```csharp
.ConfigureFonts(fonts =>
{
   fonts.AddFont("Gilroy-Regular.ttf", "FontText", FontWeight.Regular);
   fonts.AddFont("Gilroy-Medium.ttf", "FontText", FontWeight.Medium);
});
```
Now if you set the `FontWeight` to `500` the control will use the `Gilroy-Medium.ttf` file.
This might come in very handy when your Figma design shows you to use this weight and you want just to pass it over to SkiaLabel.

 __`HorizontalTextAlignment`__  : 
 ```csharp
public enum DrawTextAlignment
{
	Start,
	Center,
	End,
	FillWords,
	FillWordsFull,
	FillCharacters,
	FillCharactersFull,
}
```


### `SkiaLottie`

`SkiaLottie` is a control that renders Lottie files. It can even tint some colors inside your animation!

### `SkiaRive`

Actually for Windows only, this plays and controls Rive animation files. Other platforms will be added soon, poke if you would like to help binding some c++;

### SkiaHoverMask

A control deriving from SkiaShape that can be used to create hover effects. 
It will render a mask over its children when hovered, think of it as an inverted shape.

### Docs under construction
 
