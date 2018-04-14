+++
author = "Vashishtha Jogi"
categories = ["Programming"]
date = 2016-09-16T05:43:00Z
description = "So you are writing an app which has credit card entry form and you want to format the credit card numbers and expiry as xxxx-xxxx-xxxx-xxxx, xx/xx. How do you do that?"
draft = false
slug = "how-to-format-uitextfield-for-credit-card-input"
tags = ["Programming"]
title = "How to format UITextField for credit card input"

+++

So you are writing an app which has credit card entry form and you want to format the credit card numbers and expiry as xxxx-xxxx-xxxx-xxxx, xx/xx. How do you do that? Let’s first start with how can you pass your `UITextField` text to formatter (assume they exist for now, more on that in a while). Let’s say you have two UITextFields `creditCardNumberTextField` and `creditCardExpiryTextField`. The input in them needs to be formatted as an when any new input is done. So, setup triggers for that in `viewDidLoad`.

```objc
- (void)viewDidLoad
{
    [super viewDidLoad];
    [creditCardNumberTextField addTarget:self action:@selector(creditCardNumberFormatter:) forControlEvents:UIControlEventEditingChanged];
    [creditCardExpiryTextField addTarget:self action:@selector(creditCardExpiryFormatter:) forControlEvents:UIControlEventEditingChanged];
}

- (void)creditCardNumberFormatter:(id)sender {
    NSString *formattedText = [StringUtils formatCreditCard:self.creditCardNumberTextField.text]; // this is out formatter
    if (![formattedText isEqualToString:self.creditCardNumberTextField.text]) {
        self.creditCardNumberTextField.text = formattedText;
    }
    if (self.ccNumberTextField.text.length == 19) {
        [self.creditCardNumberTextField resignFirstResponder];
        [self.creditCardExpiryTextField becomeFirstResponder];
    }
}

- (void)creditCardExpiryFormatter:(id)sender {
    NSString *formattedText = [StringUtils formatCreditCardExpiry:self.creditCardExpiryTextField.text];
    if (![formattedText isEqualToString:self.ccExpiryTextField.text]) {
        self.ccExpiryTextField.text = formattedText;
    }
}
```

Let’s write the formatter now.

```objc
#import <Foundation/Foundation.h>

@interface StringUtils : NSObject

+ (NSString *)formatCreditCard:(NSString *)input;
+ (NSString *)formatCreditCardExpiry:(NSString *)input;
+ (NSString *)trimSpecialCharacters:(NSString *)input;

@end

@implementation StringUtils

+ (NSString *)formatCreditCard:(NSString *)input
{
    input = [[self class] trimSpecialCharacters:input];
    NSString *output;
    switch (input.length) {
        case 1:
        case 2:
        case 3:
        case 4:
            output = [NSString stringWithFormat:@"%@", [input substringToIndex:input.length]];
            break;
        case 5:
        case 6:
        case 7:
        case 8:
            output = [NSString stringWithFormat:@"%@-%@", [input substringToIndex:4], [input substringFromIndex:4]];
            break;
        case 9:
        case 10:
        case 11:
        case 12:
            output = [NSString stringWithFormat:@"%@-%@-%@", [input substringToIndex:4], [input substringWithRange:NSMakeRange(4, 4)], [input substringFromIndex:8]];
            break;
        case 13:
        case 14:
        case 15:
        case 16:
            output = [NSString stringWithFormat:@"%@-%@-%@-%@", [input substringToIndex:4], [input substringWithRange:NSMakeRange(4, 4)], [input substringWithRange:NSMakeRange(8, 4)], [input substringFromIndex:12]];
            break;
        default:
            output = @"";
            break;
    }
    return output;
}

+ (NSString *)formatCreditCardExpiry:(NSString *)input
{
    input = [[self class] trimSpecialCharacters:input];
    NSString *output;
    switch (input.length) {
        case 1:
        case 2:
            output = [NSString stringWithFormat:@"%@", [input substringToIndex:input.length]];
            break;
        case 3:
        case 4:
            output = [NSString stringWithFormat:@"%@/%@", [input substringToIndex:2], [input substringFromIndex:2]];
            break;
        default:
            output = @"";
            break;
    }
    return output;
}

+ (NSString *)trimSpecialCharacters:(NSString *)input
{
    NSCharacterSet *special = [NSCharacterSet characterSetWithCharactersInString:@"/+-() "];
    return [[input componentsSeparatedByCharactersInSet:special] componentsJoinedByString:@""];
}
```

The above code will properly format credit card numbers and expiry dates as you enter them in the textfield. There is one more thing that is still remaining. You want the input to stop when the input textfield has all the credit card numbers inputted or has the expiry inputted. That can be achieved by the following code:

```objc
- (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string
{
    if ([string isEqualToString:@""]) { // when backspace is hit
        return YES;
    }
    if (textField == self.creditCardNumberTextField) {
        if (textField.text.length > 18)
            return NO;
    } else if (textField == self.creditCardExpiryTextField) {
        if (textField.text.length > 4)
            return NO;
    }
    return YES;
}
```
