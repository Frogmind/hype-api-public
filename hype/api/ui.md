# UI

## API Reference

## find

Finds a UI for an entity or by name and returns a widget handle.

### Signature

```luau
hype.ui.find(entity: Entity): UIWidget
```

### Parameters
- name - object name containing a UI widget
- entity - entity whose object contains a UI widget; also searches direct children

### Notes
- Returns a UIWidget handle used to access children and properties
- Errors if no UI widget is found

## getUI

Deprecated alias for hype.ui.find.

### Signature

```luau
hype.ui.getUI(...): UIWidget
```

### Notes
- Deprecated: use hype.ui.find(...) instead

## createButton

Creates a Button widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createButton(): Button
```

## createText

Creates a Text widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createText(): Text
```

## createVerticalLayout

Creates a Vertical Layout widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createVerticalLayout(): Layout
```

## createHorizontalLayout

Creates a Horizontal Layout widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createHorizontalLayout(): Layout
```

## createWrappingLayout

Creates a Wrapping Layout widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createWrappingLayout(): Layout
```

## createBorder

Creates a Border panel widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createBorder(): Layout
```

## createScroller

Creates a Scroller widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createScroller(): Layout
```

## createProgressBar

Creates a ProgressBar widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createProgressBar(): ProgressBar
```

## createProgressCircle

Creates a ProgressCircle widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createProgressCircle(): ProgressCircle
```

## createTextArea

Creates a TextArea widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createTextArea(): TextArea
```

## createImage

Creates an Image widget under the root UI and returns its handle.

### Signature

```luau
hype.ui.createImage(): Image
```

## instantiate

Instantiates a saved UI from a UI component into the live UI.

### Signature

```luau
UIWidget:instantiate(): Layout
```

### Notes
- Returns the root Layout handle of the instantiated canvas
- Initializes default images and sets size by content

## findChild

Finds a direct or nested child widget by name, returning a typed handle.

### Signature

```luau
UIWidget:findChild(name: string): (Layout|Button|Text|ProgressBar|ProgressCircle|TextArea|Image)
```

### Parameters
- name - child widget name

### Notes
- Searches recursively under the widgetâ€™s root canvas
- Errors if the child is not found

## getLayout

Gets a Layout child by name.

### Signature

```luau
UIWidget:getLayout(name: string): Layout
```

## getButton

Gets a Button child by name.

### Signature

```luau
UIWidget:getButton(name: string): Button
```

## getText

Gets a Text child by name.

### Signature

```luau
UIWidget:getText(name: string): Text
```

## getProgressBar

Gets a ProgressBar child by name.

### Signature

```luau
UIWidget:getProgressBar(name: string): ProgressBar
```

## getProgressCircle

Gets a ProgressCircle child by name.

### Signature

```luau
UIWidget:getProgressCircle(name: string): ProgressCircle
```

## getTextArea

Gets a TextArea child by name.

### Signature

```luau
UIWidget:getTextArea(name: string): TextArea
```

## getImage

Gets an Image child by name.

### Signature

```luau
UIWidget:getImage(name: string): Image
```

## setVisible

Sets overall visibility of the UI component instance.

### Signature

```luau
UIWidget:setVisible(visible: boolean): ()
```

### Parameters
- visible - show or hide the whole UI

## getText

Gets the button text.

### Signature

```luau
Button:getText(): string
```

## getColor

Gets the button border color.

### Signature

```luau
Button:getColor(): vector4
```

## getPosition

Gets the button position.

### Signature

```luau
Button:getPosition(): vector
```

## getRotation

Gets the button rotation angle.

### Signature

```luau
Button:getRotation(): number
```

## getScale

Gets the button scale factor.

### Signature

```luau
Button:getScale(): number
```

## getSize

Gets the button size.

### Signature

```luau
Button:getSize(): vector
```

### Notes
- Z component is 0; use X/Y for width/height

## isEnabled

Checks whether the button is enabled (focusable).

### Signature

```luau
Button:isEnabled(): boolean
```

## isVisible

Checks whether the button is visible.

### Signature

```luau
Button:isVisible(): boolean
```

## setText

Sets the button text.

### Signature

```luau
Button:setText(text: string): ()
```

## setColor

Sets the button border color.

### Signature

```luau
Button:setColor(color: vector4): ()
```

## setPosition

Sets the button position.

### Signature

```luau
Button:setPosition(pos: vector): ()
```

## setPosition3D

Sets the 3D position of the button.

### Signature

```luau
Button:setPosition3D(pos: vector): ()
```

### Notes
- Not implemented yet

## move

Moves the button by a delta.

### Signature

```luau
Button:move(delta: vector): ()
```

## setRotation

Sets the button rotation angle.

### Signature

```luau
Button:setRotation(angle: number): ()
```

## setScale

Sets the button scale factor.

### Signature

```luau
Button:setScale(scale: number): ()
```

### Notes
- Internally preserves custom scale against touch scaling

## setSize

Sets the button size.

### Signature

```luau
Button:setSize(size: vector): ()
```

### Notes
- Uses X/Y components; values are clamped to >= 0

## setOpacity

Sets the button opacity.

### Signature

```luau
Button:setOpacity(opacity: number): ()
```

### Notes
- Clamped to [0,1]

## setEnabled

Enables or disables the button (focusable).

### Signature

```luau
Button:setEnabled(enabled: boolean): ()
```

## setTextColor

Sets the text color of the button.

### Signature

```luau
Button:setTextColor(color: vector4): ()
```

## setBorderColor

Sets the border color of the button.

### Signature

```luau
Button:setBorderColor(color: vector4): ()
```

## setVisible

Shows or hides the button.

### Signature

```luau
Button:setVisible(visible: boolean): ()
```

## setCollapsed

Collapses the button in its parent layout (no space when collapsed).

### Signature

```luau
Button:setCollapsed(collapsed: boolean): ()
```

## setMove3DIncludeFilter

Sets 3D move include collision group filter.

### Signature

```luau
Button:setMove3DIncludeFilter(groupMask: number): ()
```

## setMove3DIgnoreFilter

Sets 3D move ignore collision group filter.

### Signature

```luau
Button:setMove3DIgnoreFilter(groupMask: number): ()
```

## setPressedColor

Sets pressed-state color.

### Signature

```luau
Button:setPressedColor(color: vector4): ()
```

### Notes
- Not implemented yet

## setShape

Sets visual shape/background by name.

### Signature

```luau
Button:setShape(name: string): ()
```

## setBorderWidth

Sets border width.

### Signature

```luau
Button:setBorderWidth(width: number): ()
```

## setImage

Sets background image by name.

### Signature

```luau
Button:setImage(name: string): ()
```

## setTextMargin

Sets relative text margin inside the button.

### Signature

```luau
Button:setTextMargin(margin: number): ()
```

## setTransition

Sets show/hide transition.

### Signature

```luau
Button:setTransition(transition: string): ()
```

### Notes
- Expected: None/Fade/Zoom/Dramatic/Bounce/Chill/Fast

## setKeyboard1

Maps a keyboard/mouse primary button by name.

### Signature

```luau
Button:setKeyboard1(name: string): ()
```

### Notes
- Use values from ControllerSupport keyboard list

## setKeyboard2

Maps a keyboard/mouse secondary button by name.

### Signature

```luau
Button:setKeyboard2(name: string): ()
```

### Notes
- Use values from ControllerSupport keyboard list

## setController

Maps a gamepad button by name.

### Signature

```luau
Button:setController(name: string): ()
```

### Notes
- Use values from ControllerSupport gamepad list

## setPassTouchThrough

Allows touches to pass through to widgets below.

### Signature

```luau
Button:setPassTouchThrough(enabled: boolean): ()
```

## onStart

Subscribes to button press start.
})): Subscription

### Signature

```luau
Button:onStart(component: ComponentInstance, callback: function(component: ComponentInstance, event: { source: Button, touchId: number, x: number, y: number
```

## onEnd

Subscribes to button press end.
})): Subscription

### Signature

```luau
Button:onEnd(component: ComponentInstance, callback: function(component: ComponentInstance, event: { source: Button, touchId: number, x: number, y: number
```

## onMove

Subscribes to button move (2D touch).
})): Subscription

### Signature

```luau
Button:onMove(component: ComponentInstance, callback: function(component: ComponentInstance, event: { source: Button, touchId: number, x: number, y: number
```

## onMove3D

Subscribes to button move with 3D raycast info.
hit: table? })): Subscription

### Signature

```luau
Button:onMove3D(component: ComponentInstance, callback: function(component: ComponentInstance, event: { source: Button, touchId: number, x: number, y: number,
```

### Notes
- Performs a 3D raycast from the touch position; event.hit is provided on intersections

## remove

Removes the text widget and its children from UI.

### Signature

```luau
Text:remove(): ()
```

## setAlignment

Sets alignment inside parent layout.

### Signature

```luau
Button:setAlignment(alignment: string): ()
```

### Notes
- Expected: Left/Center/Right/Top/Bottom (depends on layout type)

## setHorizontalAlignment

Sets horizontal alignment in parent layout.

### Signature

```luau
Button:setHorizontalAlignment(alignment: string): ()
```

## setVerticalAlignment

Sets vertical alignment in parent layout.

### Signature

```luau
Button:setVerticalAlignment(alignment: string): ()
```

## setLeftMargin

Sets left margin in parent layout.

### Signature

```luau
Button:setLeftMargin(margin: number): ()
```

## setTopMargin

Sets top margin in parent layout.

### Signature

```luau
Button:setTopMargin(margin: number): ()
```

## setRightMargin

Sets right margin in parent layout.

### Signature

```luau
Button:setRightMargin(margin: number): ()
```

## setBottomMargin

Sets bottom margin in parent layout.

### Signature

```luau
Button:setBottomMargin(margin: number): ()
```

## setExpandRatio

Sets expand ratio in parent layout.

### Signature

```luau
Button:setExpandRatio(ratio: number): ()
```

## getText

Gets the text string.

### Signature

```luau
Text:getText(): string
```

## getColor

Gets the text color.

### Signature

```luau
Text:getColor(): vector4
```

## getPosition

Gets the position.

### Signature

```luau
Text:getPosition(): vector
```

## getRotation

Gets the rotation angle.

### Signature

```luau
Text:getRotation(): number
```

## getScale

Gets the scale factor.

### Signature

```luau
Text:getScale(): number
```

## getSize

Gets the size.

### Signature

```luau
Text:getSize(): vector
```

## isVisible

Checks whether the text is visible.

### Signature

```luau
Text:isVisible(): boolean
```

## setText

Sets the text string.

### Signature

```luau
Text:setText(text: string): ()
```

## setValue

Sets a numeric value to be displayed.

### Signature

```luau
Text:setValue(value: number): ()
```

### Notes
- Formatting depends on current text format

## setTime

Sets a time value to be displayed.

### Signature

```luau
Text:setTime(seconds: number): ()
```

## setColor

Sets the text color.

### Signature

```luau
Text:setColor(color: vector4): ()
```

## setPosition

Sets the position.

### Signature

```luau
Text:setPosition(pos: vector): ()
```

## setPosition3D

Sets the 3D position.

### Signature

```luau
Text:setPosition3D(pos: vector): ()
```

### Notes
- Not implemented yet

## move

Moves by a delta.

### Signature

```luau
Text:move(delta: vector): ()
```

## setRotation

Sets the rotation angle.

### Signature

```luau
Text:setRotation(angle: number): ()
```

## setScale

Sets the scale factor.

### Signature

```luau
Text:setScale(scale: number): ()
```

### Notes
- Internally preserves custom scale against touch scaling

## setSize

Sets the size.

### Signature

```luau
Text:setSize(size: vector): ()
```

### Notes
- Uses X/Y components; values are clamped to >= 0

## setOpacity

Sets the opacity.

### Signature

```luau
Text:setOpacity(opacity: number): ()
```

### Notes
- Clamped to [0,1]

## setVisible

Shows or hides the text.

### Signature

```luau
Text:setVisible(visible: boolean): ()
```

## setName

Sets the widget name.

### Signature

```luau
Text:setName(name: string): ()
```

## setTextSize

Sets the font size multiplier.

### Signature

```luau
Text:setTextSize(scale: number): ()
```

### Notes
- Clamped to [0.1, 3.0]

## setAutomaticWidth

Enables automatic width based on text contents.

### Signature

```luau
Text:setAutomaticWidth(enabled: boolean): ()
```

## setAutomaticHeight

Enables automatic height based on text contents.

### Signature

```luau
Text:setAutomaticHeight(enabled: boolean): ()
```

## setTextAlign

Sets text alignment.

### Signature

```luau
Text:setTextAlign(align: string): ()
```

### Notes
- Expected: Left/Center/Right

## setDecimals

Sets number of decimals when formatting numerical text.

### Signature

```luau
Text:setDecimals(decimals: integer): ()
```

## setFormat

Sets formatting mode.

### Signature

```luau
Text:setFormat(format: string): ()
```

### Notes
- Expected: Default/Time/Rounded/Rounded up/Rounded down/No formatting

## setShowTrailingZeroes

Shows or hides trailing zeroes in number formatting.

### Signature

```luau
Text:setShowTrailingZeroes(enabled: boolean): ()
```

## setOutline

Enables or disables an outline effect.

### Signature

```luau
Text:setOutline(enabled: boolean): ()
```

## setTransition

Sets show/hide transition.

### Signature

```luau
Text:setTransition(transition: string): ()
```

### Notes
- Expected: None/Fade/Zoom/Dramatic/Bounce/Chill/Fast

## setAlignment

Sets alignment inside parent layout.

### Signature

```luau
Text:setAlignment(alignment: string): ()
```

## setHorizontalAlignment

Sets horizontal alignment in parent layout.

### Signature

```luau
Text:setHorizontalAlignment(alignment: string): ()
```

## setVerticalAlignment

Sets vertical alignment in parent layout.

### Signature

```luau
Text:setVerticalAlignment(alignment: string): ()
```

## setLeftMargin

Sets left margin in parent layout.

### Signature

```luau
Text:setLeftMargin(margin: number): ()
```

## setTopMargin

Sets top margin in parent layout.

### Signature

```luau
Text:setTopMargin(margin: number): ()
```

## setRightMargin

Sets right margin in parent layout.

### Signature

```luau
Text:setRightMargin(margin: number): ()
```

## setBottomMargin

Sets bottom margin in parent layout.

### Signature

```luau
Text:setBottomMargin(margin: number): ()
```

## setExpandRatio

Sets expand ratio in parent layout.

### Signature

```luau
Text:setExpandRatio(ratio: number): ()
```

## setCollapsed

Collapses the widget in its parent layout.

### Signature

```luau
Text:setCollapsed(collapsed: boolean): ()
```

## getPosition

Gets the position.

### Signature

```luau
Layout:getPosition(): vector
```

## getRotation

Gets the rotation angle.

### Signature

```luau
Layout:getRotation(): number
```

## getScale

Gets the scale factor.

### Signature

```luau
Layout:getScale(): number
```

## getSize

Gets the size.

### Signature

```luau
Layout:getSize(): vector
```

## isVisible

Checks whether the layout is visible.

### Signature

```luau
Layout:isVisible(): boolean
```

## setPosition

Sets the position.

### Signature

```luau
Layout:setPosition(pos: vector): ()
```

## setPosition3D

Sets the 3D position.

### Signature

```luau
Layout:setPosition3D(pos: vector): ()
```

### Notes
- Not implemented yet

## move

Moves by a delta.

### Signature

```luau
Layout:move(delta: vector): ()
```

## setRotation

Sets the rotation angle.

### Signature

```luau
Layout:setRotation(angle: number): ()
```

## setScale

Sets the scale factor.

### Signature

```luau
Layout:setScale(scale: number): ()
```

## setSize

Sets the size.

### Signature

```luau
Layout:setSize(size: vector): ()
```

### Notes
- Uses X/Y components; values are clamped to >= 0

## setOpacity

Sets the opacity.

### Signature

```luau
Layout:setOpacity(opacity: number): ()
```

### Notes
- Clamped to [0,1]

## setVisible

Shows or hides the layout.

### Signature

```luau
Layout:setVisible(visible: boolean): ()
```

## setColor

Sets the panel color (Border layout only).

### Signature

```luau
Layout:setColor(color: vector4): ()
```

### Notes
- Applies to Border widget type

## setName

Sets the widget name.

### Signature

```luau
Layout:setName(name: string): ()
```

## setUseContentWidth

Sizes width to content (true/false).

### Signature

```luau
Layout:setUseContentWidth(enabled: boolean): ()
```

## setUseContentHeight

Sizes height to content (true/false).

### Signature

```luau
Layout:setUseContentHeight(enabled: boolean): ()
```

## setSpacing

Sets spacing between children (per layout type).

### Signature

```luau
Layout:setSpacing(spacing: number): ()
```

## setTransition

Sets show/hide transition.

### Signature

```luau
Layout:setTransition(transition: string): ()
```

### Notes
- Expected: None/Fade/Zoom/Dramatic/Bounce/Chill/Fast

## setXPadding

Sets horizontal padding for wrapping layouts.

### Signature

```luau
Layout:setXPadding(padding: number): ()
```

## setYPadding

Sets vertical padding for wrapping layouts.

### Signature

```luau
Layout:setYPadding(padding: number): ()
```

## setContentAlignment

Sets content alignment for wrapping layouts.

### Signature

```luau
Layout:setContentAlignment(align: string): ()
```

### Notes
- Expected: Left/Center/Right/BottomLeft/BottomCenter/BottomRight

## setRoundness

Sets corner roundness (Border layout only).

### Signature

```luau
Layout:setRoundness(roundness: number): ()
```

## setBorderWidth

Sets border width (Border layout only).

### Signature

```luau
Layout:setBorderWidth(width: number): ()
```

## setBorderColor

Sets border color (Border layout only).

### Signature

```luau
Layout:setBorderColor(color: vector4): ()
```

## setImage

Sets background image (Border layout only).

### Signature

```luau
Layout:setImage(name: string): ()
```

### Notes
- Name must match an atlas widget image definition

## setBlockTouches

Blocks touches on this panel (Border layout only).

### Signature

```luau
Layout:setBlockTouches(enabled: boolean): ()
```

## setClipToScreenBounds

Clips content to screen bounds when using 3D position (Border layout only).

### Signature

```luau
Layout:setClipToScreenBounds(enabled: boolean): ()
```

## setScrollAxis

Sets scroll axis (Scroller only).

### Signature

```luau
Layout:setScrollAxis(axis: string): ()
```

### Notes
- Expected: "X" or "Y"

## setAlignContentToEnd

Aligns scroller content to the end (bottom).

### Signature

```luau
Layout:setAlignContentToEnd(enabled: boolean): ()
```

## setPassTouchThrough

Allows touches to pass through to widgets below.

### Signature

```luau
Layout:setPassTouchThrough(enabled: boolean): ()
```

## setAlignment

Sets alignment inside parent layout.

### Signature

```luau
Layout:setAlignment(alignment: string): ()
```

## setHorizontalAlignment

Sets horizontal alignment in parent layout.

### Signature

```luau
Layout:setHorizontalAlignment(alignment: string): ()
```

## setVerticalAlignment

Sets vertical alignment in parent layout.

### Signature

```luau
Layout:setVerticalAlignment(alignment: string): ()
```

## setLeftMargin

Sets left margin in parent layout.

### Signature

```luau
Layout:setLeftMargin(margin: number): ()
```

## setTopMargin

Sets top margin in parent layout.

### Signature

```luau
Layout:setTopMargin(margin: number): ()
```

## setRightMargin

Sets right margin in parent layout.

### Signature

```luau
Layout:setRightMargin(margin: number): ()
```

## setBottomMargin

Sets bottom margin in parent layout.

### Signature

```luau
Layout:setBottomMargin(margin: number): ()
```

## setExpandRatio

Sets expand ratio in parent layout.

### Signature

```luau
Layout:setExpandRatio(ratio: number): ()
```

## setCollapsed

Collapses the layout in its parent layout.

### Signature

```luau
Layout:setCollapsed(collapsed: boolean): ()
```

## addChild

Adds a widget as a child of this layout.

### Signature

```luau
Layout:addChild(child: UIWidget): ()
```

### Notes
- If child already has a parent, it is reparented

## removeChild

Removes a child widget from this layout.

### Signature

```luau
Layout:removeChild(child: UIWidget): ()
```

## findChild

Finds a direct or nested child widget by name.

### Signature

```luau
Layout:findChild(name: string): UIWidget
```

## clear

Removes all child widgets from this layout.

### Signature

```luau
Layout:clear(): ()
```

## remove

Removes the layout and its subtree from UI.

### Signature

```luau
Layout:remove(): ()
```

## getValue

Gets current value.

### Signature

```luau
ProgressBar:getValue(): number
```

## getMaxValue

Gets maximum value.

### Signature

```luau
ProgressBar:getMaxValue(): number
```

## getPosition

Gets the position.

### Signature

```luau
ProgressBar:getPosition(): vector
```

## getRotation

Gets the rotation angle.

### Signature

```luau
ProgressBar:getRotation(): number
```

## getScale

Gets the scale factor.

### Signature

```luau
ProgressBar:getScale(): number
```

## getSize

Gets the size.

### Signature

```luau
ProgressBar:getSize(): vector
```

## isVisible

Checks whether the widget is visible.

### Signature

```luau
ProgressBar:isVisible(): boolean
```

## getBarColor

Gets bar color.

### Signature

```luau
ProgressBar:getBarColor(): vector4
```

## getBackgroundColor

Gets background color.

### Signature

```luau
ProgressBar:getBackgroundColor(): vector4
```

## getBorderColor

Gets border color.

### Signature

```luau
ProgressBar:getBorderColor(): vector4
```

## getBorderWidth

Gets border width.

### Signature

```luau
ProgressBar:getBorderWidth(): number
```

## getRoundness

Gets corner roundness.

### Signature

```luau
ProgressBar:getRoundness(): number
```

## setValue

Sets current value.

### Signature

```luau
ProgressBar:setValue(value: number): ()
```

## setMaxValue

Sets maximum value.

### Signature

```luau
ProgressBar:setMaxValue(value: number): ()
```

## setPosition

Sets the position.

### Signature

```luau
ProgressBar:setPosition(pos: vector): ()
```

## move

Moves by a delta.

### Signature

```luau
ProgressBar:move(delta: vector): ()
```

## setRotation

Sets the rotation angle.

### Signature

```luau
ProgressBar:setRotation(angle: number): ()
```

## setScale

Sets the scale factor.

### Signature

```luau
ProgressBar:setScale(scale: number): ()
```

## setSize

Sets the size.

### Signature

```luau
ProgressBar:setSize(size: vector): ()
```

## setOpacity

Sets the opacity.

### Signature

```luau
ProgressBar:setOpacity(opacity: number): ()
```

### Notes
- Clamped to [0,1]

## setVisible

Shows or hides the widget.

### Signature

```luau
ProgressBar:setVisible(visible: boolean): ()
```

## setBarColor

Sets bar color.

### Signature

```luau
ProgressBar:setBarColor(color: vector4): ()
```

## setBackgroundColor

Sets background color.

### Signature

```luau
ProgressBar:setBackgroundColor(color: vector4): ()
```

## setBorderColor

Sets border color.

### Signature

```luau
ProgressBar:setBorderColor(color: vector4): ()
```

## setBorderWidth

Sets border width.

### Signature

```luau
ProgressBar:setBorderWidth(width: number): ()
```

## setRoundness

Sets corner roundness.

### Signature

```luau
ProgressBar:setRoundness(roundness: number): ()
```

## setName

Sets widget name.

### Signature

```luau
ProgressBar:setName(name: string): ()
```

## setDirection

Sets fill direction.

### Signature

```luau
ProgressBar:setDirection(direction: string): ()
```

### Notes
- Expected values depend on implementation (e.g., LeftToRight)

## setBackgroundImage

Sets background image.

### Signature

```luau
ProgressBar:setBackgroundImage(name: string): ()
```

## setBarImage

Sets bar image.

### Signature

```luau
ProgressBar:setBarImage(name: string): ()
```

## setTransition

Sets show/hide transition.

### Signature

```luau
ProgressBar:setTransition(transition: string): ()
```

### Notes
- Expected: None/Fade/Zoom/Dramatic/Bounce/Chill/Fast

## remove

Removes the progress bar from UI.

### Signature

```luau
ProgressBar:remove(): ()
```

## setAlignment

Sets alignment inside parent layout.

### Signature

```luau
ProgressBar:setAlignment(alignment: string): ()
```

## setHorizontalAlignment

Sets horizontal alignment in parent layout.

### Signature

```luau
ProgressBar:setHorizontalAlignment(alignment: string): ()
```

## setVerticalAlignment

Sets vertical alignment in parent layout.

### Signature

```luau
ProgressBar:setVerticalAlignment(alignment: string): ()
```

## setLeftMargin

Sets left margin in parent layout.

### Signature

```luau
ProgressBar:setLeftMargin(margin: number): ()
```

## setTopMargin

Sets top margin in parent layout.

### Signature

```luau
ProgressBar:setTopMargin(margin: number): ()
```

## setRightMargin

Sets right margin in parent layout.

### Signature

```luau
ProgressBar:setRightMargin(margin: number): ()
```

## setBottomMargin

Sets bottom margin in parent layout.

### Signature

```luau
ProgressBar:setBottomMargin(margin: number): ()
```

## setExpandRatio

Sets expand ratio in parent layout.

### Signature

```luau
ProgressBar:setExpandRatio(ratio: number): ()
```

## setCollapsed

Collapses the widget in its parent layout.

### Signature

```luau
ProgressBar:setCollapsed(collapsed: boolean): ()
```

## getValue

Gets current value.

### Signature

```luau
ProgressCircle:getValue(): number
```

## getMaxValue

Gets maximum value.

### Signature

```luau
ProgressCircle:getMaxValue(): number
```

## getPosition

Gets the position.

### Signature

```luau
ProgressCircle:getPosition(): vector
```

## getRotation

Gets the rotation angle.

### Signature

```luau
ProgressCircle:getRotation(): number
```

## getScale

Gets the scale factor.

### Signature

```luau
ProgressCircle:getScale(): number
```

## getSize

Gets the size.

### Signature

```luau
ProgressCircle:getSize(): vector
```

## isVisible

Checks whether the widget is visible.

### Signature

```luau
ProgressCircle:isVisible(): boolean
```

## getBarColor

Gets bar color.

### Signature

```luau
ProgressCircle:getBarColor(): vector4
```

## getOutlineColor

Gets outline color.

### Signature

```luau
ProgressCircle:getOutlineColor(): vector4
```

## getOutlineThickness

Gets outline thickness.

### Signature

```luau
ProgressCircle:getOutlineThickness(): number
```

## getInnerRadius

Gets inner radius.

### Signature

```luau
ProgressCircle:getInnerRadius(): number
```

## getStartAngle

Gets start angle.

### Signature

```luau
ProgressCircle:getStartAngle(): number
```

## isClockwise

Gets direction flag (clockwise if true).

### Signature

```luau
ProgressCircle:isClockwise(): boolean
```

## setValue

Sets current value.

### Signature

```luau
ProgressCircle:setValue(value: number): ()
```

## setMaxValue

Sets maximum value.

### Signature

```luau
ProgressCircle:setMaxValue(value: number): ()
```

## setPosition

Sets the position.

### Signature

```luau
ProgressCircle:setPosition(pos: vector): ()
```

## move

Moves by a delta.

### Signature

```luau
ProgressCircle:move(delta: vector): ()
```

## setRotation

Sets the rotation angle.

### Signature

```luau
ProgressCircle:setRotation(angle: number): ()
```

## setScale

Sets the scale factor.

### Signature

```luau
ProgressCircle:setScale(scale: number): ()
```

## setSize

Sets the size.

### Signature

```luau
ProgressCircle:setSize(size: vector): ()
```

## setOpacity

Sets the opacity.

### Signature

```luau
ProgressCircle:setOpacity(opacity: number): ()
```

### Notes
- Clamped to [0,1]

## setVisible

Shows or hides the widget.

### Signature

```luau
ProgressCircle:setVisible(visible: boolean): ()
```

## setBarColor

Sets bar color.

### Signature

```luau
ProgressCircle:setBarColor(color: vector4): ()
```

## setOutlineColor

Sets outline color.

### Signature

```luau
ProgressCircle:setOutlineColor(color: vector4): ()
```

## setOutlineThickness

Sets outline thickness.

### Signature

```luau
ProgressCircle:setOutlineThickness(thickness: number): ()
```

## setInnerRadius

Sets inner radius.

### Signature

```luau
ProgressCircle:setInnerRadius(radius: number): ()
```

## setStartAngle

Sets start angle.

### Signature

```luau
ProgressCircle:setStartAngle(angle: number): ()
```

## setClockwise

Sets direction flag (clockwise when true).

### Signature

```luau
ProgressCircle:setClockwise(clockwise: boolean): ()
```

## setName

Sets widget name.

### Signature

```luau
ProgressCircle:setName(name: string): ()
```

## setTransition

Sets show/hide transition.

### Signature

```luau
ProgressCircle:setTransition(transition: string): ()
```

### Notes
- Expected: None/Fade/Zoom/Dramatic/Bounce/Chill/Fast

## remove

Removes the progress circle from UI.

### Signature

```luau
ProgressCircle:remove(): ()
```

## setAlignment

Sets alignment inside parent layout.

### Signature

```luau
ProgressCircle:setAlignment(alignment: string): ()
```

## setHorizontalAlignment

Sets horizontal alignment in parent layout.

### Signature

```luau
ProgressCircle:setHorizontalAlignment(alignment: string): ()
```

## setVerticalAlignment

Sets vertical alignment in parent layout.

### Signature

```luau
ProgressCircle:setVerticalAlignment(alignment: string): ()
```

## setLeftMargin

Sets left margin in parent layout.

### Signature

```luau
ProgressCircle:setLeftMargin(margin: number): ()
```

## setTopMargin

Sets top margin in parent layout.

### Signature

```luau
ProgressCircle:setTopMargin(margin: number): ()
```

## setRightMargin

Sets right margin in parent layout.

### Signature

```luau
ProgressCircle:setRightMargin(margin: number): ()
```

## setBottomMargin

Sets bottom margin in parent layout.

### Signature

```luau
ProgressCircle:setBottomMargin(margin: number): ()
```

## setExpandRatio

Sets expand ratio in parent layout.

### Signature

```luau
ProgressCircle:setExpandRatio(ratio: number): ()
```

## setCollapsed

Collapses the widget in its parent layout.

### Signature

```luau
ProgressCircle:setCollapsed(collapsed: boolean): ()
```

## getText

Gets the text.

### Signature

```luau
TextArea:getText(): string
```

## getColor

Gets the text color.

### Signature

```luau
TextArea:getColor(): vector4
```

## getPosition

Gets the position.

### Signature

```luau
TextArea:getPosition(): vector
```

## getRotation

Gets the rotation angle.

### Signature

```luau
TextArea:getRotation(): number
```

## getScale

Gets the scale factor.

### Signature

```luau
TextArea:getScale(): number
```

## getSize

Gets the size.

### Signature

```luau
TextArea:getSize(): vector
```

## isVisible

Checks whether the widget is visible.

### Signature

```luau
TextArea:isVisible(): boolean
```

## setText

Sets the text.

### Signature

```luau
TextArea:setText(text: string): ()
```

## setColor

Sets the text color.

### Signature

```luau
TextArea:setColor(color: vector4): ()
```

## setPosition

Sets the position.

### Signature

```luau
TextArea:setPosition(pos: vector): ()
```

## move

Moves by a delta.

### Signature

```luau
TextArea:move(delta: vector): ()
```

## setRotation

Sets the rotation angle.

### Signature

```luau
TextArea:setRotation(angle: number): ()
```

## setScale

Sets the scale factor.

### Signature

```luau
TextArea:setScale(scale: number): ()
```

## setSize

Sets the size.

### Signature

```luau
TextArea:setSize(size: vector): ()
```

## setOpacity

Sets the opacity.

### Signature

```luau
TextArea:setOpacity(opacity: number): ()
```

### Notes
- Clamped to [0,1]

## setVisible

Shows or hides the widget.

### Signature

```luau
TextArea:setVisible(visible: boolean): ()
```

## setName

Sets widget name.

### Signature

```luau
TextArea:setName(name: string): ()
```

## setTextSize

Sets font size multiplier.

### Signature

```luau
TextArea:setTextSize(scale: number): ()
```

## setTextAlign

Sets text alignment.

### Signature

```luau
TextArea:setTextAlign(align: string): ()
```

### Notes
- Expected: Left/Center/Right

## setTransition

Sets show/hide transition.

### Signature

```luau
TextArea:setTransition(transition: string): ()
```

### Notes
- Expected: None/Fade/Zoom/Dramatic/Bounce/Chill/Fast

## remove

Removes the text area from UI.

### Signature

```luau
TextArea:remove(): ()
```

## setAlignment

Sets alignment inside parent layout.

### Signature

```luau
TextArea:setAlignment(alignment: string): ()
```

## setHorizontalAlignment

Sets horizontal alignment in parent layout.

### Signature

```luau
TextArea:setHorizontalAlignment(alignment: string): ()
```

## setVerticalAlignment

Sets vertical alignment in parent layout.

### Signature

```luau
TextArea:setVerticalAlignment(alignment: string): ()
```

## setLeftMargin

Sets left margin in parent layout.

### Signature

```luau
TextArea:setLeftMargin(margin: number): ()
```

## setTopMargin

Sets top margin in parent layout.

### Signature

```luau
TextArea:setTopMargin(margin: number): ()
```

## setRightMargin

Sets right margin in parent layout.

### Signature

```luau
TextArea:setRightMargin(margin: number): ()
```

## setBottomMargin

Sets bottom margin in parent layout.

### Signature

```luau
TextArea:setBottomMargin(margin: number): ()
```

## setExpandRatio

Sets expand ratio in parent layout.

### Signature

```luau
TextArea:setExpandRatio(ratio: number): ()
```

## setCollapsed

Collapses the widget in its parent layout.

### Signature

```luau
TextArea:setCollapsed(collapsed: boolean): ()
```

## getColor

Gets the color.

### Signature

```luau
Image:getColor(): vector4
```

## getPosition

Gets the position.

### Signature

```luau
Image:getPosition(): vector
```

## getRotation

Gets the rotation angle.

### Signature

```luau
Image:getRotation(): number
```

## getScale

Gets the scale factor.

### Signature

```luau
Image:getScale(): number
```

## getSize

Gets the size.

### Signature

```luau
Image:getSize(): vector
```

## isVisible

Checks whether the widget is visible.

### Signature

```luau
Image:isVisible(): boolean
```

## setPixart

Sets Pixart content by name.

### Signature

```luau
Image:setPixart(name: string): ()
```

## setIcon

Sets a built-in icon by name.

### Signature

```luau
Image:setIcon(name: string): ()
```

## setProfilePicture

Sets a profile picture for a user.

### Signature

```luau
Image:setProfilePicture(userId: string): ()
```

## setColor

Sets the color.

### Signature

```luau
Image:setColor(color: vector4): ()
```

## setPosition

Sets the position.

### Signature

```luau
Image:setPosition(pos: vector): ()
```

## move

Moves by a delta.

### Signature

```luau
Image:move(delta: vector): ()
```

## setRotation

Sets the rotation angle.

### Signature

```luau
Image:setRotation(angle: number): ()
```

## setScale

Sets the scale factor.

### Signature

```luau
Image:setScale(scale: number): ()
```

## setSize

Sets the size.

### Signature

```luau
Image:setSize(size: vector): ()
```

## setOpacity

Sets the opacity.

### Signature

```luau
Image:setOpacity(opacity: number): ()
```

### Notes
- Clamped to [0,1]

## setVisible

Shows or hides the widget.

### Signature

```luau
Image:setVisible(visible: boolean): ()
```

## setName

Sets widget name.

### Signature

```luau
Image:setName(name: string): ()
```

## setTransition

Sets show/hide transition.

### Signature

```luau
Image:setTransition(transition: string): ()
```

### Notes
- Expected: None/Fade/Zoom/Dramatic/Bounce/Chill/Fast

## remove

Removes the image from UI.

### Signature

```luau
Image:remove(): ()
```

## setAlignment

Sets alignment inside parent layout.

### Signature

```luau
Image:setAlignment(alignment: string): ()
```

## setHorizontalAlignment

Sets horizontal alignment in parent layout.

### Signature

```luau
Image:setHorizontalAlignment(alignment: string): ()
```

## setVerticalAlignment

Sets vertical alignment in parent layout.

### Signature

```luau
Image:setVerticalAlignment(alignment: string): ()
```

## setLeftMargin

Sets left margin in parent layout.

### Signature

```luau
Image:setLeftMargin(margin: number): ()
```

## setTopMargin

Sets top margin in parent layout.

### Signature

```luau
Image:setTopMargin(margin: number): ()
```

## setRightMargin

Sets right margin in parent layout.

### Signature

```luau
Image:setRightMargin(margin: number): ()
```

## setBottomMargin

Sets bottom margin in parent layout.

### Signature

```luau
Image:setBottomMargin(margin: number): ()
```

## setExpandRatio

Sets expand ratio in parent layout.

### Signature

```luau
Image:setExpandRatio(ratio: number): ()
```

## setCollapsed

Collapses the widget in its parent layout.

### Signature

```luau
Image:setCollapsed(collapsed: boolean): ()
```
