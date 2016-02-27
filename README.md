ValidatedTextInputLayout
========================

> Android library for text inputs with support for validation.
>> Extended from android design library's _TextInputLayout_.


## Demo ##
![Basic](./images/demo.gif)

## Features ##
 - **AutoValidation**  
 Validate the input field as the text changes.  
    `mInput.autoValidate(true);`
    If `false` you need to call the `validate()` method explicitly for validation.  
    OR  
    use xml attribute `autoValidate` as true or false.
 
 - **AutoTrim**  
 `mInput.getValue()` will return the trimmed value equivalent to `String.trim()` method    
    `mInput.autoTrimValue(true);`  
    OR  
    use xml attribute `autoTrim` as true or false.
    
 - **Add Validators**  
 You can add multiple validators to a single input field.  
     `mInput.addValidator(/* Your first Validator class goes here */);`  
     `mInput.addValidator(/* Your second Validator class goes here */);`  
 
 - **Clear Validators**  
 Removes all the validators associated with the input field.  
    `mInput.clearValidators();`  
    
 - **Default Available Validators**  
    + **RequiredValidator**  
    Validates the input field as required. i.e. empty value is not valid.  
        `mInput.addValidator(new RequiredValidator("Your error message"));`  
        OR  
        use xml attribute `isRequired` as true or false.  
        The default message will be "This field is required."  
        For custom message you can use xml attribute `requiredValidationMessage`
        
    + **LengthValidator**  
    Validates the input field for minimum and maximum length specified.  
        `mInput.addValidator(new LengthValidator(8 /* Max Length */, "Your error message"));`  
        `mInput.addValidator(new LengthValidator(4 /* Min Length */, *8 /* Max Length */, "Your error message"));`  
         OR  
         use xml attributes `minLength` and `maxLength` with default values being "zero" and "indefinite" respectively.  
         The default message will be one of following
         - The input must have length between "minLength" and "maxLength".
         - The input length must be greater than or equal to "minLength".
         - The input length must be less than or equal to "maxLength".  
         based on your values for `minLength` and `maxLength` attributes.  
         For custom message you can use xml attribute `lengthValidationMessage`
 
 - **Custom Validators**  
 You can create your own validators to use with ValidatedTextInputLayout just by extending the `BaseValidator` class.  
 You need to call the `super()` method with the desired message and override `isValid()` method to return true or false;    
 
 Example: Validator class to check if field value contains  character sequence "xyz"  
  
        public class MyValidator extends BaseValidator {
            public MyValidator(String pErrorMessage){
                super(pErrorMessage);
            }
            
            @Override
            public boolean isValid(String pText){
                return pText.contains("xyz");
            }
        }

## Usage ##
 - You can use and style it similar to **Android Design Library's** _TextInputLayout_  
 
        <ValidatedTextInputLayout
                         xmlns:validation="http://schemas.android.com/apk/res-auto"
                         android:id="@+id/username"
                         android:layout_width="match_parent"
                         android:layout_height="wrap_content"
                         validation:isRequired="true"
                         validation:autoTrim="true"
                         validation:requiredValidationMessage="Your custom error message here.">
                 
                         <EditText
                             android:layout_width="match_parent"
                             android:layout_height="wrap_content"
                             android:hint="Password"
                             android:inputType="textPassword"/>
        </ValidatedTextInputLayout>
                
        <ValidatedTextInputLayout
                 android:id="@+id/password"
                 android:layout_width="match_parent"
                 android:layout_height="wrap_content">
         
                 <EditText
                     android:layout_width="match_parent"
                     android:layout_height="wrap_content"
                     android:hint="Password"
                     android:inputType="textPassword"
                     validation:autoValidate="true"
                     validation:lengthValidationMessage="Your custom error message here."
                     validation:maxLength="8"
                     validation:minLength="4"/>
        </ValidatedTextInputLayout>

**Thanks for using :D**  