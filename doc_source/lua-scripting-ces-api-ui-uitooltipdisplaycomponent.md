# UITooltipDisplayComponent<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent"></a>

Controls the display behavior of a tooltip\.

## UiTooltipDisplayBus<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus"></a>

Services messages for the `UiTooltipDisplayComponent`\.

### GetAutoPosition<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-getautoposition"></a>

Returns whether the tooltip display element is auto positioned\.

**Syntax**

```
bool GetAutoPosition()
```

### GetAutoPositionMode<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-getautopositionmode"></a>

Returns the auto position mode\.

**Syntax**

```
eUiTooltipDisplayAutoPositionMode GetAutoPositionMode()
```

Following are possible values for `eUiTooltipDisplayAutoPositionMode`\.

```
enum eUiTooltipDisplayAutoPositionMode
    {
        eUiTooltipDisplayAutoPositionMode_OffsetFromMouse,
        eUiTooltipDisplayAutoPositionMode_OffsetFromElement
    };
```

### GetAutoSize<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-getautosize"></a>

Returns whether the tooltip display element should be resized so that the text element size matches the size of the string\.

**Syntax**

```
bool GetAutoSize()
```

### GetDelayTime<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-getdelaytime"></a>

Returns the amount of time to wait before showing the tooltip display element after hover start\.

**Syntax**

```
float GetDelayTime()
```

### GetDisplayTime<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-getdisplaytime"></a>

Returns the amount of time the tooltip display element is to remain visible\.

**Syntax**

```
float GetDisplayTime()
```

### GetOffset<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-getoffset"></a>

Returns the offset from the tooltip display element's pivot to the mouse position\.

**Syntax**

```
const AZ::Vector2& GetOffset()
```

### GetTextEntity<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-gettextentity"></a>

Returns the entity ID of the text element that is used for resizing\.

**Syntax**

```
AZ::EntityId GetTextEntity()
```

### SetAutoPosition<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-setautoposition"></a>

Sets whether the tooltip display element is auto positioned\.

**Syntax**

```
void SetAutoPosition(bool autoPosition)
```

### SetAutoPositionMode<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-setautopositionmode"></a>

Sets the auto position mode\.

**Syntax**

```
void SetAutoPositionMode(eUiTooltipDisplayAutoPositionMode autoPositionMode)
```

For possible values for `eUiTooltipDisplayAutoPositionMode`, see [GetAutoPositionMode](#lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-getautopositionmode)\.

### SetAutoSize<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-setautosize"></a>

Sets whether the tooltip display element should be resized so that the text element size matches the size of the string\.

**Syntax**

```
void SetAutoSize(bool autoSize)
```

### SetDelayTime<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-setdelaytime"></a>

Sets the amount of time to wait before showing the tooltip display element after hover start\.

**Syntax**

```
void SetDelayTime(float delayTime)
```

### SetDisplayTime<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-setdisplaytime"></a>

Sets the amount of time the tooltip display element is to remain visible\.

**Syntax**

```
void SetDisplayTime(float displayTime)
```

### SetOffset<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-setoffset"></a>

Sets the offset from the tooltip display element's pivot to the mouse position\.

**Syntax**

```
void SetOffset(const AZ::Vector2& offset)
```

### SetTextEntity<a name="lua-scripting-ces-api-ui-uitooltipdisplaycomponent-uitooltipdisplaybus-settextentity"></a>

Sets the entity ID of the text element that is used for resizing\. The text element must be a child of this entity\.

**Syntax**

```
void SetTextEntity(AZ::EntityId textEntity)
```