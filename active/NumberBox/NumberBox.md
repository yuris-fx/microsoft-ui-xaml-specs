# Number box

<!-- The purpose of this spec is to describe a new feature and
its APIs that make up a new feature in WinUI. -->

<!-- There are two audiences for the spec. The first are people
that want to evaluate and give feedback on the API, as part of
the submission process.  When it's complete
it will be incorporated into the public documentation at
docs.microsoft.com (http://docs.microsoft.com/uwp/toolkits/winui/).
Hopefully we'll be able to copy it mostly verbatim.
So the second audience is everyone that reads there to learn how
and why to use this API. -->

## Background
<!-- Use this section to provide background context for the new API(s) 
in this spec. -->

<!-- This section and the appendix are the only sections that likely
do not get copied to docs.microsoft.com; they're just an aid to reading this spec. -->

<!-- If you're modifying an existing API, included a link here to the
existing page(s) -->

<!-- For example, this section is a place to explain why you're adding this API rather than
modifying an existing API. -->

<!-- For example, this is a place to provide a brief explanation of some dependent
area, just explanation enough to understand this new API, rather than telling
the reader "go read 100 pages of background information posted at ...". -->


## Description
<!-- Use this section to provide a brief description of the feature.
For an example, see the introduction to the PasswordBox control 
(http://docs.microsoft.com/windows/uwp/design/controls-and-patterns/password-box). -->

Number box is a numerics only text control with support for validation, increment stepping, and computing inline calculations.

**Important APIs:** [NumberBox class](https://docs.microsoft.com/en-us/uwp/api/microsoft.ui.xaml.controls.numberbox) [TODO - generated with MSDN documentation on publication.]

## Is this the right control? 

Use a **NumberBox** to capture and display mathematical input. A **NumberBox** can also be enabled with basic calculator support to compute multiplication, division, addition, and subtraction across parenthetical order with standard operator precedence.

## Examples
<!-- Use this section to explain the features of the API, showing
example code with each description. The general format is: 
  feature explanation,
  example code
  feature explanation,
  example code
  etc.-->
  
<!-- Code samples should be in C# and/or C++/WinRT -->

<!-- As an example of this section, see the Examples section for the PasswordBox control 
(https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/password-box#examples). -->

### Create a simple NumberBox

XAML
```XAML
<NumberBox x:Name="EquationInputNumberBox" Header="Enter equation:" PlaceholderText="A + B * C" />
```

![](images/numberbox-placeholder-text.png)

### Enable calculation support

XAML
```XAML
<NumberBox x:Name="EquationInputNumberBox"
    Header="Enter equation:" 
    PlaceholderText="A + B * C" 
    AcceptsCalculation="True" />
```

![](images/numberbox-acceptscalculation.png)

### Add increment and decrement stepping

XAML
```XAML
<NumberBox x:Name="ItemQuantityNumberBox" 
    Header="Quantity"
    StepFrequency="2"
    SpinButtonPlacementMode="Inline"
    HyperDragEnabled="True" 
    HyperScrollEnabled="True" />
```

![](images/numberbox-spinnerbutton.png)

### Format display and output

XAML
```XAML
<NumberBox x:Name="PercentageNumberBox" 
    Header="Enter a percentage:"
    PlaceholderText="2/3" 
    MinMaxMode="WrapEnabled"
    MinValue="0"
    MaxValue="100" 
    AreLeadingZerosTrimmed="False"
    DecimalPrecision="5"
    DoesInputRound=False" />
```

## Remarks
<!-- Explanation and guidance that doesn't fit into the Examples section. -->

<!-- APIs should only throw exceptions in exceptional conditions; basically,
only when there's a bug in the caller, such as argument exception.  But if for some
reason it's necessary for a caller to catch an exception from an API, call that
out with an explanation either here or in the Examples -->

## API Notes
<!-- Option 1: Give a one or two line description of each API (type
and member), or at least the ones that aren't obvious
from their name.  These descriptions are what show up
in IntelliSense. For properties, specify the default value of the property if it
isn't the type's default (for example an int-typed property that doesn't default to zero.) -->

<!-- Option 2: Put these descriptions in the below API Details section,
with a "///" comment above the member or type. -->


## API Notes

### Notable Properties  

| Name | Description |
|:-:|:--|
| StepFrequency | Gets or sets the value part of a value range that steps should be created for. |

## API Details
<!-- The exact API, in MIDL3 format (https://docs.microsoft.com/en-us/uwp/midl-3/) -->

```c++ 
enum NumberBoxSpinButtonPlacementMode
{
    Hidden,
    Inline,
};

enum NumberBoxBasicValidationMode
{
    InvalidInputOverwritten,
    IconMessage,
    TextBlockMessage,
    Disabled,
};

enum NumberBoxMinMaxMode
{
    None,
    MinEnabled,
    MaxEnabled,
    MinAndMaxEnabled,
    WrapEnabled,
};

enum NumberBoxNumberRounder
{
    None,
    IncrementNumberRounder,
    SignificantDigitsNumberRounder,
};

runtimeclass NumberBoxValueChangingEventArgs
{
    Boolean IsContentChanging;
};

runtimeclass NumberBoxValueChangedEventArgs
{
    System.Windows.Controls.UndoAction Action;
    System.Collections.Generic.ICollection<System.Windows.Controls.ValueChange> Changes;
};

unsealed runtimeclass NumberBox : Windows.UI.Xaml.Controls.Control
{
    NumberBox();
   
    Double Value;
    
    NumberBoxBasicValidationMode BasicValidationMode;
    
    Boolean AcceptsCalculation;
    
    NumberBoxSpinButtonPlacementMode SpinButtonPlacementMode;
    Boolean HyperDragEnabled;
    Boolean HyperScrollEnabled;
    Double StepFrequency;
  
    Int IntegerDigits; 
    Int FractionDigits;
    Int SignificantDigits; 
    Boolean IsDecimalPointAlwaysDisplayed;
    Boolean IsZeroSigned;
    
    RoundingAlgorithm RoundingAlgorithm;
    NumberBoxNumberRounder NumberRounder; 
    Double IncrementPrecision;
    Int SignificantDigitPrecision;
    
    NumberBoxMinMaxMode MinMaxMode;
    Double MinValue;
    Double MaxValue;

    IconSource DecrementIcon;
    IconSource IncrementIcon;
    Windows.UI.Xaml.Style DecrementButtonStyle;
    Windows.UI.Xaml.Style IncrementButtonStyle;
    NumberBoxTemplateSettings TemplateSettings{ get; };

    event Windows.Foundation.TypedEventHandler<NumberBox, NumberBoxValueChangingEventArgs> ValueChanging;
    event Windows.Foundation.TypedEventHandler<NumberBox, NumberBoxValueChangedEventArgs> ValueChanged;

    static Windows.UI.Xaml.DependencyProperty ValueProperty{ get; };
    
    static Windows.UI.Xaml.DependencyProperty BasicValidationModeProperty{ get; };
    
    static Windows.UI.Xaml.DependencyProperty AcceptsCalculationProperty{ get; };
    
    static Windows.UI.Xaml.DependencyProperty SpinButtonPlacementModeProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty HyperDragEnabledProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty HyperScrollEnabledProperty{ get; };   
    static Windows.UI.Xaml.DependencyProperty StepFrequencyProperty{ get; };

    static Windows.UI.Xaml.DependencyProperty IntegerDigitsProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty FractionDigitsProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty SignificantDigitsProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty IsDecimalPointAlwaysDisplayedProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty IsZeroSignedProperty{ get; };
    
    static Windows.UI.Xaml.DependencyProperty RoundingAlgorithmProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty NumberRounderProperty{ get; }; 
    static Windows.UI.Xaml.DependencyProperty IncrementPrecisionProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty SignificantDigitPrecisionProperty{ get; };
    
    static Windows.UI.Xaml.DependencyProperty MinMaxModeProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty MinValueProperty{ get; };
    static Windows.UI.Xaml.DependencyProperty MaxValueProperty{ get; };
}
```

## Appendix
<!-- Anything else that you want to write down for posterity, but 
that isn't necessary to understand the purpose and usage of the API.
For example, implementation details. -->

### Behavioral Components

| Property | Notes |
|:---:|:---|
| InputScope | "Number" will be used for the InputScope. This may be overwritten by the developer but alternative InputScope types will not be explicitly supported. | 
| AcceptsCalculation | NumberBox will provide computation support for multiplication, division, addition, and subtraction across parenthetical order with standard operator precedence; i.e., [ 0-9()+-/* ] |
| Validation | * If BasicValidationMode="Disabled", no automatic validation will occur. This setting allows developers to configure custom validation via [Input Validation]( https://github.com/microsoft/microsoft-ui-xaml-specs/blob/user/lucashaines/inputvalidation/active/InputValidation/InputValidation.md). <br><br> * If BasicValidationMode="TextBlockMessage" or BasicValidationMode="IconMessage", input that is outside the bounds of MinValue/MaxValue or non-numerical/formulaic will trigger a validation warning consistent with [Input Validation]( https://github.com/microsoft/microsoft-ui-xaml-specs/blob/user/lucashaines/inputvalidation/active/InputValidation/InputValidation.md). A MinValue error will display "Minimum is [MinValue]." A MaxValue error will display "Maximum is [MaxValue]." Input errors will display "Only use numbers and ()+-/* ." Division by zero will return "Division by 0 unsupported." <br><br> * If BasicValidationMode="InvalidInputOverwritten", input that is non-numerical/formulaic will automatically be overwritten with the last legal value. Input that is stepped outside the bounds of MinValue/MaxValue will be coerced to the respective bound. Manually entered input that is outside outside the bounds of MinValue/MaxValue will be reverted to the last valid input. |
| Events | * Loss of focus, "Enter", and stepping [SEE API NOTES > SPINBUTTON && HYPER SCROLL && HYPER DRAG && KEYBOARD STEPPING] will trigger evalution. <br><br> * When Text (derived from TextBox) is changed by codebehind or user input on the evaluation triggers noted above, the TextChanging event will be fired. After, if BasicValidationEnabled="True", validation will be performed [See API NOTES > VALIDATION]. Text will then be updated and the TextChanged event will be fired. Text will then be converted to a Double and the ValueChanging event event will be fired. After, Value will be updated and the ValueChanged event will be fired. <br><br> * When Value is changed by codebehind, the ValueChanging event will be fired. After, if BasicValidationEnabled="True", validation will be performed [See API NOTES > VALIDATION]. Value will then be updated and the ValueChanged event will be fired. Value will then be converted to a String and the TextChanging event event will be fired.  After, Text will be updated and the TextChanged event will be fired. <br><br> * Requesting Value will forcibly trigger calculation. If Value is in an error state (NumberBoxBasicValidationMode != InvalidInputOverwritten), return Double.NaN (as Null can have meaning). |
| SpinButton | * If a calculation is stepped, it will be calculated before the step is applied. <br><br> SpinButton will disable increment/decrement components when at MaxValue/MinValue, respectively. |
| Hyper Scroll | * Focus and hover required for hyper scroll behavior to take place as to not reduce quality of experience on scrollable surfaces. <br><br> * If a calculation is stepped, it will be calculated before the step is applied.|
| Hyper Drag | * Align to WinRT XAML Toolkit's NumericUpDown implementation. <br><br> * If a calculation is stepped, it will be calculated before the step is applied. |
| Keyboard Stepping | * Up and Down arrow keys will increment and decrement the Text/Value when NumberBox is in focus. <br><br> * If a calculation is stepped, it will be calculated before the step is applied. |

### Inputs and Accessibility

#### UI Automation Patterns 

#### Keyboard Navigation 
| State | Action |
|:---|:---|
| Focus is on item in tab stop order before NumberBox | Tab moves focus into NumberBox's editable text field. |
| Focus is on NumberBox's editable text field. | Tab triggers evaluation and moves focus to validation error message if one is returned. Otherwise, tab moves focus to SpinButton (Decrement). |
| Focus is on NumberBox's validation error message. | Tab moves focus to NumberBox's SpinButton (Decrement). |
| Focus is on NumberBox's SpinButton (Decrement). | Tab moves focus to SpinButton (Increment). |
| Focus is on NumberBox's SpinButton (Increment). | Tab moves focus out of NumberBox and to the next item in the tab stop order. |

#### Narrator

| State | Action |
|:---|:---|
| Focus is moved to NumberBox's editable text field. | AutomationProperty.Name, Header, and Text properties are read. |
| Evaluation is triggered. | Evaluation is announced. |
| Validation Error Message is returned. | Error message is announced. |
| Focus is moved to NumberBox's validation error message. | Error message is announced. |
| Focus is moved to NumberBox's SpinButton (Decrement). | Property name is announced. |
| Focus is moved to NumberBox's SpinButton (Increment). | Property name is announced.  |


#### Gamepad  

| State | Action |
|:---|:---|
| Focus is near NumberBox | Spatial navigation may be used to access NumberBox where NumberBox's editable text field first receives focus. |
| Focus is on NumberBox's editable text field. | Spatial navigation: <br> Spatial navigation will navigate between the SpinButton, the editable textfield, or away from NumberBox. <br><br> A: <br> Will enter input mode. Calculation will be triggered on exit of input mode. <br><br> B (while in input mode): <br> Will trigger evaluation and exit input mode. |
| Focus is on NumberBox's SpinButton (Decrement). | Spatial navigation: <br> Spatial navigation will navigate between the SpinButton, the editable textfield, or away from NumberBox. <br><br> A: <br> Invoke decrement SpinButton action. |
| Focus is on NumberBox's SpinButton (Increment). | Spatial navigation: <br> Spatial navigation will navigate between the SpinButton, the editable textfield, or away from NumberBox. <br><br> A: <br> Invoke increment SpinButton action. |

### Data and Intelligence Metrics
##### P0: Feature Key Performance Indicators

Feature has received enough app/developer validation and feedback for it to exit preview.

* KPI: Three or more first party applications are validating the feature in prerelease.
    * Measurement: Occurrence of NumberBox type in apps on developer devices via telemetry (running under debugger). **Note for telemetry sampling considerations:** Need to be cautious for WinUI as it does not work the same way as with OS SDK. If the solution is not carefully considered, it will result in too little dev data (at 2% sampling) or too much end-user data (at 100% sampling) and hence throttling (telemetry data loss). Requires further investigation. 
    * Measurement: Count of users providing feedback on GitHub/UserVoice/Feedback Hub/SIUF.
    
Developers feel delighted and satisfied with the feature. 

* KPI: Dev NSAT is positive (min), >20 (aspirational) as we exit 2019.
    * Measurement: Developer survey via SIUF, e.g.: "How useful is the feature?"
    
##### P1: Feature Performance Indicators

Calculation support is leveraged by developers + appropriately surfaced to end users. 

* KPI: ~4% of unique instances of NumberBox surface an equation evaluation. 
    * Measurement: Ratio of occurances of NumberBox triggering evaluations compared to total count of NumberBox instances. 
    
##### P2+: Trailing Indicators

N/A

## Open Questions

* Is there value in creating a preview for calculation results? @mdtauk created a few example visualizations: 

![NumberBox with a tool tip above to show a preview of the calculation results](https://user-images.githubusercontent.com/16964652/58919441-fbfe7900-86e2-11e9-8d2b-dd4dadfa74c5.png)

![NumberBox with a calculation in progress and highlight text previewing the calculation results](https://user-images.githubusercontent.com/7389110/58920708-5b807700-872b-11e9-9924-21a7b7d37e68.png)

* Can touch/virtual keyboards intelligently adapt to numeral-formulaic input?
