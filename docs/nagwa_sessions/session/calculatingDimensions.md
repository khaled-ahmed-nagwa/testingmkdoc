# Calculating Dimensions for a Responsive Layout

To accommodate the variations in screen sizes and maintain a consistent aspect ratio across all student devices while in session, we employ an algorithm to calculate the required dimensions. The `calculateDimensions` function plays a vital role in this process. It takes two parameters:

- `BuildContext`: This provides the necessary screen size information.
  
- `Orientation`: This helps adjust the dimensions based on portrait or landscape mode.

This method efficiently calculates and provides dimensions for various components, including margins, sidebar width, drawing area width, and content height. Its primary objective is to dynamically adjust these dimensions based on the screen size and orientation, ensuring a well-optimized layout and display on different devices and screen orientations.

## Algorithm Implementation
1. The method first determines the screen size (`A` and `B`) based on the provided `BuildContext` and `Orientation`.
2. It calculates `BOver18`, which is `B` divided by 18 and rounded down to the nearest integer.
3. If the calculated value of `A` is greater than or equal to `BOver18 * 32`, it proceeds with the following steps:
      1. Calculates `h3` as `BOver18 * 18`.
      2. Calculates `w1` as `(h3 / 9) * 12`.
      3. Calculates `w2` as `(h3 / 9) * 4`.
      4. Calculates the left margin (`lm`) as `(A - (w1 + w2))` divided by 2 and rounded up to the nearest integer.
      5. Calculates the right margin (`rm`) as `A - (w1 + w2 + lm)`.
      6. Sets the top and bottom margins (`tm` and `bm`) to 0.


4. If the above condition is not met, it follows these steps:
      1. Calculates `w1` as `(A / 32)` multiplied by 24 and rounded down to the nearest integer.
      2. Calculates `w2` as `(A / 32)` multiplied by 8 and rounded down to the nearest integer.
      3. Calculates `h3` as `((w1 + w2) / 16) * 9`.
      4. Calculates the left margin (`lm`) as `(A - (w1 + w2))` divided by 2 and rounded up to the nearest integer.
      5. Calculates the right margin (`rm`) as `A - (w1 + w2 + lm)`.
      6. Calculates the top margin (`tm`) as `(B - h3)` divided by 2 and rounded down to the nearest integer.
      7. Calculates the bottom margin (`bm`) as `B - (h3 + tm)`.
   
5. Return a new `Dimensions` object with the calculated margins, sidebar width (`w2`), drawing area width (`w1`), and content height (`h3`).


## Parameters Describtion 

<div style="text-align: center;">
    <table width="100%" style="max-width: 600px; margin: 0 auto; border-collapse: collapse;">   
    <tr>
        <th style="width: 40%; text-align: left;">Parameter</th>
        <th style="width: 60%; text-align: left;">Description</th>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">context</td>
        <td style="width: 60%; text-align: left;">is the context of the screen</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">orientation</td>
        <td style="width: 60%; text-align: left;">is the orientation of the screen</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">Dimensions</td>
        <td style="width: 60%; text-align: left;">is a class that contains the dimensions of the screen</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">margins</td>
        <td style="width: 60%; text-align: left;">is a map that contains the margins of the screen</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">sideBarWidth</td>
        <td style="width: 60%; text-align: left;">is the width of the sidebar</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">drawingAreaWidth</td>
        <td style="width: 60%; text-align: left;">is the width of the drawing area</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">contentHeight</td>
        <td style="width: 60%; text-align: left;">is the height of the content</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">A</td>
        <td style="width: 60%; text-align: left;">is the width of the screen</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">B</td>
        <td style="width: 60%; text-align: left;">is the height of the screen</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">BOver18</td>
        <td style="width: 60%; text-align: left;">is the height of the screen divided by 18</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">h3</td>
        <td style="width: 60%; text-align: left;">is the height of the content</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">w1</td>
        <td style="width: 60%; text-align: left;">is the width of the drawing area</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">w2</td>
        <td style="width: 60%; text-align: left;">is the width of the sidebar</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">lm</td>
        <td style="width: 60%; text-align: left;">is the left margin</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">rm</td>
        <td style="width: 60%; text-align: left;">is the right margin</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">tm</td>
        <td style="width: 60%; text-align: left;">is the top margin</td>
    </tr>
    <tr>
        <td style="width: 40%; text-align: left;">bm</td>
        <td style="width: 60%; text-align: left;">is the bottom margin</td>
    </tr>
</table>
</div>
---------------
## Code Implementation

??? tip "Dimensions Calculations Code"

    ```java 
    import 'dart:math';

    import 'package:flutter/cupertino.dart';

    class Dimensions {
    final Map<String, int> margins;

    final int sideBarWidth;

    final int drawingAreaWidth;

    final int contentHeight;

    final int toolbarHeight;

    final int slidesBarHeight;

    Dimensions({
        required this.margins,
        required this.sideBarWidth,
        required this.drawingAreaWidth,
        required this.contentHeight,
        required this.toolbarHeight,
        required this.slidesBarHeight,
    });
    }

    Dimensions calculateDimensions(BuildContext context, Orientation orientation) {
    late double A;
    late double B;
    if (orientation == Orientation.portrait) {
        B = MediaQuery.of(context).size.height;
        // width
        A = MediaQuery.of(context).size.width;
    } else {
        B = MediaQuery.of(context).size.height;
        A = MediaQuery.of(context).size.width;
    }

    const toolbarHeight = 100;

    final BOver18 = ((B - 200) / 18).floor();

    if (A >= BOver18 * 32) {
        print('A is greater');

        final contentHeight = BOver18 * 18;

        final slidesBarHeight = B - toolbarHeight - contentHeight;

        final drawingAreaWidth = (contentHeight / 9) * 12;

        final sideBarWidth = (contentHeight / 9) * 4;

        final lm = (A - (drawingAreaWidth + sideBarWidth)) ~/ 2;

        final rm = A - (drawingAreaWidth + sideBarWidth + lm);

        const tm = 0;

        const bm = 0;

        return Dimensions(
        margins: {
            'tm': tm,
            'lm': lm,
            'rm': rm.toInt(),
            'bm': bm,
        },
        sideBarWidth: sideBarWidth.toInt(),
        drawingAreaWidth: drawingAreaWidth.toInt(),
        contentHeight: contentHeight,
        toolbarHeight: toolbarHeight,
        slidesBarHeight: slidesBarHeight.toInt(),
        );
    }

    final drawingAreaWidth2 = (A / 32).floor() * 24;

    final sideBarWidth2 = (A / 32).floor() * 8;

    final contentHeight2 = ((drawingAreaWidth2 + sideBarWidth2) / 16) * 9;

    // screen height is the minimum of a, b

    final slidesBarHeight2 = A * 3 / 4 - (toolbarHeight + contentHeight2);

    final lm = (A - (drawingAreaWidth2 + sideBarWidth2)) ~/ 2;

    final rm = A - (drawingAreaWidth2 + sideBarWidth2 + lm);

    final tm = (B - (contentHeight2 + slidesBarHeight2 + toolbarHeight)) ~/ 2;

    final bm = B - (contentHeight2 + tm + slidesBarHeight2 + toolbarHeight);

    return Dimensions(
        margins: {
        'tm': tm,
        'lm': lm,
        'rm': rm.toInt(),
        'bm': bm.toInt(),
        },
        sideBarWidth: sideBarWidth2,
        drawingAreaWidth: drawingAreaWidth2,
        contentHeight: contentHeight2.toInt(),
        toolbarHeight: toolbarHeight,
        slidesBarHeight: slidesBarHeight2.toInt(),
    );
    }
    ```