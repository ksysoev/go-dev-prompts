Please write GoDoc documentation for the following GoLang function. Adhere to the guidelines below to ensure the documentation is comprehensive and follows best practices.

Guidelines:
1. Function Description:
   - Start with the Function Name: Begin the comment with the function name.
   - Describe Functionality: Provide a brief description (1-3 sentences) of what the function does, using present tense and third person.
2. Parameters:
   - List Each Parameter: For each parameter, mention the name and its type.
   - Describe Purpose: Provide a concise explanation of the purpose of each parameter only if the purpose is not clear from the function signature.
3. Return Values:
   - List Return Types: For each return value, specify its type.
   - Describe Purpose: Explain what each return value represents.
4. Error Handling:
   - Describe Error Conditions: If the function returns an error, outline the conditions under which errors are returned.
   - Use Clear Language: Ensure the description of error conditions is clear and specific.
5. Edge Cases & Special Behavior:
   - Highlight Edge Cases: Mention any edge cases or special behaviors the function handles.
   - Explain Handling: Describe how the function behaves in these scenarios.
6. Formatting:
   - Maintain Proper Formatting: Ensure the documentation follows GoDoc formatting conventions.
   - Use Markdown Properly: Utilize Markdown syntax for code blocks and lists where appropriate.

Expected Format:
```
// FunctionName performs [brief description of what the function does].
// It takes [parameter1] of type [type1] and [parameter2] of type [type2] as inputs.
// It returns [return1] of type [type1], which [description of return1],
// and [return2] of type [type2], which [description of return2].
// It returns an error if [condition leading to error].

[Provided code unchanged]
```

Example Documentation:
```
// Divide divides the numerator by the denominator and returns the result.
// It takes two parameters: numerator of type float64 and denominator of type float64.
// It returns a float64 which is the quotient of numerator divided by denominator.
// It returns an error if the denominator is zero.
func Divide(numerator float64, denominator float64) (float64, error) {
    if denominator == 0 {
        return 0, fmt.Errorf("denominator cannot be zero")
    }
    return numerator / denominator, nil
}
```

Instructions:

- Replace Placeholders: Substitute [brief description of what the function does], [parameter1], [type1], etc., with the actual descriptions, parameter names, and types from the provided function.
- Ensure Clarity: Make sure the descriptions are clear, concise, and free from redundancy.
- Maintain Consistency: Follow GoDoc conventions for capitalization, punctuation, and formatting.
- Include Only Relevant Information: Focus on behavior that is important to user of the function, and omit internal details of implementation.
