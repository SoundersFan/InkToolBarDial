# Expander + InkToolbar + Surface Dial crash.

When we use a Surface Dial with an app that has a InkToolbar inside an Expander an exception is thrown as the InkToolbar is trying to show it's flyout.

Use this project to see the crash:

## Repro
### Prep:
1. Pair a [Surface Dial](https://www.microsoft.com/en-us/d/surface-dial/925r551sktgn?activetab=pivot:overviewtab) with your device.
2. Build and Debug (F5) the app in VS2022 (2019 will probably work too)

### Repro steps:
Note: do not expand the expander.

1. Press and hold a Surface Dial that is paired to the system in order to bring up the tool selector menu.
2. Rotate dial to highlight the Pen tool.
3. Press Dial to select the Pen tool
4. Press the Dial again. This should bring up the InkToolbar flyout.

### Result:
App crashes, with exception:

```
The parameter is incorrect.
This element is already associated with a XamlRoot, it cannot be associated with a different one until it is removed from the previous XamlRoot."
```

## Counter examples:

Replace the InkToolbar with any of the following declarations and the issue is not reproducable as there is no Pen tool available at step #2 in the repro steps.
``` XML
<InkToolbar
    VerticalAlignment="Top"
    HorizontalAlignment="Right"
    TargetInkCanvas="{x:Bind Canvas}" />
```
``` XML
<InkToolbar
    VerticalAlignment="Top"
    HorizontalAlignment="Right"
    TargetInkCanvas="{x:Bind Canvas}"
    InitialControls="PensOnly" />
```
``` XML
<InkToolbar
    VerticalAlignment="Top"
    HorizontalAlignment="Right"
    TargetInkCanvas="{x:Bind Canvas}"
    InitialControls="None" />
```