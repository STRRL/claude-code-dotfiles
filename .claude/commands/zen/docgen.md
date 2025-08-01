---
description: "Comprehensive documentation generation with complexity analysis - systematic documentation with algorithmic complexity, call flow information, and gotcha identification"
argument-hint: "[class, function, or module to document]"
allowed-tools: ["zen"]
---

Generate comprehensive documentation with complexity analysis and gotcha identification for: $ARGUMENTS

**DOCUMENTATION STANDARDS**
Follow these principles:
1. **ALWAYS use MODERN documentation style** for the programming language:
   - Python: Use triple quotes for docstrings
   - **Objective-C: MANDATORY /// style** - NEVER use any other doc style
   - **Swift: MANDATORY /// style** - NEVER use any other doc style  
   - Java/JavaScript: Use /** */ JSDoc style
   - C++: Use /// for documentation comments
   - C#: Use /// XML documentation comments
   - Go: Use // comments above functions/types
   - Rust: Use /// for documentation comments
2. Document all parameters with types and descriptions
3. Include return value documentation with types
4. Add complexity analysis for non-trivial algorithms
5. Document dependencies and call relationships
6. Explain the purpose and behavior clearly
7. Add inline comments for complex logic within functions
8. **SURFACE GOTCHAS AND UNEXPECTED BEHAVIORS:** Document any non-obvious behavior, edge cases, or hidden dependencies

**COMPLEXITY ANALYSIS GUIDELINES**
- **MANDATORY:** Analyze time complexity (Big O notation) for every non-trivial function
- **MANDATORY:** Analyze space complexity when relevant (O(1), O(n), O(log n), etc.)
- Consider worst-case, average-case, and best-case scenarios where they differ
- Document complexity in a clear, standardized format within the function documentation
- Explain complexity reasoning for non-obvious cases
- Include complexity analysis even for simple functions (e.g., "Time: O(1), Space: O(1)")
- Use standard Big O notation: O(1), O(log n), O(n), O(n log n), O(n²), O(2^n), etc.

**CALL FLOW DOCUMENTATION**
- **MANDATORY:** Document which methods/functions this code calls (outgoing dependencies)
- **MANDATORY:** Document which methods/functions call this code (incoming dependencies) when discoverable
- Identify key dependencies and interactions between components
- Note side effects and state modifications (file I/O, network calls, global state changes)
- Explain data flow through the function (input → processing → output)
- Document any external dependencies (databases, APIs, file system, etc.)
- Note any asynchronous behavior or threading considerations

**GOTCHAS AND UNEXPECTED BEHAVIOR DOCUMENTATION**
Always look for and document:
- Parameter combinations that produce unexpected results or trigger special behavior
- Hidden dependencies on global state, environment variables, or external resources
- Order-dependent operations where calling sequence matters
- Silent failures or error conditions that might not be obvious
- Performance gotchas (e.g., operations that appear O(1) but are actually O(n))
- Thread safety considerations and potential race conditions
- Null/None parameter handling that differs from expected behavior
- Default parameter values that change behavior significantly
- Side effects that aren't obvious from the function signature
- Exception types that might be thrown in non-obvious scenarios
- Resource management requirements (files, connections, etc.)
- Platform-specific behavior differences
- Version compatibility issues or deprecated usage patterns

**FORMAT FOR GOTCHAS:**
Use clear warning sections in documentation:
```
Note: [Brief description of the gotcha]
Warning: [Specific behavior to watch out for]
Important: [Critical dependency or requirement]
```

**DOCUMENTATION EXAMPLES:**

**OBJECTIVE-C DOCUMENTATION (ALWAYS use ///):**
```
/// Processes user input and validates the data format
/// - Parameter inputData: The data string to validate and process
/// - Returns: ProcessedResult object containing validation status and processed data
/// - Complexity: Time O(n), Space O(1) - linear scan through input string
/// - Call Flow: Called by handleUserInput(), calls validateFormat() and processData()
/// - Note: Returns nil if inputData contains invalid UTF-8 sequences
- (ProcessedResult *)processUserInput:(NSString *)inputData;
```

**SWIFT DOCUMENTATION:**
```
/// Searches for an element in a sorted array using binary search
/// - Parameter target: The value to search for
/// - Returns: The index of the target element, or nil if not found
/// - Complexity: Time O(log n), Space O(1) - divides search space in half each iteration
/// - Call Flow: Called by findElement(), calls compareValues()
/// - Warning: Array must be sorted in ascending order for correct results
func binarySearch(target: Int) -> Int? { ... }
```

**SYSTEMATIC APPROACH**
1. **ANALYSIS & IMMEDIATE DOCUMENTATION:** Examine code structure, identify gaps, and ADD DOCUMENTATION as you go using MODERN documentation styles
2. **ITERATIVE IMPROVEMENT:** Continue analyzing while refining previously documented code with modern formatting
3. **STANDARDIZATION & POLISH:** Ensure consistency and completeness across all documentation using appropriate modern styles for each language

**COMPREHENSIVE DISCOVERY REQUIREMENT**
You MUST discover and document ALL functions, classes, and modules. Complete coverage is required.

**FINAL VERIFICATION:**
In your final step, you MUST:
1. Read through each file you documented
2. List every function, method, class, and property in each file
3. Confirm each has proper documentation including:
   - Modern documentation style appropriate for the language
   - Complexity analysis (Big O notation)
   - Call flow information
   - Parameter and return value documentation
4. If ANY items lack documentation, document them immediately before finishing
5. Provide a comprehensive accountability report showing exactly what was documented

Focus on creating documentation that makes the code more maintainable, understandable, and follows modern best practices for the specific programming language and project.