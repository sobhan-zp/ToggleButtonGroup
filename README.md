# ToggleButtonGroup

[![API](https://img.shields.io/badge/API-15%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=15)

A group of toggle buttons, supports multiple / single selection.

## Gradle

```
dependencies {
    compile 'com.nex3z:toggle-button-group:0.2.1'
}
```

## MultiSelectToggleGroup

You can create a group of multiple selection toggle buttons with `MultiSelectToggleGroup`.

<div align="center">
  <img src="images/multi.gif" height="75" />
</div>

Define the `MultiSelectToggleGroup` as follows:

```xml
<com.nex3z.togglebuttongroup.MultiSelectToggleGroup
    android:id="@+id/multi_selection_group"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:textSize="16sp"
    android:textColor="@color/selector_text"
    android:saveEnabled="true"
    app:textButtons="@array/weekdays"
    app:flow="false"
    app:buttonSpacing="auto"
    app:animationType="scale"/>
```

Use `textColor` attribute to set text colors. Use a selector to specify text colors for checked and unchecked state. The `@color/selector_text` are defined as follows:

```xml
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_checked="true" android:color="#ffffff" />
    <item android:color="#000000" />
</selector>
```

Use `textButtons` attribute to add buttons with the text from the specified string array. The `@array/weekdays` are defined as follows:

```xml
<resources>
    <string-array name="weekdays">
        <item>S</item>
        <item>M</item>
        <item>T</item>
        <item>W</item>
        <item>T</item>
        <item>F</item>
        <item>S</item>
    </string-array>
</resources>
```

Use `flow` attribute to specify whether to allow button flow to next row. `false` means that all buttons are restricted in one row.

Use `buttonSpacing` attribute to config the horizontal spacing between buttons. `auto` means that the actual spacing is calculated according to the width and the number of the child views in the row, so that the child views are placed evenly.

## SingleSelectToggleGroup

You can create a group of single selection toggle buttons with `SingleSelectToggleGroup`.

<div align="center">
  <img src="images/single.gif" height="75" />
</div>

Define the `SingleSelectToggleGroup` as follows:

```xml
<com.nex3z.togglebuttongroup.SingleSelectToggleGroup
    android:id="@+id/single_selection_group"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:textSize="16sp"
    android:textColor="@color/selector_text"
    android:saveEnabled="true"
    app:flow="false"
    app:buttonSpacing="8dp"
    app:animationType="scale"/>
```

You can alwo use `setButtons(List<String> texts)` to add buttons to the group:

```java
SingleSelectToggleGroup singleSelect = (SingleSelectToggleGroup) findViewById(R.id.single_selection_group);
List<String> choices = Arrays.asList("A", "B", "C", "D");
singleSelect.setButtons(choices);
```

For both `MultiSelectToggleGroup` and `SingleSelectToggleGroup`, `getCheckedPositions()` will get the checked buttons' positions.

## Flow Buttons to Next Row

<div align="center">
  <img src="images/tags.gif"/>
</div>

```xml
<com.nex3z.togglebuttongroup.MultiSelectToggleGroup
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:textSize="16sp"
    android:textColor="@color/selector_text"
    app:buttonHeight="40dp"
    app:buttonWidth="wrap_content"
    app:textButtons="@array/dummy_text"
    app:buttonTextPaddingLeft="16dp"
    app:buttonTextPaddingRight="16dp"
    app:checkedBackground="@drawable/round_rect_checked_bg"
    app:buttonBackground="@drawable/round_rect_button_bg"
    app:flow="true"
    app:buttonSpacing="auto"
    app:rowSpacing="8dp"
    app:animationType="alpha" />
```

With `flow` attribute set to `true`, buttons are allowed to flow to next row when there is no enough space in current row. With `buttonSpacing` set to `auto`, buttons are evenly placed in each row. The background and checked state image are provided by `buttonBackground` and `checkedBackground`.

For more detail, please check the provided [sample](https://github.com/nex3z/ToggleButtonGroup/tree/master/sample).

## Listeners

### OnCheckedChangeListener

Use `OnCheckedChangeListener` to listen to any button's checked state.

```java
singleSelect.setOnCheckedChangeListener(new ToggleButtonGroup.OnCheckedChangeListener() {
    @Override
    public void onCheckedChange(int position, boolean isChecked) {
        // ...
    }
});
```

### OnCheckedPositionChangeListener

You can also use `OnCheckedPositionChangeListener` to retrieve all checked buttons' positions when there is any change, which is more handy for `MultiSelectToggleGroup`.

```java
multiSelect.setOnCheckedPositionChangeListener(new ToggleButtonGroup.OnCheckedPositionChangeListener() {
    @Override
    public void onCheckedPositionChange(Set<Integer> checkedPositions) {
        //...
    }
});

```

## Customization

The toggle button group can be customized with the following attributes.

| Attribute                   | Format                                          | Description                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------|-------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| android:textSize            | dimension                                       | Size of the text.                                                                                                                                                                                                                                                                                                                                                                                         |
| android:textColor           | reference/color                                 | Text color. May be a reference (such as a selector with text color for checked and unchecked state) or a solid color.                                                                                                                                                                                                                                                                                     |
| android:saveEnabled         | boolean                                         | Controls whether the saving of this view's state is enabled. The default is false, which disables state saving while recreating.                                                                                                                                                                                                                                                                          |
| app:textButtons             | reference                                       | The string array resource to find the value for buttons' text                                                                                                                                                                                                                                                                                                                                             |
| app:checkedTextColor        | color                                           | Color of the text when the button is checked, if you don't want to use `textColor` with selector.                                                                                                                                                                                                                                                                                                         |
| app:uncheckedTextColor      | color                                           | Color of the text when the button is unchecked, if you don't want to use `textColor`.                                                                                                                                                                                                                                                                                                                     |
| app:checkedBackground       | reference                                       | Sets a drawable resource as the background image for checked state, which is shown when the button is checked and hidden when unchecked.                                                                                                                                                                                                                                                                  |
| app:buttonBackground        | reference                                       | Sets a drawable resource as the button background, which is always shown in both checked and unchecked state.                                                                                                                                                                                                                                                                                             |
| app:animationType           | `none`/`scale`/`alpha`                          | `none` for disabling animation. `scale` / `alpha` for scale / alpha animation.                                                                                                                                                                                                                                                                                                                            |
| app:animationDuration       | integer                                         | Sets the duration of the animation for toggling button in milliseconds. The default is 150 milliseconds.                                                                                                                                                                                                                                                                                                  |
| app:buttonWidth             | `match_parent`/<br>`wrap_content`/<br>dimension | The width of the button.                                                                                                                                                                                                                                                                                                                                                                                  |
| app:buttonHeight            | `match_parent`/<br>`wrap_content`/<br>dimension | The height of the button.                                                                                                                                                                                                                                                                                                                                                                                 |
| app:buttonSpacing           | `auto`/dimension                                | The horizontal spacing between child views. Either `auto`, or a fixed size. `auto` means that buttons are placed evenly in each row.                                                                                                                                                                                                                                                                      |
| app:buttonSpacingForLastRow | `auto`/`align`/<br>dimension                    | The horizontal spacing between buttons of the last row. Either `auto`, `align` or a fixed size. `auto` means that buttons are placed evenly in each row. `align` means that the horizontal spacing of the buttons in the last row keeps the same with the spacing used in the row above. If there is only one row, this value is ignored and the spacing will be calculated according to `buttonSpacing`. |
| app:rowSpacing              | `auto`/dimension                                | The vertical spacing between rows. Either `auto`, or a fixed size. `auto` means that the rows are placed evenly in vertical.                                                                                                                                                                                                                                                                              |
| app:flow                    | boolean                                         | `true` to allow flow. `false` to restrict all child views in one row.                                                                                                                                                                                                                                                                                                                                     |
| app:buttonTextPaddingTop    | dimension                                       | The top padding of the text in the button.                                                                                                                                                                                                                                                                                                                                                                |
| app:buttonTextPaddingBottom | dimension                                       | The bottom padding of the text in the button.                                                                                                                                                                                                                                                                                                                                                             |
| app:buttonTextPaddingLeft   | dimension                                       | The left padding of the text in the button.                                                                                                                                                                                                                                                                                                                                                               |
| app:buttonTextPaddingRight  | dimension                                       | The right padding of the text in the button.                                                                                                                                                                                                                                                                                                                                                              |

## Licence

```
Copyright 2016 nex3z

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
